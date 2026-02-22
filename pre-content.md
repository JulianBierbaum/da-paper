# Pre-Content

## Kurzbeschreibung

Diese Diplomarbeit befasst sich mit der Konzeption und Implementierung eines automatisierten Systems zur Erfassung und Analyse von Fahrzeugkennzeichen für die Zotter Schokolade GmbH.
Ziel war die Entwicklung einer Softwarelösung, um Videostreams von Überwachungskameras zu verarbeiten, Kennzeichen und Fahrzeugdaten aus den Bildern zu extrahieren und diese auszuwerten, um einen fundierten Überblick über Besucherstatistiken zu bieten.
Dabei ermöglicht das System beispielsweise eine Herkunftsanalyse auf Länderebene, welche für österreichische und slowenische Fahrzeuge bis auf die Bezirksebene verfeinert wird.
Die implementierten Kernkomponenten umfassen Backend-Services zur Datenerfassung und Benachrichtigung per E-Mail (realisiert mit Python und FastAPI) sowie die Integration eines Grafana-Dashboards zur Visualisierung der gesammelten und analysierten Daten.
Ein besonderes Augenmerk galt der Gewährleistung von Datenschutzkonformität (DSGVO) und hoher Ausfallsicherheit durch ein Backup- sowie Disaster-Recovery-Konzept für die PostgreSQL-Datenbank.
Um die Wartbarkeit und Softwarequalität sicherzustellen, wurde der Entwicklungsprozess durch CI/CD-Pipelines automatisiert.
Das realisierte System basiert auf einer hybriden Microservice-Architektur unter Verwendung von Docker-Containern, welche durch ihre starke Kapselung im Live-System einfach auszurollen sind.


## Abstract

This diploma thesis focuses on the design and implementation of an automated system for capturing and analyzing vehicle license plates for the parking lot of Zotter Schokolade.
The objective was to develop a software solution capable of processing video streams from surveillance cameras, extracting license plates and additional vehicle data from images, and analyzing the collected data to provide an overview of visitor statistics.
For example, the system enables origin analysis on a country level, which is further refined to the district level for vehicles from Austria and Slovenia.
The implemented core components include backend services for data acquisition and email notifications (implemented using Python and FastAPI), as well as the integration of a Grafana dashboard for the visualization of the collected and analyzed data.
Particular emphasis was placed on ensuring compliance with data protection regulations (GDPR) and achieving high system availability through a backup and disaster recovery concept for the PostgreSQL database.
To ensure maintainability and software quality, the development process was automated using CI/CD pipelines.
The resulting system is based on a hybrid microservice architecture using Docker containers, which, due to their strong isolation, can be easily deployed in a production environment.


## Vorwort

Eine Diplomarbeit in Zusammenarbeit mit Zotter war von Anfang an mein Ziel. 
Nicht nur, weil mich persönlich vieles mit diesem Unternehmen verbindet, sondern auch, weil ich die Dynamik des Unternehmens sehr einzigartig finde.
Es entsteht ständig etwas Neues oder etwas Bestehendes wird verändert, gerade das macht das Arbeiten im IT-Bereich bei Zotter so spannend. 
Die Wahl des Themas ergab sich aus einer Brainstorming-Session: Wie lässt sich das Besucheraufkommen erfassen und analysieren? Kameras bei den Eingangstüren mit Zählfunktion? Freiwillige Umfragen?
Nach einiger Zeit sind wir auf die Idee gekommen, die Kennzeichen der Besucherfahrzeuge zu analysieren. Und an dieser Idee hielten wir fest.

Ich möchte mich bei allen bedanken, die mich im Laufe dieser Diplomarbeit unterstützt haben.
Ein besonderer Dank gilt Michael Zotter, ohne dessen Hilfe und Vertrauen dieses Projekt nie zustande gekommen wäre. 
Er hat mir nicht nur die Möglichkeit gegeben, diese Arbeit umzusetzen, sondern mir auch den nötigen Freiraum und Zugang zur Infrastruktur gewährt.

Ebenso danke ich Herrn DI (FH) Ing. Gerald Ebner, der mich über den gesamten Verlauf dieser Arbeit fachlich begleitet und unterstützt hat.
Meinen Klassenkameraden danke ich für die Motivation und entschuldige mich gleichermaßen für mein viel zu häufiges Nachfragen und Vergleichen mit anderen Arbeiten, welches zu großen Teilen zu meiner Motivation beigetragen hat.
Abschließend möchte ich meiner Familie danken, die mich während meiner gesamten HTL-Laufbahn, eigentlich muss man sagen mein ganzes Leben lang, bedingungslos unterstützt hat.

Danke!
