# Erste Messungen und vorläufige Kalibrierung der Motoren mit Hallencoder

Zugehöriges Arbeitspaket: [MR-002 – Motorcharakterisierung](https://github.com/dynamo1807/Rover-Robot-Project/issues/2).

## Stand und Versuchsaufbau

Erste Auswertung eines Hallencoder-Kanals anhand des bereitgestellten Arduino-Sketches und eines Screenshots des seriellen Monitors. Dies ist ein vorläufiger Messbericht, keine abgeschlossene Kalibrierung beider Rover-Motoren und keine Verifikation der geplanten STM32-Firmware.

| Parameter | Wert |
| --- | --- |
| Encoder A / B | Pins 2 / 3, jeweils INPUT_PULLUP |
| Auswertung | X4, CHANGE-Interrupts auf beiden Kanälen |
| Vorläufige Auflösung | 3894 Counts pro Umdrehung |
| Auswerteintervall | mindestens 500000 µs = 500 ms |
| Serielle Ausgabe | 9600 Baud |

Der Projekteigner hat den **Zeng WHCD JGB37-520 in der Variante 12 V / 110 RPM mit Hallencoder** ausgewählt (siehe [D-009](DECISIONS.md#d-009--motorauswahl-für-mr-002-2026-10-23)). Diese Angabe beschreibt die ausgewählte Variante, keine unabhängig bestätigte Drehzahl. Board, Zuordnung des gemessenen Exemplars zu M1/M2, tatsächliche Versorgungsspannung im Versuch, Last, Messdatum und Referenzmessgerät sind noch nicht angegeben. Ebenso ist noch festzuhalten, ob die Counts pro Umdrehung auf Motorwelle oder Getriebeabtrieb bezogen sind. Der Sketch erfasst einen Motor; getrennte Nachweise für beide Motoren stehen aus. Er steuert den Motor nicht an.

## Auswerteverfahren

Beide Encoderpegel werden zu einem Zweibit-Zustand zusammengefasst. Eine Tabelle bewertet den Übergang vom vorherigen zum aktuellen Zustand mit +1, −1 oder 0. Damit werden bei gültigen Quadraturübergängen beide Flanken beider Kanäle gezählt (X4). Ungültige Zweibit-Sprünge liefern 0; der Sketch führt keinen separaten Fehlerzähler.

Der gemeinsame Zähler wird für die Auswertung bei kurz gesperrten Interrupts kopiert. Aus der Zählerdifferenz und der tatsächlich verstrichenen Zeit ergibt sich:

```text
deltaCounts = currentCount - lastCount
deltaTime_s = elapsed_us / 1000000
RPM = (deltaCounts / COUNTS_PER_REV) × (60 / deltaTime_s)
```

Positive Werte werden als „Vorwaerts“, negative als „Rueckwaerts“ ausgegeben. Diese Bezeichnung hängt von Anschlussfolge und Einbaulage ab und muss mit der gewünschten Fahrtrichtung abgeglichen werden. „Stillstand“ bedeutet hier lediglich, dass die Netto-Zählerdifferenz im Messfenster null ist.

## Erste Messergebnisse

Transkription der bereitgestellten seriellen Ausgabe:

```text
Drehzahl: 0.00 RPM | Richtung: Stillstand | Encoder: 0
Drehzahl: -68.90 RPM | Richtung: Rueckwaerts | Encoder: -2236
Drehzahl: -111.15 RPM | Richtung: Rueckwaerts | Encoder: -5843
Drehzahl: -111.65 RPM | Richtung: Rueckwaerts | Encoder: -9466
Drehzahl: -111.83 RPM | Richtung: Rueckwaerts | Encoder: -13095
Drehzahl: -111.93 RPM | Richtung: Rueckwaerts | Encoder: -16727
Drehzahl: -111.99 RPM | Richtung: Rueckwaerts | Encoder: -20361
Drehzahl: -112.02 RPM | Richtung: Rueckwaerts | Encoder: -23996
```

Nach dem ersten Messfenster mit Bewegung nähert sich die berechnete Anzeige etwa −112 RPM. Die letzte Zählerdifferenz beträgt −3635 Counts; bei etwa 0,5 s und 3894 Counts/Umdrehung entspricht das rund −112,02 RPM. Die Werte sind damit rechnerisch plausibel. Die zwei angezeigten Nachkommastellen belegen keine entsprechende Messgenauigkeit.

Die kurze Messreihe bestätigt weder die tatsächliche Drehzahl noch die Auflösung von 3894 Counts/Umdrehung. Auch verlustfreie Erfassung bei maximaler Drehzahl, beide Drehrichtungen und das Verhalten des zweiten Motors sind damit noch nicht nachgewiesen. VR-002 und VR-003 aus dem [Verifikationsplan](https://github.com/dynamo1807/Rover-Robot-Project/blob/main/docs/VERIFICATION.md) bleiben offen.

## Kalibrierung fortsetzen

1. Motor und Board eindeutig identifizieren; Versorgung, Last und Encoderverdrahtung protokollieren. Am verwendeten Board müssen beide Pins externe Interrupts unterstützen; Encoderpegel und Versorgung müssen zu den Eingängen passen.
2. Bezugswelle festlegen und markieren: Motorwelle oder Getriebeabtrieb/Radwelle.
3. Anfangszähler erfassen, beispielsweise zehn vollständige Umdrehungen in einer Richtung ausführen und den Endzähler erfassen.
4. `COUNTS_PER_REV = abs(Endzähler - Anfangszähler) / Anzahl_Umdrehungen` bestimmen. Dieser Wert enthält bereits die X4-Auswertung; nicht nochmals mit vier multiplizieren.
5. Mehrfach und in beiden Richtungen wiederholen; Streuung, Zählerdifferenzen und Umdrehungszahl festhalten. Beide Motoren separat prüfen.
6. Drehzahl gegen eine unabhängige Referenz messen und bei den vorgesehenen Drehzahlen auf Zählverluste prüfen. Vorzeichen zur tatsächlichen Vorwärtsfahrt zuordnen.
7. Erst anschließend den bestätigten Wert samt Bezugswelle und Messunsicherheit übernehmen.

## Verwendeter Sketch

Vom Anwender bereitgestellter Versuchsstand; hier dokumentiert, nicht auf Zielhardware neu kompiliert oder getestet.

```cpp
const byte encoderA = 2;
const byte encoderB = 3;

// Vorlaeufige X4-Aufloesung
// Muss durch Kalibrierung bestaetigt werden
const float COUNTS_PER_REV = 3894.0;

volatile long encoderCount = 0;
volatile byte lastState = 0;

const int8_t transitionTable[16] = {
   0, -1,  1,  0,
   1,  0,  0, -1,
  -1,  0,  0,  1,
   0,  1, -1,  0
};

unsigned long lastTime = 0;
long lastCount = 0;

const unsigned long INTERVAL = 500000UL; // 500 ms

void updateEncoder() {
  byte a = digitalRead(encoderA);
  byte b = digitalRead(encoderB);

  byte currentState = (a << 1) | b;
  byte transition = (lastState << 2) | currentState;

  encoderCount += transitionTable[transition];
  lastState = currentState;
}

void setup() {
  Serial.begin(9600);

  pinMode(encoderA, INPUT_PULLUP);
  pinMode(encoderB, INPUT_PULLUP);

  lastState = (digitalRead(encoderA) << 1)
            | digitalRead(encoderB);

  attachInterrupt(
    digitalPinToInterrupt(encoderA),
    updateEncoder,
    CHANGE
  );

  attachInterrupt(
    digitalPinToInterrupt(encoderB),
    updateEncoder,
    CHANGE
  );

  lastTime = micros();

  Serial.println("Motor-Drehzahlmessung gestartet");
}

void loop() {
  unsigned long currentTime = micros();
  unsigned long elapsed = currentTime - lastTime;

  if (elapsed >= INTERVAL) {

    noInterrupts();
    long currentCount = encoderCount;
    interrupts();

    long deltaCounts = currentCount - lastCount;

    float deltaTime = elapsed / 1000000.0;

    float rpm = ((float)deltaCounts / COUNTS_PER_REV)
                * (60.0 / deltaTime);

    Serial.print("Drehzahl: ");
    Serial.print(rpm, 2);
    Serial.print(" RPM");

    Serial.print(" | Richtung: ");

    if (rpm > 0) {
      Serial.print("Vorwaerts");
    }
    else if (rpm < 0) {
      Serial.print("Rueckwaerts");
    }
    else {
      Serial.print("Stillstand");
    }

    Serial.print(" | Encoder: ");
    Serial.println(currentCount);

    lastCount = currentCount;
    lastTime = currentTime;
  }
}
```

Für längere Versuche sind zusätzlich der Überlauf des vorzeichenbehafteten Zählers und für genaue Zeitzuordnung die getrennte Erfassung von Zeit und Zähler zu berücksichtigen. Die unsigned Zeitdifferenz behandelt den normalen micros()-Überlauf, sofern regelmäßig ausgewertet wird. Die Grenzen der Interrupt-Auswertung müssen auf dem tatsächlich verwendeten Board geprüft werden.
