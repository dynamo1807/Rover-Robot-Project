# Hardware

Dieses Verzeichnis ist die verbindliche Quelle für die Rover-Elektronik.

Geplante Struktur:

```text
hardware/
├── pcb/                  KiCad-Projekt und eigene Bibliotheken
├── bom/                  geprüfte Stückliste und Beschaffungsalternativen
├── calculations/         Berechnungen zu Leistung, Strom, Thermik und Schutz
├── manufacturing/        versionierte Fertigungsdaten
└── tests/                Hardware-Prüfverfahren und zusammengefasste Ergebnisse
```

Keine erzeugten KiCad-Sicherungen oder lokalen Editoreinstellungen committen.
Fertigungsdaten müssen die Hardware-Revision und den Quell-Commit nennen, aus
dem sie erzeugt wurden.

Die elektrische Ausgangsbasis und die Freigabekriterien der Platine sind in
[`docs/ELECTRONICS.md`](../docs/ELECTRONICS.md) festgelegt.
