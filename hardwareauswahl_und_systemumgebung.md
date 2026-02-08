# Hardware- und Technologieauswahl 

## Hardwareauswahl

Die Auswahl der Hardware ist entscheidend für die Zuverlässigkeit und Präzision der Kennzeichenerkennung und des Gesamtsystems. 
Diese beschränkt sich für diese Diplomarbeit auf zwei primäre Komponenten: 
1. Eine Kamera, welche Live-Daten von der Parkplatz Ein- und Ausfahrt erfasst und diese senden kann.
2. Ein Server oder ähnliches, auf welchen die Services der Diplomarbeit deployed werden können.

Das folgende Kapitel soll einen Einblick in den Entscheidungsprozess bieten, nach dem die benötigte Hardware ausgewählt wurde.
Hierfür werden zunächst die Grundanforderungen an das Gesamtsystem aus der Aufgabenstellung (!! Cross Reference) abgeleitet, aufbauend werden dann die spezifischen Anforderungen an die Hardwarekomponenten dargelegt.
Danach werden die einzelnen, im Auswahlprozess evaluierten Optionen gegenübergestellt und hinsichtlich ihrer Eignung analysiert. 


### Anforderungsanalyse an die Hardware

1. Grundanforderungen

Wie oben kurz erwähnt, gibt es einige Anforderungen, die für die Funktionsfähigkeit des Systems unausweichlich sind. 
Zunächst gilt es, die Lokalitäten vor Ort zu betrachten, also Lage und Aufbau des Bereiches, in dem der Fahrzeugverkehr erkannt werden soll.

(LUFTBILD)

Wie das Luftbild zeigt, verfügt der Parkplatz über eine kombinierte Ein- und Ausfahrt. 
Dies reduziert zwar den Installationsaufwand der Hardware, erhöht jedoch die Software-Komplexität, da die Bewegungsrichtung der Fahrzeuge softwareseitig erkannt werden muss.
Im Bezug auf die Frequenz, in welcher die Fahrzeuge erkannt werden müssen, wurde aufgrund der Breite der Einfahrt approximiert, dass mit einer Frequenz von maximal einem Fahrzeug alle 2-3 Sekunden auszugehen ist.
Das System muss folglich in der Lage sein, 20-30 Bilder pro Minute zu analysieren und die daraus gewonnenen Daten zu speichern. 

