# Theoretische Grundlagen

## Containerisierung (Docker)

Die Containerisierung ist eine Methode, bei der Anwendungen und deren Abhängigkeiten in einer leichtgewichtigen, isolierten Einheit, den Container verpackt werden.

Docker
Docker ist eine offene Plattform, die 2013 veröffentlicht wurde und die Containerisierung von Anwendungen standardisiert. 
Es stellt die notwendigen Tools bereit, um Container einfach zu erstellen und mit ihnen arbeiten zu können, und abstrahiert dabei die Komplexität der zugrundeliegenden Linux-Kernel-Features (Namespaces, cgroups).
Die Docker-Plattform besteht aus der Docker Engine (Daemon, REST API und CLI), Docker Images und Docker Containern.

Architektur und Funktionsweise
Docker basiert auf einer Client-Server-Architektur (https://docs.docker.com/get-started/docker-overview/).
Der Docker-Daemon verwaltet Container, Images, Netzwerke und Volumes, während der Docker-Client (CLI) die Schnittstelle für Benutzerinteraktionen bereitstellt. 
Images, also Abbilder des Anwendung und ihrer Umgebung werden als unveränderliche Vorlagen aus sogenannten Dockerfiles erstellt und in Layern organisiert, wobei jede Instruktion im Dockerfile einen neuen Layer erzeugt. 
Dieses Layer-System ermöglicht effizientes Caching: Wenn ein Image neu gebaut werden muss, müssen nur die Layer neu erstellt werden, an denen tatsächlich Änderungen vorgenommen wurden.

Container werden aus diesen Images instanziiert und stellen isolierte Prozesse und deren Umgebung dar. 
Im Gegensatz zu virtuellen Maschinen, die jeweils ein vollständiges Gastbetriebssystem benötigen, teilen sich Container den Host-Kernel, was sie deutlich ressourcenschonender macht.

Vorteile von Containerisierung und Docker
Der wohl größte Punkt der für Containerisierung spricht ist die Eliminierung des klassischen "Works on my machine"-Problems. 
Der Container läuft in der Entwicklung identisch zur Produktion, da das gesamte Betriebssystem, einschließlich Konfigurationen, Bibliotheken und Abhängigkeiten, im Image verpackt sind. 
Dies reduziert Deployment-Fehler erheblich und erleichtert das Debugging, da Entwickler exakt dieselbe Umgebung lokal reproduzieren können.

Wie zuvor erwähnt läuft jeder Service (Grafana, PostgreSQL, Python-Services etc.) in einer vollständig isolierten Umgebung. 
Abhängigkeiten oder Python-Pakete (etwa definiert in einem uv.lock-File) eines Services können nicht mit denen eines anderen kollidieren. 
Die Dateisystem-Isolation stellt sicher, dass jeder Container sein eigenes Root-Dateisystem hat, wodurch versehentliche Überschreibungen oder unbeabsichtigte Datenzugriffe verhindert werden. 
Auch sind Container auf Netzwerk-Ebene isoliert, heißt Kommunikation zwischen Container und mit der "Außenwelt" kann nur über definierte Schnittstellen stattfinden.

Ein weiterer Vorteil ist die Versionskontrolle und Rollback-Fähigkeit, welche Docker-Images bieten. 
Diese können mit Tags versehen werden, wodurch spezifische Versionen einer Anwendung eindeutig identifizierbar sind. 
Bei Problemen, etwa nach einem Update kann somit schnell zu einer vorherigen, stabilen Version zurückgewechselt werden.

Zudem bieten Container eine hohe Skalierbarkeit. Sie können horizontal skaliert werden, indem mehrere Instanzen desselben Services gestartet werden. 
In Verbindung mit Orchestrierungstools wie Kubernetes können Services dynamisch basierend auf der aktuellen Last skaliert werden.

Docker Compose
Docker Compose ist ein Tool zur Definition und Verwaltung von Multi-Container-Anwendungen. 
Compose ermöglicht die Orchestrierung mehrerer Services durch eine deklarative YAML-Konfigurationsdatei.
In dieser Datei werden alle Services, Abhängigkeiten, Netzwerke, Volumes (persistenter Speicher) und Umgebungsvariablen definiert. 
Docker Compose startet Services in der vordefinierten Reihenfolge und ermöglicht automatische Kommunikation zwischen ihnen. 
Besonders wertvoll ist Docker Compose für Entwicklungsumgebungen, da es die gesamte Infrastruktur als Code definiert. 
Statt mehrere Services manuell zu starten, orchestriert eine einzige Datei das komplette System, was auch unterschiedliche Umgebungen wie etwa Entwicklung und Live (Produktion) durch separate Compose-Dateien ermöglicht.

Docker Hub
Docker Hub ist die zentrale, cloudbasierte Registry für Docker-Images und fungiert als öffentliches Repository, ähnlich wie GitHub für Code. 
Es enthält eine Vielzahl an vorgefertigten Images, darunter offizielle Images für gängige Software und Technologien wie PostgreSQL, Redis oder Python, welche von den jeweiligen Maintainern verifiziert werden.
Beim starten einen Stacks onder Containers lädt Docker automatisch benötigte Images von Docker Hub herunter, falls sie nicht lokal vorhanden sind. 
In dieser Diplomarbeit werden beispielsweise offizielle Images für PostgreSQL und Grafana verwendet, während selbsterstellte Images für die Python-Services verwendet werden, welche in einem eigenen Docker-Registry gespeichert sind.

Durch die Containerisierung kann das gesamte System der Diplomarbeit mit einem einzigen Befehl auf jedem System orchestriert gestartet, gestoppt oder neu gebaut werden, unabhängig vom Host-Betriebssystem (Linux, macOS, Windows). 
Die Infrastruktur wird als Code (Infrastructure as Code) definiert, was Versionierung und Nachvollziehbarkeit von Umgebungsänderungen ermöglicht.


Mögliche alternativen aber nicht nicht argumentieren

!!!!! es bietet sich für die diplomarbeit an, weil


## Microservice Architektur

Die Microservice-Architektur ist ein Designansatz, bei dem eine Anwendung als Sammlung kleiner, lose gekoppelter Dienste aufgebaut wird.

Grundkonzept und Definition
Während zum Beispiel eine monolithische Architektur alle Funktionen einer Anwendung in einem einzigen, zusammenhängenden Prozess vereint, werden bei Microservices einzelne Funktionsbereiche in eigenständige Services ausgelagert. 
Jeder dieser Services läuft in einem eigenen Prozess, besitzt eine klar definierte Schnittstelle und kommuniziert über leichtgewichtige Protokolle wie REST/HTTP oder Message Queues wie RabbitMQ mit anderen Services.

Der Begriff "Microservice" bezieht sich dabei weniger auf die absolute Größe des Codes, sondern vielmehr auf die fokussierte Verantwortung: Ein Service sollte genau eine Aufgabe erfüllen und diese gut erfüllen (Single Responsibility Principle).

Jeder Microservice ist eine eigenständige Einheit mit eigener Datenhaltung, Geschäftslogik und oft auch einem eigenen Technologie-Stack. 
Microservices kommunizieren über klar definierte APIs, typischerweise mittels HTTP/REST oder Message Queues. In diesem Projekt erfolgt die Kommunikation primär über RESTful APIs, wobei jeder Service seine Endpunkte bereitstellt. 

Ein fundamentaler Vorteil von Microservices ist die Möglichkeit, Services unabhängig voneinander zu deployen. 
Wenn eine Änderung an einem Service vorgenommen wird, kann dieser Service aktualisiert werden, ohne dass andere Services neu gestartet oder verändert werden müssen. 
Dieses Prinzip profitiert stark von der Containerisierung, welche im letzten Kapitel erklärt wurde.

Vorteile der Microservice-Architektur

Technologiefreiheit

Jeder Service kann in der für seine Anforderungen am besten geeigneten Programmiersprache und mit dem optimalen Framework entwickelt werden. 
Während die Python-Services in diesem Projekt etwa FastAPI für die API-Entwicklung nutzen, könnte ein zukünftiger Service für in Go geschrieben werden, oder ein Frontend-Service könnte Next.js verwenden.

Fehlertoleranz und Resilience
Durch die Isolation der Services wird die Fehlerausbreitung begrenzt. Wenn ein Service abstürzt oder nicht erreichbar ist, beeinträchtigt dies nicht die Kernfunktion der Kennzeichenerfassung. 
Das System kann mit degradierter Funktionalität weiterlaufen, anstatt vollständig auszufallen.

Organisatorische Agilität
Microservices ermöglichen es, dass Entwickler unabhängig voneinander arbeiten können. Jeder kann für einen oder mehrere Services verantwortlich sein und autonom Entscheidungen über Technologien, Entwicklungsprozesse und Deployment-Strategien treffen.

Wartbarkeit und Verständlichkeit
Kleinere, fokussierte Codebasen sind einfacher zu verstehen und zu warten als ein großer Monolith. 
Neue Entwickler können sich schnell in einen einzelnen Service einarbeiten, ohne das gesamte System verstehen zu müssen. 
Auch Refactorings oder große Änderungen sind risikoärmer, da Änderungen auf einen Service beschränkt bleiben.

Die Kombination von Microservices mit Docker-Containerisierung verstärkt diese Vorteile noch: Jeder Service läuft in seiner eigenen isolierten Umgebung, Dependencies sind klar definiert, 
und die gesamte Infrastruktur kann als Code versioniert und reproduzierbar deployed werden (!!!!Cross Reference Docker-Compose Kapitel).

Die Implementierung einer Microservice Architekur bring auch einige Herausforderungen und Trade-offs mit sich.
Diese beziehen sich primär die erhöhte Komplexität, welche die Verteilung der Funktionalität unausweichlich mit sich bringt und ein gewisser Overhead, der entsteht, da jeder Service in einer separaten Instanz (Container) gestartet werden muss.

Im Fazit ist die Microservice-Architektur ein mächtiger Ansatz für komplexe Systeme, der Flexibilität, Fehlertoleranz und Skalierbarkeit bietet. 

Mögliche alternativen aber nicht nicht argumentieren

!!!!! es bietet sich für die diplomarbeit an, weil

## ALPR (Automatic License Plate Recognition)

ALPR (Automatic License Plate Recognition) bezeichnet die automatisierte Erfassung und Auswertung von Fahrzeugkennzeichen aus Bilddaten mittels Computer Vision und Deep Learning. (https://platerecognizer.com/what-is-alpr/) 
ALPR-Systeme arbeiten kontinuierlich und transformieren visuelle Informationen wie Kamera-Snapshots in strukturierte, maschinell verarbeitbare Daten und ermöglichen damit die automatische Identifikation von Fahrzeugen.

Grundfunktionsweise
Der Erkennungsprozess und die Verarbeitung der Daten erfolgt typischerweise in einem mehrstufigen Prozess: (https://senstar.com/de/senstarpedia/wie-alpr-funktioniert/)

1. Detection (Lokalisierung): 
Das System identifiziert zunächst relevante Bildbereiche. 
Moderne Ansätze nutzen hierfür Object Detection-Algorithmen, um Fahrzeuge im Gesamtbild zu lokalisieren und anschließend den spezifischen Kennzeichenbereich zu extrahieren. 
Diese Vorselektion reduziert die zu verarbeitende Datenmenge erheblich und fokussiert nachfolgende Verarbeitungsschritte nur auf relevante Regionen.

2. Transformation (Normalisierung): 
Kennzeichen werden selten in perfekter Frontalansicht und bei besten Lichtverhältnissen erfasst. 
Für eine zuverlässige Erkennung müssen Parameter wie Perspektive, Kontrast, Helligkeit oder andere Bildattribute angepasst werden, um die Sichtbarkeit des Kennzeichens zu verbessern.

3. OCR (Optical Character Recognition): 
Die eigentliche Zeichenerkennung wandelt Bildinformationen in Text um. 
Diese nutzen Deep Learning-basierte Ansätze, die einzelne Zeichen nicht nur isoliert betrachten, sondern auch den Kontext benachbarter Zeichen berücksichtigen. 
Jedes erkannte Zeichen wird mit einem Konfidenzwert versehen, der die Erkennungssicherheit quantifiziert.

4. Post-Processing (Validierung): 
Die Rohergebnisse werden gegen bekannte Muster und Regeln validiert wie etwa länderspezifische Kennzeichensyntaxen (etwa die österreichische Struktur aus Bezirk und Erkennungsnummer) dient als Prüfung der Plausibilität der erkannten Nummerntafel. 
Auch werden typische OCR-Verwechslungen wie "0" versus "O" oder "1" versus "I" kontextbasiert korrigiert.

Technologie und Anbieter
In diesem System wird der Dienst Plate Recognizer eingesetzt, der moderne Deep Learning-Ansätze nutzt und über klassische Texterkennung hinausgeht.

MMC-Erkennung (Make, Model, Color)
Neben der im Vergleich sehr zuverlässigen Kennzeichenerkennung identifiziert Plate Recognizer zusätzliche Fahrzeugattribute (https://platerecognizer.com/vehicle-make-model-recognition-with-color/) ein Ansatz, der MMC-Erkennung genannt wird: 
Make (Marke): Identifikation des Fahrzeugherstellers basierend auf charakteristischen Designmerkmalen.
Model (Modell): Feinere Unterscheidung innerhalb einer Marke, etwa zwischen verschiedenen Baureihen oder Generationen.
Color (Farbe): Bestimmung der Primärfarbe unter Kompensation von Lichtverhältnissen und Unterscheidung zwischen verschiedenen Lackierungstypen.

On-Premise SDK
Plate Recognizer bietet sowohl Cloud-basierte APIs als auch ein On-Premise SDK an. 
Die On-Premise-Variante ermöglicht vollständige lokale Ausführung ohne externe Netzwerkabhängigkeit (https://guides.platerecognizer.com/docs/snapshot/getting-started), eine Anforderung, welche Zotter Schokoladen sehr wichtig war.

Vorteile der lokalen Ausführung:
Der größte Vorteil in der Offline-Verarbeitung der Bilddaten liegt darin, dass die potenziell personenbezogene Informationen niemals das lokale Netzwerk des Unternehmens verlassen. 
Dies ist besonders relevant für europäische Datenschutzanforderungen wie die DSGVO (Datenschutzgrundverordnung), die strenge Regeln für die Verarbeitung solcher Daten vorsehen.
Außerdem funktioniert das System unabhängig von einer Internetverbindung, was Zuverlässigkeit auch mit eingeschränkter Konnektivität garantiert.

Mögliche alternativen aber nicht nicht argumentieren

!!!!! es bietet sich für die diplomarbeit an, weil