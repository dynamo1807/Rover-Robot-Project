# Technisches Entscheidungsprotokoll

Dieses kompakte Protokoll hält die Entwurfsbasis fest, ohne unbestätigte
Annahmen als endgültig darzustellen. Eine Entscheidung wechselt erst von
**Vorgeschlagen** zu **Angenommen**, wenn ihre Folgen und die erforderlichen
Nachweise verstanden sind.

| ID | Status | Entscheidung | Begründung | Anlass zur Neubewertung |
| --- | --- | --- | --- | --- |
| D-001 | Angenommen | STM32G431 als Controllerfamilie verwenden; auf der eigenen Platine den STM32G431CBT6 vorsehen | Motorsteuerungs-Timer, Analogfunktionen, Leistung und ein praktikabler Nucleo-Prototyppfad | Konflikt bei Pins/Ressourcen oder Bauteil nicht verfügbar |
| D-002 | Angenommen | Einen DRV8872 pro Motor verwenden | Unabhängige bidirektionale Kanäle mit Stromregelung und Fehlermeldung | Gemessene Motor- oder Thermikgrenzen werden nicht eingehalten |
| D-003 | Vorgeschlagen | Zwei 12-V-Metallgetriebemotoren der Klasse GA25/JGA25-370 mit AB-Hall-Encodern und etwa 100–130 U/min verwenden | Passende Baugröße, Encoderverfügbarkeit und einfacher Differentialantrieb | Messungen aus MR-002 oder Chassisanforderungen werden nicht erfüllt |
| D-004 | Angenommen | Für die erste Plattform einen Differentialantrieb verwenden | Mechanisch einfach und mit unabhängiger Raddrehzahlregelung vereinbar | Gelände- oder Nutzlastanforderung ändert sich |
| D-005 | Angenommen | Vor Bestellung der eigenen Platine mit einem G431-Entwicklungsboard validieren | Verringert gleichzeitige Unsicherheit bei Hardware und Firmware | Keiner; dies ist eine Maßnahme zur Risikobegrenzung |
| D-006 | Vorgeschlagen | I2C-/GPIO-Schnittstellen für IMU- und ToF-Erweiterungen reservieren | Ermöglicht spätere Autonomie, ohne sie an den ersten Erfolg der Antriebsbasis zu koppeln | Pin- oder Strombudget reicht nicht aus |
| D-007 | Offen | Batteriechemie, Zellenzahl, Schutz, Laden und Regelung | Verifizierte Last- und Laufzeitdaten reichen noch nicht aus | In MR-004 klären |
| D-008 | Offen | Firmware-Buildsystem und Grenze zwischen STM32 HAL und LL | Anforderungen an Reproduzierbarkeit und Prüfbarkeit müssen bewertet werden | In MR-011 klären |

## Entscheidungsverfahren

1. Entscheidung und brauchbare Alternativen benennen.
2. Randbedingungen, Nachweise und Folgen dokumentieren.
3. Das zuständige GitHub-Issue verknüpfen.
4. Die Entscheidung erst nach Erfüllung ihrer Abnahmekriterien als angenommen markieren.
5. Bei Ablösung den alten Eintrag erhalten und die neue Entscheidung verknüpfen.
