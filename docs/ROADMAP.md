# Projekt-Roadmap

Der Fortschritt richtet sich nach Nachweisen und Abschlusskriterien, nicht nur
nach erledigten Aufgaben. Spätere Meilensteine können präzisiert werden, wenn
Messungen die aktuellen Annahmen ersetzen.

## M0 — Anforderungen und Entwurfsbasis

**Ergebnis:** Der Umfang der ersten Antriebsbasis ist eindeutig und technisch begutachtbar.

Abschlusskriterien:

- Funktions- und Sicherheitsanforderungen sind dokumentiert;
- aktuelle Architektur und Schnittstellen sind dokumentiert;
- angenommene und offene Entscheidungen sind sichtbar;
- P0-Backlog-Einträge haben Verantwortliche oder eine eindeutige nächste Aktion;
- keine künftige Autonomiefunktion ist zur Validierung der Antriebsbasis erforderlich.

## M1 — Am Prüfstand validierter Antrieb

**Ergebnis:** Ein repräsentativer Motorkanal und beide Encoderkanäle sind vor
Freigabe der eigenen Platine verstanden.

Abschlusskriterien:

- elektrische Kenndaten, Drehzahl und Encoderdaten der ausgewählten Motoren wurden gemessen;
- Stromregelung und thermische Reserve des DRV8872 wurden nachgewiesen;
- ein G431-Entwicklungsboard steuert einen Motor mit dem vorgesehenen Befehlsschema;
- Encoderrichtung und Erfassung bei Höchstdrehzahl wurden geprüft;
- Stromversorgungsarchitektur und Schutzkonzept sind festgelegt.

## M2 — Platinenfreigabe

**Ergebnis:** Begutachtbare Fertigungsdaten für Controller-Platine Revision A.

Abschlusskriterien:

- MCU-Pin- und Timerzuordnung ist festgelegt;
- Schaltplanprüfung und ERC sind abgeschlossen;
- Layoutprüfung und DRC sind abgeschlossen;
- Stückliste, Alternativen, Fertigungsdaten und Bestückungshinweise wurden erzeugt;
- Inbetriebnahmereihenfolge und Messpunkte sind dokumentiert.

## M3 — Inbetriebnahme des Controllers

**Ergebnis:** Eine bestückte Platine ist elektrisch sicher und steuerbar.

Abschlusskriterien:

- Widerstandsprüfungen und erste Inbetriebnahme mit Strombegrenzung sind erfolgreich;
- alle Versorgungen, Reset, Takt, SWD und UART funktionieren;
- beide Motorkanäle und Encoder bestehen die ungeregelten Prüfungen;
- Fehlereingänge und sicheres Stoppverhalten funktionieren;
- Abweichungen der Inbetriebnahme sind dokumentiert und Schaltplankorrekturen zurückgeführt.

## M4 — Geregelte Antriebsbasis

**Ergebnis:** Die Drehzahlregelung beider Räder arbeitet unter repräsentativer Last zuverlässig.

Abschlusskriterien:

- reproduzierbare Firmware-Builds und grundlegende automatisierte Tests existieren;
- beide Raddrehzahlschätzer sind kalibriert;
- die PID-Antwort erfüllt festgelegte Nachführ- und Stabilitätsanforderungen;
- Befehlszeitüberschreitung, Watchdog und Fehlerinjektionstests funktionieren;
- Thermik- und Laufzeittests unter repräsentativer Last sind erfolgreich.

## M5 — Mechanische Integration

**Ergebnis:** Validierte Elektronik und Antrieb arbeiten im gedruckten Chassis.

Abschlusskriterien:

- CAD-Daten und Druckeinstellungen sind versioniert;
- Batterie, Platine, Motoren, Verkabelung und Zugentlastung sind sicher befestigt;
- Wartungszugang und Kühlung sind ausreichend;
- Geradeausfahrt, Wenden, Bremsen und Dauertest sind erfolgreich.

## M6 — Sensorbereiter Rover

**Ergebnis:** Die Antriebsbasis stellt stabile Schnittstellen für Autonomieexperimente bereit.

Abschlusskriterien:

- IMU- und ToF-Schnittstellen sind elektrisch und mechanisch validiert;
- Telemetrie mit Zeitstempeln und grundlegende Odometrie sind verfügbar;
- Sensorfehler beeinträchtigen den sicheren manuellen Betrieb oder Prüfstandsbetrieb nicht;
- der nächste Autonomiemeilenstein besitzt eindeutige Anforderungen.

Mögliche spätere Arbeiten umfassen Hindernisvermeidung, Sensorfusion,
Funksteuerung, Kameraintegration, Kartierung/SLAM und einen Manipulator. Sie
gelten erst dann als zugesagt, wenn sie in den aktiven Backlog aufgenommen wurden.
