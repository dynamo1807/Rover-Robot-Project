# Mitwirken

Beiträge sollen den Rover verbessern und zugleich die Nachvollziehbarkeit
zwischen Problem, Entwurfsentscheidung, geändertem Quellstand und
Verifikationsnachweis erhalten.

## Arbeitsablauf

1. Ein GitHub-Issue mit messbaren Abnahmekriterien erstellen oder auswählen.
2. Sicherstellen, dass blockierende Entscheidungen und Abhängigkeiten geklärt sind.
3. Einen fokussierten Branch wie `hardware/mr-007-schematic-review` oder
   `firmware/mr-013-encoder-driver` anlegen.
4. Quelldateien und Dokumentation in kleinen, zusammenhängenden Änderungen committen.
5. Die Änderung anhand der zutreffenden Checkliste oder des Prüfplans verifizieren.
6. Einen Pull Request eröffnen, der das Issue verknüpft und Nachweise enthält.

Direkte Commits auf `main` sollten auf die Repository-Verwaltung oder eine
anfängliche Projektbasis beschränkt bleiben. Produktänderungen sollen über
begutachtbare Branches erfolgen.

## Commit-Nachrichten

Einen imperativen Betreff mit optionalem Geltungsbereich verwenden:

```text
docs: Architektur- und Verifikationsbasis festlegen
hardware: Strombegrenzung des DRV8872 berechnen
firmware: Quadratur-Encodererfassung implementieren
mechanical: Motorhalterung Revision B ergänzen
```

Die Arbeitspaket-ID im Text nennen, wenn der Zusammenhang nicht eindeutig ist.

## Regeln für verbindliche Quelldaten

- Editierbare KiCad-, CAD- und Firmware-Quellen committen.
- Quelldaten nicht durch Bildschirmfotos oder exportierte PDFs ersetzen.
- Erzeugte Fertigungsdaten gehören in einen eindeutig benannten Release-Ordner
  und müssen die Quellrevision nennen, aus der sie erzeugt wurden.
- Messwerte mit Einheit, Aufbau, Messgerät und – falls entscheidungsrelevant –
  Messunsicherheit dokumentieren.
- Niemals Zugangsdaten, private SSH-Schlüssel, Token oder persönliche
  Konfiguration committen.

## Checkliste für die Hardwareprüfung

- [ ] Anforderungen und Annahmen sind verknüpft.
- [ ] Datenblattgrenzen wurden für Minimal- und Maximalbedingungen geprüft.
- [ ] Leistungs- und Strombilanzen verwenden ungünstigste Fallwerte.
- [ ] Steckerbelegungen und Polaritäten sind dokumentiert.
- [ ] Die ERC-/DRC-Ausgabe enthält keine ungeklärten Meldungen.
- [ ] Testpunkte und Zugänge für die Inbetriebnahme sind ausreichend.
- [ ] Stücklisteneinträge sind bestellbar und enthalten nach Möglichkeit Alternativen.
- [ ] Der Verifikations- oder Inbetriebnahmeplan deckt die geänderte Schaltung ab.

## Checkliste für die Firmwareprüfung

- [ ] Öffentliche Schnittstellen und Einheiten sind eindeutig.
- [ ] Fehlerpfade und Initialisierungsfehler werden behandelt.
- [ ] Aktorausgänge sind begrenzt und standardmäßig sicher.
- [ ] Interruptpfade sind zeitlich begrenzt und nicht blockierend.
- [ ] Relevante Host- oder Zielsystemtests sind erfolgreich.
- [ ] Compilerwarnungen sind behoben.
- [ ] Telemetrie oder andere Nachweise zeigen bei Bedarf das Verhalten auf dem Zielsystem.
- [ ] Die Dokumentation bildet geändertes Verhalten oder Timing ab.

## Fertigstellungskriterien

Eine Änderung ist fertig, wenn:

- alle Abnahmekriterien des Issues erfüllt sind;
- erforderliche Quellen, Berechnungen und Nachweise committet oder verknüpft sind;
- betroffene Dokumentation und Entscheidungen aktuell sind;
- Kommentare aus der Begutachtung geklärt sind;
- die Verifikation reproduzierbar ist;
- kein bekannter P0-Sicherheitsfehler oder veröffentlichungsblockierender Defekt besteht.

## Sicherheitsbedenken melden

Für Sicherheitsbedenken auf Entwurfsebene, die kein Sicherheitsgeheimnis
offenlegen, ein Issue erstellen. Keine privaten Zugangsdaten oder sensiblen
personenbezogenen Informationen in Issues, Commits oder Prüfprotokolle aufnehmen.
