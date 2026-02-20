# Fazit und Ausblick

## Zusammenfassung der Ergebnisse

Im Rahmen dieser Diplomarbeit wurde ein vollständiges System zur automatisierten Kennzeichenerkennung und Verkehrsanalyse für die Zotter Schokolade GmbH konzipiert, implementiert und in den Produktivbetrieb überführt. 
Dieses erfasst durchfahrende Fahrzeuge an der Betriebszufahrt mittels einer IP-Kamera, erkennt deren Kennzeichen über eine lokal betriebene ALPR-Lösung und speichert die anonymisierten Daten in einer PostgreSQL-Datenbank. 
Die gesammelten Daten werden über ein Grafana-Dashboard visualisiert.

Das System läuft seit dem 8. August 2025, mit Ausnahme von kleineren Ausfällen, durchgehend im Produktivbetrieb.
Bis zur Verfassung dieser Dokumentation (Februar 2026) wurden über 60.000 Fahrzeugkennzeichen erfasst. 
Die dabei erzielten Erkennungsdaten sind als Richtwerte zu verstehen und nicht als absolute Kennzahlen, da eine vollständige Referenzmessung, also der Abgleich jeder einzelnen Durchfahrt mit der entsprechenden Erkennung, im Rahmen dieser Arbeit nicht durchgeführt wurde. 
Wie im Kapitel Qualitätssicherung (!! Cross Reference) erläutert, ist die Dunkelziffer nicht erfasster Fahrzeuge nicht exakt bezifferbar.


## Kritische Reflexion

Die Microservice-Architektur hat sich als passend für das Projekt erwiesen, da sie eine klare Trennung der Verantwortlichkeiten ermöglicht und einzelne Komponenten unabhängig voneinander entwickelt werden konnten. 
Die Wahl der Synology DVA-Serie als Hardware-Plattform hat sich insofern bewährt, als sie sowohl die Kameraverwaltung als auch die Docker-basierte Applikation auf einer einzigen Hardware vereint. 
Die lokale Bildverarbeitung durch den Plate Recognizer SDK-Container gewährleistet, dass keinerlei Bilddaten das lokale Netzwerk verlassen, was den Datenschutzanforderungen vollständig entspricht.

(!! Was noch gut lief, persönliche Punkte, z.B.:
MkDocs / Documentation-as-Code Ansatz?
Automatisiertes Backup?
CI/CD Pipeline?
Zusammenarbeit mit dem Unternehmen?)
Was man rückblickend anders machen würde:

Würde man eine andere Kamera / anderes NAS wählen?
Hat die DVA genug Rechenleistung oder war sie am Limit?
Wäre ein anderes ALPR-Modell besser gewesen?
Hätte man von Anfang an einen Analytics-Service fertig implementieren sollen?
War Python/FastAPI die richtige Wahl oder hätte etwas anderes besser gepasst?
Gab es Features, die aufwändiger waren als erwartet?

Zielerreichung:

(!! Die funktionalen und nicht-funktionalen Anforderungen aus dem Anforderungskapitel durchgehen:
Automatisierte Erkennung zuverlässig umgesetzt?
Datenschutz gewährleistet (Anonymisierung, lokale Verarbeitung)?
Echtzeitvisualisierung über Dashboard?
Benachrichtigungssystem?
Automatisierter Betrieb ohne manuelle Eingriffe?
usw.)


## Ausblick

Erweiterungsmöglichkeiten (z.B. KI-Modelle direkt auf der Hardware, App-Anbindung)
