# Einleitung

# Motivation

Die Erlebniswelt von Zotter Schokolade zählt mit ihren über 300.000 jährlichen Besuchern (Stand 2025) zu den Top-3 der steirischen Sehenswürdigkeiten mit Bezahl-Eintritt. (https://www.steiermark.com/de/Magazin/Die-meistbesuchten-Ausflugsziele-der-Steiermark_mad_45932860).
Diese enormen Besucherströme stellen eine nicht unbedeutende organisatorische Herausforderung für Mitarbeiter und Management dar.
Trotz der hohen Frequenz an Besuchern gleichte der Parkplatz aus datentechnischer Sicht einer "Black Box", da keine automatisierte Erfassung oder Auswertung von Fahrzeugbewegungen existierte. 
Informationen über die tatsächliche Auslastung, Stoßzeiten oder die Verweildauer basierten auf subjektiven Beobachtungen statt auf Daten.
Dies erschwerte sowohl die operative Ressourcenplanung als auch strategische Entscheidungen erheblich.
Diese Diplomarbeit zielt darauf ab, diese Lücke zu schließen, indem ein modernes Kennzeichenerkennungssystem (ALPR) eingeführt wird, um Kennzeichen und Fahrzeugdaten zu erfassen, diese unter anderem auf Herkunft zu analysieren und anonymisiert zu speichern.
Auf diese Daten aufbauend, können Analysen, grafische Dashboards mit den wichtigsten Informationen und langfristige Vorhersagen getroffen werden.
Ziel ist es, mit diesen Möglichkeiten der Datensammlung und Analyse die strategische Planung, das Marketing und die Parkplatz-Logistik zu unterstützen.


# Zielsetzung

Das Ziel dieser Diplomarbeit ist es, mit Daten des Besucherparkplatzes der Zotter Schokolade GmbH Analysen und Visualisierungen zu bieten, mit deren Hilfe bessere Entscheidungen in den Bereichen Betriebsführung, Marketing und Ressourcenplanung ermöglicht werden.

Das entwickelte System soll:
- Transparenz durch Echtzeit-Einblicke in Parkplatzauslastung, Besucherfrequenz und Stoßzeiten liefern
- Die Ressourcenplanung durch eine Datengrundlagen für strategische Planung unterstützen
- Verbesserung des zielgerichteten Marketings durch die Bereitstellung von Herkunftsanalysen 
- Basis für die GHG (Greenhouse Gas Protocol) Scope 3 Emissionsberechnung des Besucheraufkommens liefern (https://ghgprotocol.org/corporate-value-chain-scope-3-standard)
- Datenschutz und DSGVO-Konformität durch Anonymisierung aller personenbezogenen Daten gewährleisten

Das System soll nicht:

- Individuelle Besucher identifizieren oder tracken
- Bewegungsprofile einzelner Fahrzeuge über den Parkplatzkontext hinaus erstellen
- Personenbezogene Daten dauerhaft speichern

Durch die Abgrenzung dieser Ziele wird sichergestellt, dass das System nur als Werkzeug für betriebliche Optimierung dient, ohne dabei die Privatsphäre der Besucher zu gefährden.


# Aufgabenstellung

Um diesen Anforderungen gerecht zu werden wurden diese in folgende Teilaufgaben aufgeteilt:

- Installation bzw. Montage und Konfiguration der erforderlichen Hardware 

- Implementierung eines ALPR-Systems (Automatic License Plate Recognition) zur Kennzeichenerkennung

- Erkennung von Ein- und Ausfahrten mit Zeitstempeln

- Auswertung der Kennzeichen nach Herkunftsland und Region mit der Erkennung von Fahrzeugtypen (PKW, LKW, etc.)

- DSGVO-konforme Anonymisierung und Speicherung der erfassten Daten

- Erstellung eines Scripts für die automatische Datenbank-Initialisierung

- Entwicklung einer automatisierten Backup- und Wiederherstellungslösung

- Implementierung eines Dashboards zur Visualisierung der Daten

- Integration eines E-Mail-Benachrichtigungssystems


# Aufbau der Arbeit
Umschreibung des aufbaus
TO-DO