# Fazit und Ausblick

## Zusammenfassung der Ergebnisse

Im Rahmen dieser Diplomarbeit wurde ein vollständiges System zur automatisierten Kennzeichenerkennung und Verkehrsanalyse für die Zotter Schokolade GmbH konzipiert, implementiert und in den Produktivbetrieb überführt. 
Dieses erfasst durchfahrende Fahrzeuge an der Betriebszufahrt mittels einer IP-Kamera, erkennt deren Kennzeichen über eine lokal betriebene ALPR-Lösung und speichert die anonymisierten Daten in einer PostgreSQL-Datenbank. 
Die gesammelten Daten werden über ein Grafana-Dashboard visualisiert.

Das System läuft seit dem 8. August 2025, mit Ausnahme von kleineren Ausfällen, durchgehend im Produktivbetrieb.
Bis zur Verfassung dieser Dokumentation (Februar 2026) wurden über 60.000 Fahrzeugkennzeichen erfasst. 
Die dabei erzielten Erkennungsdaten sind als Richtwerte zu verstehen und nicht als absolute Kennzahlen, da eine vollständige Referenzmessung, also der Abgleich jeder einzelnen Durchfahrt mit der entsprechenden Erkennung, im Rahmen dieser Arbeit nicht durchgeführt wurde. 
Wie im Kapitel Qualitätssicherung (!! Cross Reference) erläutert, ist die Dunkelziffer nicht erfasster Fahrzeuge aus diesem Grund nicht exakt bezifferbar.

Die für diese Diplomarbeit gesetzten Ziele wurden wie in dieser Dokumentation direkt oder indirekt beschrieben nach bestem Wissen und Gewissen erfüllt.

Der Ansatz der hybriden Microservice-Architektur hat sich als passend für das Projekt erwiesen, da dieser eine klare Trennung der Verantwortlichkeiten ermöglicht und einzelne Komponenten unabhängig voneinander entwickelt werden konnten.
Dennoch vereinfacht dieser Ansatz der zentralen Datenbank die Komplexität im Vergleich zu einer klassischen Microservice-Architektur erheblich.
Ebenso bewährte sich die Wahl der Synology DVA-Serie als Hardware-Plattform, da sie sowohl die Kameraverwaltung als auch die Docker-basierte Applikation auf einem einzigen Gerät vereint. 
Die lokale Bildverarbeitung durch den Plate Recognizer SDK-Container gewährleistet, dass keinerlei Bilddaten das lokale Netzwerk verlassen, was den Datenschutzanforderungen vollständig entspricht.


## Ausblick

Neben den offensichtlichen Erweiterungsmöglichkeiten wie der Fertigstellung der konzipierten, aber noch nicht implementierten Services, wurden im Laufe der Konzeptionsphase einige Vorschläge erwogen, welche zukünftig in das System integriert werden könnten:

- Vollständige Implementierung des Web-Frontends: Die Ablösung von Grafana durch die geplante Next.js-Applikation würde eine dedizierte Benutzeroberfläche bieten, die nicht nur der Visualisierung dient, sondern auch die Verwaltung von Benachrichtigungseinstellungen und Systemkonfigurationen ermöglichen könnte.
- Tiefere Hardware-Integration mit lokalen Modellen: Aktuell wird die KI-Leistung der Synology DVA primär für die Fahrzeugerkennung genutzt, während das ALPR-Modell in einem separaten Container läuft. Zukünftig könnten KI-Modelle zur Kennzeichenerkennung direkt auf stärkerer Hardware laufen, um Kosten und Latenz zu minimieren.
- Systematische Trefferquotenmessung: Um die Verlässlichkeit der Daten statistisch zu untermauern, könnten Referenzmessungen durchgeführt werden. Hierbei würde über einen definierten Zeitraum die tatsächliche Anzahl der Durchfahrten erfasst und mit den Systemdaten abgeglichen werden, um die Dunkelziffer exakt zu bestimmen.
- Erweiterung der regionalen Anreicherung: Der Bezirkserkennungs-Anreicherung könnte um weitere Länder (z. B. Deutschland) erweitert werden, um auch für Fahrzeuge aus diesen Ländern eine genauere Herkunftsanalyse zu ermöglichen.
- Prädiktive Analysen: Mit der Implementierung des Analytics-Service könnten Modelle bereitgestellt werden, welche basierend auf historischen Daten das Verkehrsaufkommen für einen gewissen Zeitraum vorhersagen.
- Active Directory Integration: Die Umsetzung des Auth-Service zur Anbindung an das Active Directory des Unternehmens würde die Sicherheit und Benutzerverwaltung standardisieren.