2. Anforderungen Kamera
Da die Kamera im Außenbereich eingesetzt wird, ist eine gewisse Witterungsbeständigkeit zwingend erforderlich. 
Aufgrund der notwendigen Positionierung der Kamera sollte diese mindestens die Schutzklasse IP66 (Ingress Protection) erfüllen, 
was einem Schutz vor starken Wasserstrahlen aus allen Richtungen entspricht. (https://security.baseus.com/en-eu/blogs/content/a-guide-to-ip65-ip66-and-ip67-ratings-for-outdoor-security-cameras)

Da das Kennzeichenerkennungssystem primär für die Erfassung von Kunden-Kennzeichen konzipiert ist, ist von einer effektiven Hauptbetriebszeit während der Öffnungszeiten der Zotter-Erlebniswelt ausgegangen worden.
Diese betragen: Mo–Fr: 9–18 Uhr, Sa: 9–18:30 Uhr
Aufgrund dessen lag im Entscheidungsprozess kein großes Augenmerk auf den Nachtsichtfähigkeiten des Kamerasystems.

3. Anforderungen Server
Die notwendige Rechenleistung des Servers hängt sehr stark von der Komplexität und Art der Prozesse ab, welche auf diesem ausgerollt und aktiv sind.
Deshalb wurde diese anfangs absichtlich nicht genau definiert.
Festgelegt wurde jedoch der Einsatz eines Linux-Betriebssystems, da dieses dem internen Unternehmensstandard entspricht, einen geringen OS-Overhead aufweist und eine breite Kompatibilität bietet.
Dies wurde allerdings als zweitrangig betrachtet, da das System durch die Verwendung von Containerisierung mit Docker ohnehin eine Plattformunabhängigkeit bietet. 
Auch wurde seitens Zotter vorausgesetzt, dass sämtliche Daten nicht nur aus Datenschutzgründen On-Premise, sondern für eine bessere Isolation des Systems lokal auf dem eingesetzten Server gespeichert werden sollen.


### Evaluierung der Hardware-Optionen

#### Kamera

Im Bezug auf die Kamera wurden von Anfang an nur IP-Kameras in Betracht gezogen, also Kameras, bei denen Video-Streams und Kommunikation per Ethernet stattfinden.
Dies hat zwei Hauptgründe:
1. Daten können in den meisten Fällen direkt per API-Requests ausgelesen werden, entweder über HTTP/REST-APIs oder im Fall von Video-Streams über RTSP (Real Time Streaming Protocol).
2. Viele IP-Kameras nutzen PoE (Power over Ethernet) für ihre Spannungsversorgung, was die Aufbaukomplexität weiter minimiert, da nur ein Kabel, welches Strom und Daten überträgt, verlegt werden muss.

Vor dem offiziellen Start der Diplomarbeit wurden hierzu schon einige Überlegungen angestellt und mögliche Produkt-Kandidaten vorgemerkt.
Im Zuge von Gesprächen mit Michael Zotter wurde darauf aufmerksam gemacht, dass bereits einige IP-Kameras des Herstellers Synology für frühere Testversuche angeschafft wurden.
Besonders das Modell BC500, von welchem einige Stück bereits im Besitz der Firma Zotter waren, erschien als besonders geeignet. (https://www.synology.com/en-eu/products/BC500)

(BILD BC500)

Mit einer Witterungsbeständigkeitsbewertung von IP67, da als Außenkamera konzipiert, ist diese gut für den Außeneinsatz geeignet.
Die maximale Videoauflösung von 2880×1620 Pixel bei maximal 30 FPS erschien auch für eine konsistente Kennzeichenerkennung ausreichend.
Auch verfügt die BC500 über eine automatische Nachtsichtfunktion mittels Infrarot-LEDs.
Zusätzlich schien die BC500 über eine robuste API für das Auslesen von Daten und das Streamen des Feeds zu verfügen.

Aufgrund der oben angesprochenen sofortigen Verfügbarkeit und des wegfallenden Mehraufwands für diese Kamera, verbunden mit den genannten Spezifikationen, fiel die Entscheidung nach Absprache mit unserer Kontaktperson auf das Synology-Modell.


#### Server

Die gewählte Microservice-Architektur im Zusammenspiel mit der angewandten Containerisierung erlaubt eine hohe Flexibilität für die Art der benötigten Hardware.
Desweiteren war aus einem früheren Praktikum bei Zotter Schokolade bekannt, dass die hausinternen Server-Kapazitäten für Container-Deployment besitzen. 

Als zweite Option wurde das Einrichten eines kleinen Servers auf der Hardware eines Office-Mini-PCs erwogen. 
Dieser wäre aus reiner Implementierungs- und Funktionssicht mit der ersten Option gleichwertig, mit dem Vorteil, dass dieser Ansatz eine gewisse Unabhängigkeit zum internen Netzwerk und zur zentralen Infrastruktur ermöglicht.

An diesem Punkt wurde im Kamera-Entscheidungsprozess auf die bestehenden Synology-Produkte aufmerksam gemacht. Mit dieser Neuausrichtung kam die Idee auf, das System auf einem eigenen NAS-System (Network-attached Storage), ebenfalls von Synology zu betreiben.

Nicht nur wurden NAS-Systeme von Synology bereits im Unternehmen eingesetzt, diese sind in den meisten Bereichen gleichwertig mit den vorherigen beiden diskutierten Ansätzen und bieten in manchen Bereichen klare Vorteile:
1. Die Vorteile der zweiten Option bleiben bestehen, es gibt weiterhin eine gesteigerte Unabhängigkeit zur Unternehmensinfrastruktur und damit hergehend mehr Entwicklungsfreiheit.
2. Da es sich um ein NAS-System handelt, also ein Gerät, welches primär für die Speicherung von Daten konzipiert ist, stellt der benötigte Speicherplatz kein Problem mehr dar, da einfach neue Disks verbaut werden können (standardmäßig 2× 2TB Disks, RAID 1).
3. Diese NAS-Systeme besitzen bereits recht leistungsstarke Komponenten, welche im Bezug auf Rechenleistung meist gleichwertig zu einem durchschnittlichen Mini-PC sind. 
Auch sind die meisten NAS-Geräte mit einem vollwertigen Betriebssystem ausgestattet, welches Methoden bereitstellt, um Container mittels Docker reibungslos laufen zu lassen.

Der größte Vorteil kommt aber mit der Kombination mit den oben beschriebenen Kameras des gleichnamigen Herstellers.
Wie die Kameralinie von Synology vermuten lässt, bietet der Hersteller eigene Produkte gezielt für Überwachungsaufgaben an.
Diese laufen unter einem Gesamtsystem mit der Bezeichnung "Surveillance Station" und sind als Paket auf den hauseigenen NAS-Systemen verfügbar. (https://www.synology.com/en-global/surveillance)

Innerhalb des Surveillance Station-Ökosystems bietet Synology mit der DVA-Serie (Deep Video Analytics) spezialisierte NVR-Geräte (Network Video Recorder) an, welche über GPU-beschleunigte KI-Funktionen verfügen.
Im besonderen das Modell DVA1622 (zur Zeit des Projekts das einzige verfügbare Modell der DVA-Serie) bietet für diese Diplomarbeit in Kombination mit der Kamera BC500 viele Vorteile:

Zunächst bietet die Surveillance Station API direkten Zugriff auf Live-Streams, Snapshots und Ereignis-Metadaten, was die Integration in eigene Microservices im Vergleich zum direkten auslesen aus Kameras erheblich vereinfacht.
Die DVA-Serie unterstützt nativ viele Features aus dem Security- und Surveillance-Bereich. 
So können etwa mittels Erkennungszonen bereits auf Surveillance Station-Ebene relevante Bildbereiche wie der Einfahrtsbereich definiert werden.
Dies ist besonders für das Erstellen von "Triggers" relevant, also das Anlegen eines Bereiches, in dem im Falle einer Fahrzeugdurchfahrt die Kennzeichenerkennung stattfinden soll.
Desweiteren können alle Kamera-Einstellungen, Aufzeichnungen und Analysen über eine einheitliche Oberfläche auf dem NAS-Gerät verwaltet werden.

Die Kombination aus relevanten Features, umfassender API und nativer Kamera-Unterstützung machte das Synology DVA1622-NAS zur optimalen Wahl für die Realisierung des Kennzeichenerkennungssystems.


## Technik-Stack und Technologieauswahl der Kennzeichenerkennung

### Technologieauswahl Kennzeichenerkennung

Für die eigentliche Kennzeichenerkennung stand die Entscheidung zwischen der Entwicklung einer eigenen Lösung auf Basis von Open-Source-OCR-Bibliotheken (wie Tesseract OCR oder EasyOCR) und der Verwendung einer kommerziellen Lösung im Raum.

Bei der Evaluation von Tesseract und EasyOCR zeigte sich, dass diese generischen OCR-Engines zwar für Texterkennungsaufgaben gut geeignet sind, bei der spezifischen Herausforderung der Kennzeichenerkennung jedoch erhebliche Nachteile aufweisen. 
Kennzeichen stellen besondere Anforderungen an ein Erkennungssystem, wie im Kapitel ALPR (!! Cross Reverence) bereits erwähnt: 
Sie müssen aus verschiedenen Winkeln, bei unterschiedlichen Lichtverhältnissen, mit Verschmutzungen und in Bewegung zuverlässig erkannt werden. 
Zudem variieren Kennzeichenformate international stark in Schriftart, Layout und Zeichenabständen.

Die Entwicklung eines eigenen trainierten Modells auf Basis dieser Bibliotheken hätte einen erheblichen Aufwand für das Sammeln und Annotieren von Trainingsdaten bedeutet, wobei die resultierende Genauigkeit dennoch fraglich geblieben wäre. 
In diese Richtung wurden im Zuge der Diplomarbeit-Entwicklung Prototypen erstellt, diese blieben aber in ihrer Qualität unzureichend oder waren in ihrem Realisierungssaufwand unrealistisch. 
Aus diesem Grund fiel die Entscheidung auf Plate Recognizer, eine spezialisierte kommerzielle Lösung für Kennzeichenerkennung.

Plate Recognizer bietet hochoptimierte Machine-Learning-Modelle, die bereits auf Millionen von Kennzeichenbildern aus über 90 Ländern trainiert wurden. 
Dies gewährleistet eine deutlich höhere Erkennungsrate auch unter erschwerten Bedingungen. 
Zusätzlich zur reinen Texterkennung bietet die Lösung erweiterte Funktionen wie Fahrzeugtyp- und Farberkennung, die für zukünftige Erweiterungen des Systems nützlich sein können.

Wie zuvor erwähnt, ist ein weiterer entscheidender Vorteil die Verfügbarkeit als Docker-Container (Plate Recognizer SDK), der vollständig lokal auf dem DVA1622 NAS betrieben werden kann. 
Im Gegensatz zu Cloud-basierten API-Lösungen bleiben damit alle Bilddaten im lokalen Netzwerk, was sowohl Datenschutzanforderungen erfüllt als auch Latenzzeiten minimiert. 


### Argumentation der Software-Technologien Entscheidungen

Als Web-Framework wurde FastAPI auf Python gewählt, welches moderne asynchrone Request-Verarbeitung unterstützt und automatische API-Dokumentation via OpenAPI/Swagger generiert. 
Im Vergleich zu Flask, dem vermutlich bekanntesten Python-Framework, bietet FastAPI native Type-Hints-Unterstützung und automatische Validierung von Request-/Response-Daten durch Pydantic. 
Gegenüber dem schwergewichtigeren Django bringt FastAPI deutlich weniger Overhead mit und ist damit besser für kleine Microservices geeignet, bei denen schlanke, spezialisierte Services bevorzugt werden.

Für die Datenhaltung wurde PostgreSQL als relationale Datenbank gewählt. 
Während NoSQL-Datenbanken wie MongoDB für hochskalierbare, dokumentenbasierte Anwendungen Vorteile bieten, sprechen im vorliegenden Fall die strukturierten Datenbeziehungen (Erkennungen, Benutzer etc.) klar für eine relationale Datenbank. 

Um Datenbank-Schema Änderungen versioniert und reproduzierbar zu gestalten, wurde Alembic als Migrations-Framework gewählt. 
Im Gegensatz zu manuellen SQL-Skripten ermöglicht dies rückverfolgbare Datenbankänderungen, die automatisiert über alle Umgebungen ausgerollt werden können.

Das Gesamtsystem basiert auf Docker und einer Microservice-Architektur. 
Wie zuvor detailiert erklärt läuft jeder Dienst (Data Collection, Notification, Grafana) in seinem eigenen Container mit klar definierten Schnittstellen. 
Dies verhindert wie in den Thoretischen Grundlagen erklärt nicht nur Abhängigkeitskonflikte zwischen verschiedenen Services, sondern ermöglicht auch die unabhängige Skalierung einzelner Komponenten. 
Die Containerisierung gewährleistet zudem Plattformunabhängigkeit, da das System problemlos von der Synology-Plattform auf andere migriert werden kann, ohne dass Anpassungen am Code notwendig sind. 
