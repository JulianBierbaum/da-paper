# Pre-Content

## Kurzbeschreibung

Diese Diplomarbeit befasst sich mit der Konzeption und Implementierung eines automatisierten Systems zur Erfassung und Analyse von Fahrzeugkennzeichen für die Zotter Schokoladen GmbH.
Ziel war die Entwicklung einer Softwarelösung, um Videostreams von Überwachungskameras zu verarbeiten, Kennzeichen und Fahrzeugdaten aus den Bildern zu extrahieren und diese auszuwerten, um einen fundierten Überblick über Besucherstatistiken zu bieten.
Dabei ermöglicht das System beispielsweise eine Herkunftsanalyse auf Länderebene, welche für österreichische und slowenische Fahrzeuge bis auf die Bezirksebene verfeinert wird.
Die implementierten Kernkomponenten umfassen Backend-Services zur Datenerfassung und Benachrichtigung per E-Mail (realisiert mit Python und FastAPI) sowie der Integration eines Grafana-Dashboards zur Visualisierung der gesammelten und analysierten Daten.
Ein besonderes Augenmerk galt der Gewährleistung von Datenschutzkonformität (DSGVO) und hoher Ausfallsicherheit durch ein Backup- sowie Disaster-Recovery-Konzept für die PostgreSQL-Datenbank.
Um die Wartbarkeit und Softwarequalität sicherzustellen, wurde der Entwicklungsprozess durch CI/CD-Pipelines automatisiert.
Das realisierte System basiert auf einer hybriden Microservice-Architektur unter Verwendung von Docker-Containern, welche durch ihre starke Kapselung im Live-System einfach auszurollen sind.


## Abstract

This diploma thesis focuses on the design and implementation of an automated system for capturing and analyzing vehicle license plates for the parking lot of Zotter Schokoladen.
The objective was to develop a software solution capable of processing video streams from surveillance cameras, extracting license plates and additional vehicle data from images, and analyzing the collected data to provide an overview of visitor statistics.
For example, the system enables origin analysis on a country level, which is further refined to the district level for vehicles from Austria and Slovenia.
The implemented core components include backend services for data acquisition and email notifications (implemented using Python and FastAPI), as well as the integration of a Grafana dashboard for the visualization of the collected and analyzed data.
Particular emphasis was placed on ensuring compliance with data protection regulations (GDPR) and achieving high system availability through a backup and disaster recovery concept for the PostgreSQL database.
To ensure maintainability and software quality, the development process was automated using CI/CD pipelines.
The resulting system is based on a hybrid microservice architecture using Docker containers, which, due to their strong isolation, can be easily deployed in a production environment.


## Vorwort

TO-DO