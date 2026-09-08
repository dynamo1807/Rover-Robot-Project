# Verifikationsplan

## Zweck

Verifikation macht aus Aussagen belastbare Nachweise. Jede Prüfung enthält
einen kontrollierten Aufbau, das erwartete Ergebnis, das Messergebnis, eine
Schlussfolgerung und bei Bedarf Verknüpfungen zu Rohdaten. Prüfungen mit einem
bestromten Motor oder Akku beginnen mit Strombegrenzung und einem mechanisch
gesicherten Aufbau.

## Verifikationsmatrix auf Anforderungsebene

| ID | Anforderung | Verifikationsmethode | Geplante Phase |
| --- | --- | --- | --- |
| VR-001 | Die Firmware kann jeden Motor unabhängig in beide Richtungen ansteuern und stoppen | Prüfstandsvorführung und Telemetrie | M1/M3 |
| VR-002 | Die Encoderrichtung entspricht der festgelegten Radkonvention | Integrationstest am Zielsystem | M1/M3 |
| VR-003 | Die Encodererfassung verliert bei der vorgesehenen Höchstdrehzahl keine Zählwerte | Referenzmessung und Zählerprotokolle | M1 |
| VR-004 | Die Stromregelung des Treibers begrenzt den Strom auf den vorgesehenen Wert | Oszilloskop- und Strommessung | M1 |
| VR-005 | Treiber- und Platinentemperaturen bleiben innerhalb der Entwurfsgrenzen | Lastfall- und Thermikprüfung unter ungünstigsten Bedingungen | M1/M4 |
| VR-006 | Alle Logikversorgungen bleiben bei Start, Stopp und Richtungswechsel innerhalb der Toleranz | Oszilloskopaufnahme | M1/M3 |
| VR-007 | Ein Treiberfehler schaltet das Drehmoment ab und wird gemeldet | Fehlerinjektionstest | M3/M4 |
| VR-008 | Befehlszeitüberschreitung oder Watchdog-Ablauf führt zu einem sicheren Stopp | Firmware-Integrationstest | M4 |
| VR-009 | Die Raddrehzahlregelung ist stabil und hält die festgelegten Nachführgrenzen ein | Bericht zu Sprung- und Störantwort | M4 |
| VR-010 | SWD und UART bleiben am montierten Rover zugänglich | Inspektion und Funktionstest | M3/M5 |
| VR-011 | Batterie und Verkabelung bleiben mechanisch befestigt und geschützt | Inspektion und Bewegungstest | M5 |
| VR-012 | Die integrierte Antriebsbasis beendet den festgelegten Dauertest ohne unsicheren Fehler | Dauertest | M5 |

Numerische Toleranzen für Versorgungsspannung, Strom, Temperatur,
Drehzahlfehler, Einschwingzeit und Dauer des Belastungstests werden in MR-001
festgelegt, sobald Messungen eine belastbare Wahl ermöglichen.

## Sicherheitscheckliste für den Prüfstand

- Für die erste Inbetriebnahme ein strombegrenztes Labornetzteil verwenden.
- Den Motor sichern und die Räder von der Arbeitsfläche fernhalten.
- Eine erreichbare Trennmöglichkeit der Stromversorgung vorsehen.
- Mit niedrigen Spannungs- und Stromgrenzen sowie deaktivierten Ausgängen beginnen.
- Vor dem Einschalten Polarität und Widerstand prüfen.
- Versorgungsstrom und kritische Temperaturen überwachen.
- Einen Motor nicht länger blockieren, als es das festgelegte Prüfverfahren erlaubt.
- Tastkopfmassen dokumentieren und versehentliche Kurzschlüsse der Motorversorgung vermeiden.

## Reihenfolge der Platineninbetriebnahme

1. Sicht- und Bestückungsprüfung durchführen.
2. Im stromlosen Zustand alle Versorgungsschienen auf Widerstand prüfen.
3. Eingang mit Strombegrenzung und abgeklemmten Motorausgängen versorgen.
4. Logikversorgungen sowie Reset- und Taktverhalten prüfen.
5. SWD-Verbindung herstellen und Minimalfirmware laden.
6. UART-Diagnose und alle sicheren GPIO-Standardzustände prüfen.
7. Treiberlogik und Fehlereingänge ohne Motor testen.
8. Einen Motor mit reduzierten Grenzwerten anschließen und ungeregelt testen.
9. Erst einen Encoder und danach den zweiten Kanal validieren.
10. Erst nach Bestehen der vorherigen Schritte mit Entwurfsspannung und repräsentativer Last wiederholen.

## Vorlage für Prüfprotokolle

```markdown
# Prüfung: <Kennung und Titel>

- Datum / ausführende Person:
- Hardware-Revision:
- Firmware-Commit:
- Messmittel:
- Aufbau und Grenzwerte:
- Abnahmekriterien:
- Vorgehen:
- Ergebnisse:
- Rohdaten/Nachweise:
- Abweichungen:
- Schlussfolgerung: BESTANDEN / NICHT BESTANDEN / BLOCKIERT
- Folge-Issues:
```
