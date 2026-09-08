# Technischer Backlog

Dieser Backlog gliedert den aktuellen Entwurf in begutachtbare Arbeitspakete.
GitHub-Issues dienen als Ausführungsnachweis; diese Datei hält die geplante
Reihenfolge und die Zusammenhänge zwischen den Arbeitsbereichen fest.

Bedeutung der Prioritäten:

- **P0:** blockiert den nächsten sicheren oder technisch belastbaren Meilenstein.
- **P1:** für die erste integrierte Antriebsbasis erforderlich.
- **P2:** wertvolle Erweiterung nach Stabilisierung der Ausgangsbasis.

| ID | Priorität | Meilenstein | Arbeitspaket | Status | GitHub-Issue |
| --- | --- | --- | --- | --- | --- |
| MR-001 | P0 | M0 | Anforderungen und Abnahmekriterien der Antriebsbasis festlegen | Bereit | [#1](https://github.com/dynamo1807/Rover-Robot-Project/issues/1) |
| MR-002 | P0 | M1 | Mögliche 12-V-Encoder-Getriebemotoren charakterisieren | Bereit | [#2](https://github.com/dynamo1807/Rover-Robot-Project/issues/2) |
| MR-003 | P0 | M1 | Stromregelung und thermische Reserve des DRV8872 validieren | Blockiert durch MR-002 | [#3](https://github.com/dynamo1807/Rover-Robot-Project/issues/3) |
| MR-004 | P0 | M1 | Batterie-, Schutz- und Reglerarchitektur festlegen | Bereit | [#4](https://github.com/dynamo1807/Rover-Robot-Project/issues/4) |
| MR-005 | P0 | M1 | Vollständigen Motor- und Encoderkanal am STM32G431 prototypisch aufbauen | Blockiert durch MR-002/004 | [#5](https://github.com/dynamo1807/Rover-Robot-Project/issues/5) |
| MR-006 | P0 | M2 | Pin-, Timer- und DMA-Zuordnung des STM32G431 festlegen | Bereit | [#6](https://github.com/dynamo1807/Rover-Robot-Project/issues/6) |
| MR-007 | P0 | M2 | Schaltplanerfassung, ERC-Bereinigung und Entwurfsprüfung abschließen | In Bearbeitung | [#7](https://github.com/dynamo1807/Rover-Robot-Project/issues/7) |
| MR-008 | P0 | M2 | Platine Revision A routen und Layoutprüfung/DRC bestehen | Blockiert durch MR-003/004/006/007 | [#8](https://github.com/dynamo1807/Rover-Robot-Project/issues/8) |
| MR-009 | P1 | M2 | Bestellbare Stückliste und Beschaffungsalternativen erstellen | Blockiert durch MR-007 | [#9](https://github.com/dynamo1807/Rover-Robot-Project/issues/9) |
| MR-010 | P1 | M3 | Strombegrenzte Platineninbetriebnahme durchführen und Ergebnisse dokumentieren | Blockiert durch MR-008/009 | [#10](https://github.com/dynamo1807/Rover-Robot-Project/issues/10) |
| MR-011 | P1 | M4 | Reproduzierbares Firmwareprojekt und CI-Prüfungen einrichten | Bereit | [#11](https://github.com/dynamo1807/Rover-Robot-Project/issues/11) |
| MR-012 | P1 | M4 | Motortreiberansteuerung und deterministische Fehlerbehandlung implementieren | Blockiert durch MR-011 | [#12](https://github.com/dynamo1807/Rover-Robot-Project/issues/12) |
| MR-013 | P1 | M4 | Encodererfassung und Raddrehzahlschätzung implementieren | Blockiert durch MR-011 | [#13](https://github.com/dynamo1807/Rover-Robot-Project/issues/13) |
| MR-014 | P1 | M4 | Begrenzte PID-Raddrehzahlregelung implementieren und abstimmen | Blockiert durch MR-012/013 | [#14](https://github.com/dynamo1807/Rover-Robot-Project/issues/14) |
| MR-015 | P1 | M5 | Druckbares Antriebschassis konstruieren und verifizieren | Blockiert durch MR-002/004 | [#15](https://github.com/dynamo1807/Rover-Robot-Project/issues/15) |
| MR-016 | P2 | M6 | Erweiterungsschnittstellen für IMU und ToF definieren und validieren | Blockiert durch M4 | [#16](https://github.com/dynamo1807/Rover-Robot-Project/issues/16) |

## Empfohlene Ausführungsreihenfolge

1. MR-001, MR-002, MR-004 und MR-006 soweit möglich parallel abschließen.
2. Mit diesen Ergebnissen MR-003, MR-005 und MR-007 fertigstellen.
3. Die Platine über MR-008 und MR-009 zur Fertigung freigeben.
4. Die Hardware mit MR-010 in Betrieb nehmen und gleichzeitig mit MR-011 die Firmwarebasis schaffen.
5. MR-012 bis MR-014 vor den mechanischen Dauertests abschließen.
6. Das Chassis in MR-015 integrieren und anschließend MR-016 sowie Autonomiearbeiten priorisieren.

## Startkriterien

Ein Arbeitspaket ist bereit, wenn Problemstellung, relevante Eingaben oder
Abhängigkeiten, begrenzter Umfang und messbare Abnahmekriterien eindeutig sind
und keine ungeklärte Entscheidung die Umsetzungsrichtung beliebig macht.

## Fertigstellungskriterien

Ein Arbeitspaket ist abgeschlossen, wenn seine Abnahmekriterien erfüllt sind,
Quelldaten und Nachweise committet oder verknüpft wurden, die Dokumentation
geänderte Annahmen und Schnittstellen wiedergibt, Prüfanmerkungen geklärt sind
und kein bekannter P0-Sicherheitsfehler verbleibt.
