# Hardware- und Technologieauswahl 

## Hardwareauswahl

Die Auswahl der Hardware ist entscheidend für die Zuverlässigkeit und Präzision der Kennzeichenerkennung und des Gesamtsystems. 
Diese beschränkt sich für diese Diplomarbeit auf zwei primäre Komponenten: 
1. Eine Kamera welche Live-Daten von der Parkplatz Ein- und Ausfahrt erfasst und diese senden kann.
2. Ein Server oder ähnliches auf welchen die Services der Diplomarbeit deployed werden können.

Das Folgende Kapitel soll einen Einblick in den Entscheidungsprozess bieten, dach dem die benötigte Hardware ausgewählt wurde.
Hierfür werden zunächst die Gundanforderungen an das Gesamtsystem aus der Aufgabenstellung (!! Cross Reference) abgeleitet, aufbauend werden dann die spezifischen Anforderungen an die Hardwarekomponenten dargelegt.
Dannach werden die einzelnen, im Auswahlprozess evaluierten Optionen gegenübergestellt und hinsichtlich ihrer Eignung analysiert. 


### Anforderungsanalyse an die Hardware

1. Grundanforderungen
Wie oben kurz erwähnt gibt es einige Anforderungen, die für die Funktionsfähigkeit des Systems unausweichlich sind. 
Zunächst gilt es die Lokalitäten vor Ort zu betrachen, also Lage und Aufbau des zu Bereiches, in dem der Fahrzeugverkehr erkannt werden soll.

(LUFTBILD)

Wie das Luftbild zeigt, verfügt der Parkplatz über eine kombinierte Ein- und Ausfahrt. 
Dies reduziert zwar den Installationsaufwand der Hardware, erhöht jedoch die Software-Komplexität, da die Bewegungsrichtung der Fahrzeuge softwareseiting erkannt werden muss.
Im Bezug auf die Frequenz, in welcher die Fahrzeuge erkannt werden müssen, wurde aufgrund der Breite der Einfahrt approximiert, dass mit einer Frequenz von maximal einem Fahrzeug alle 2-3 Sekunden auszugehen ist.
Das System muss folglich in der Lage sein, 20-30 Bilder pro Minute zu analysieren und die daraus gewonnenen Daten zu speichern. 

2. Anforderungen Kamera

Da die Kamera im Außenbereich eingesetzt wird, ist eine gewisse Witterungsbeständigkeit zwingend erforderlich. 
Aufgrund der notwendigen Positionierung der Kamera, sollten diese mindestens die Schutzklasse IP66 (Ingress Protection) erfüllen, 
was einem Schutz vor starken Wasserstrahlen aus allen Richtungen entspricht. (https://security.baseus.com/en-eu/blogs/content/a-guide-to-ip65-ip66-and-ip67-ratings-for-outdoor-security-cameras)

Da das Kennzeicehnerkennungssystem primär für die Erfassung von Kunden-Kennzeichen konzipiert ist, ist von einer effektiven Hauptbetriebszeit während der Öffnungszeiten der Zotter-Erlebniswelt ausgegangen worden.
Diese betragen: Mo–Fr: 9–18 Uhr, Sa: 9–18:30 Uhr
Aufgrund dessen lag im Entscheidungsprozess kein großen Augenmerk auf den Nachtsichtfähigkeiten des Kamerasystems.

3. Anforderungen Server

Da die notwendige Rechenleistung des Servers sehr stark an die Komplexität und Art der Prozesse, welche auf diesem Laufen gebunden ist, wurde diese Anfangs absichtlich nicht genau definiert.
Festgelegt wurde jedoch der Einsatz eines Linux-Betriebssystems, da dieses dem internen Unternehmensstandard entspricht, einem geringen OS-Overhead aufweist und eine breite Kompatibilität bietet.
Dies wurde allerdings als zweitrangig betrachtet, da das System durch die Verwendung von Containerisierung mit Docker ohnehin eine Plattformunabhängigkeit bietet. 
Auch wurde Seitens Zotter vorausgesetzt, dass sämtliche Daten nicht nur aus Datenschutzgründen On-Premise, sondern für eine bessere Isolation des Systems lokal auf dem eingesetzten Server gespeichert werden sollen.


### Evaluierung der Hardware-Optionen

Kamera: Synology-Integration vs. Standard-IP-Cams
Das System nutzt die Synology Surveillance Station als zentralen Hub.
* Vorteile: Zentrale Verwaltung, lokaler Speicher der Aufnahmen und eine robuste API zur Extraktion von Snapshots.
* Kriterien: Die Kameras müssen auf der Synology-Kompatibilitätsliste stehen. Eine hohe Auflösung (min. 1080p) ist wichtig, wobei die Optik für den Fokusbereich der Kennzeichen optimiert sein sollte (Teleobjektiv bei größeren Distanzen).


Server/Recheneinheit
Die Microservice-Architektur ermöglicht verschiedene Hosting-Szenarien:
* Mini-PC / NUC: Ideal für das Deployment vor Ort. Bietet genug CPU-Leistung für den rechenintensiven plate-recognizer Container (x86_64 Architektur empfohlen).
* Synology NAS (Docker-fähig): Bei leistungsstärkeren NAS-Modellen (z.B. Plus-Serie) kann das gesamte System direkt auf dem Speichergerät betrieben werden, was die Hardwarekomplexität reduziert.
* Deployment: Die Orchestrierung erfolgt vollständig über Docker Compose, was einen schnellen Wechsel zwischen Test- und Produktionsumgebungen ermöglicht.


## Software-Technologieauswahl

### Argumentation für Software-Technologien

Das System basiert konsequent auf Docker und Microservices.
* Isolierung: Jeder Dienst (Analytics, Auth, Data Collection, Notification) läuft in seinem eigenen Container, was Abhängigkeitskonflikte verhindert.
* Skalierbarkeit: Einzelne Komponenten (z.B. der Data-Collection-Service für mehrere Standorte) können unabhängig voneinander skaliert werden.
* Wartbarkeit: Durch die Containerisierung ist das System plattformunabhängig und kann einfach gesichert oder migriert werden (manual_backup.sh).


### Technologieauswahl für die Kennzeichenerkennung

Warum Plate Recognizer?
Anstatt eine eigene Lösung auf Basis von Open-Source-Bibliotheken (wie Tesseract oder EasyOCR) zu entwickeln, wurde Plate Recognizer gewählt:
* Genauigkeit: Hochoptimierte Machine-Learning-Modelle, die auch bei schlechten Winkeln, Verschmutzung oder schwieriger Beleuchtung extrem hohe Erkennungsraten erzielen.
* Internationale Unterstützung: Unterstützung für Kennzeichen aus über 90 Ländern, inklusive Fahrzeugtyp- und Farberkennung.
* Lokaler Container: Durch den Einsatz des platerecognizer/alpr Docker-Images bleiben die Bilddaten im lokalen Netzwerk (Datenschutz), und die Latenzzeiten der Cloud-Kommunikation entfallen.
