# Elektronikentwurf

## Entwicklungsreife

Die Elektronik befindet sich in der Schaltplan- und Validierungsphase. Die
folgenden Bauteilfamilien bilden die aktuelle Ausgangsbasis. Der Entwurf ist
jedoch erst für die Platinenfertigung bereit, wenn die P0-Messungen und
Begutachtungen abgeschlossen sind.

## Ausgangskomponenten

| Funktion | Aktuelle Ausgangsbasis | Erforderliche Validierung |
| --- | --- | --- |
| Haupt-MCU | STM32G431CBT6, LQFP-48 | Pin-/Timerzuordnung, Versorgungsstrom, Taktbaum |
| Prototyp-MCU | NUCLEO-G431RB oder gleichwertig | Prototyppins den Peripheriefunktionen der endgültigen MCU zuordnen |
| Motortreiber | 2 × DRV8872 | Stromregelung, Spitzenstrom, thermische Reserve |
| Motoren | 12-V-Klasse GA25/JGA25-370, AB-Hall-Encoder | Leerlauf-/Blockierstrom, Drehzahl, Encoder-CPR, Polarität |
| Debug | SWD und UART | Steckverbinder, Pinbelegung, Schutz, Zugänglichkeit |
| Sensoren | I2C-/GPIO-Erweiterung | Spannung, Pull-ups, Steckverbinder, Adresskonflikte |

## Spannungsbereiche

Das aktuelle Konzept enthält mindestens folgende Bereiche:

- einen Batterieeingangsbereich;
- einen nominellen 12-V-Motorbereich;
- einen Logikbereich für den STM32;
- optionale Sensorversorgungen.

Batteriesystem und Logikwandlung sind bewusst **noch nicht festgelegt**. Die
Aufgabe zur Stromversorgungsarchitektur muss Eingangsspannungsbereich,
Verpolschutz, Sicherung oder Stromschutz, Transientenunterdrückung, zentrale
und lokale Entkopplung, Logikregler, Einschaltreihenfolge,
Batterieüberwachung, Ladegrenzen und einen sicheren Hauptschalter festlegen.

## Motorkanäle

Jeder Motor besitzt einen eigenen DRV8872-Kanal. Vor Festlegung des Schaltplans:

1. Leerlauf-, Last- und Blockierstrom des Motors bei der vorgesehenen Spannung messen;
2. Bauteile der Treiber-Stromregelung auswählen und berechnen;
3. nachweisen, dass Strom- und Temperaturgrenzen eingehalten werden;
4. PWM-Frequenz und Verhalten der Eingangswahrheitstabelle prüfen;
5. Freilauf-, Brems-, Auslauf- und Fehlerverhalten bestätigen;
6. Kupferflächen, Steckverbinder, Schutz und Entkopplung nach dem gemessenen Strom dimensionieren.

Motorsteckverbinder dürfen nicht allein anhand des Nennstroms ausgewählt oder
dimensioniert werden.

## Encodereingänge

Jeder Motor stellt A/B-Signale eines Hall-Encoders bereit. Für die endgültige
Schnittstelle müssen folgende Punkte dokumentiert werden:

- Versorgungsspannung und Ausgangstopologie des Encoders;
- Anforderungen an Pull-up-Widerstände;
- Impulse beziehungsweise Zählwerte pro Motor- und Getriebeumdrehung;
- zulässige STM32-Eingangsspannung;
- Timerkanäle und Alternativfunktionen;
- erforderliche Filterung oder Hysterese für die tatsächliche Kabellänge;
- Steckerbelegung sowie Polaritätskonvention für Motor und Encoder.

Der Quadraturmodus der Timer wird bevorzugt. Ein Prüfstandsversuch muss das
korrekte Vorzeichen der Zählung, lückenlose Erfassung bei Höchstdrehzahl und
stabiles Verhalten bei Drehzahl null nachweisen.

## Schaltplankonventionen

Eindeutige und einheitliche Netznamen verwenden:

```text
M1_IN1      M1_IN2      M1_FAULT      ENC1_A      ENC1_B
M2_IN1      M2_IN2      M2_FAULT      ENC2_A      ENC2_B
MOTOR_12V   +3V3        GND
```

Die Richtung eines globalen Labels ist eine ERC-Metainformation und keine
elektrische Diode. Ein Label als Ausgang kennzeichnen, wenn die lokale Schaltung
es treibt, und als Eingang, wenn die lokale Schaltung es empfängt.

Der `nFAULT`-Ausgang des DRV8872 darf nicht direkt mit GND verbunden werden. Er
muss an einen benannten MCU-Fehlereingang angeschlossen werden und die für die
gewählte Treiberkonfiguration erforderliche Pull-up-Schaltung verwenden.

`PWR_FLAG` nur einsetzen, wenn eine externe oder anderweitig passive Quelle ein
KiCad-Stromversorgungsnetz tatsächlich speist. Dasselbe Stromversorgungsnetz
nicht mit mehreren konkurrierenden Namen versehen.

## Mindestbeschaltung der MCU

Die abschließende Schaltplanprüfung umfasst:

- alle Versorgungs- und Massepins aus dem STM32-Datenblatt;
- lokale Entkopplungs- und zentrale Pufferkondensatoren;
- Reset- und Boot-Konfiguration;
- SWD-Steckverbinder, Massebezug und optionalen Reset;
- einen externen Takt nur bei nachvollziehbarer Begründung;
- UART-Debug-Schnittstelle;
- zugängliche Messpunkte für jede Versorgung und jedes kritische Steuersignal;
- Behandlung unbenutzter Pins;
- zu externen Steckverbindern passenden ESD- und Transientenschutz.

## Freigabekriterien für die Platine

Die Platine darf erst freigegeben werden, wenn:

- der Prüfstandsbericht zu Motor und Treiber am zugehörigen Issue hängt;
- Leistungsbudget und ungünstigster Eingangsspannungsbereich geprüft sind;
- alle MCU-Pins und Timerressourcen zugeordnet sind;
- KiCad ERC keine ungeklärten Fehler oder Warnungen enthält;
- die Checklisten zur Fremd- oder Eigenprüfung aller Schaltplanseiten abgeschlossen sind;
- Steckerbelegungen und Polaritäten dokumentiert sind;
- Platinenregeln und Netzklassen die tatsächlichen Ströme abbilden;
- die Fertigungsstückliste bestellbare Teilenummern und Alternativen enthält;
- der Inbetriebnahmeplan in [VERIFICATION.md](VERIFICATION.md) umsetzbar ist.
