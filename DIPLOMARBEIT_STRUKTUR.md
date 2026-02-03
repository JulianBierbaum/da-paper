# Gliederung für die Diplomarbeit

- Autor in Footnote
- Keine Relationale Datenbanken vergleichen

---

## I. Formaler Rahmen (Pre-Content)
*   **Eidesstattliche Erklärung**
*   **Kurzbeschreibung (Deutsch)**
*   **Abstract (Englisch)**
*   **Vorwort**
*   **Inhaltsverzeichnis**

---

## 1. Einleitung

*   **1.1 Motivation:** Warum wird dieses System benötigt? (z.B. Automatisierung von Zufahrtskontrollen, statistische Erhebung)
*   **1.2 Zielsetzung:** Abgrenzung (Was soll das System können, was nicht?)
*   **1.3 Aufgabenstellung:** Klare Definition, was im Rahmen der Arbeit zu tun war (Pflichtenheft)
*   **1.4 Aufbau der Arbeit:** Kurzer Wegweiser durch die Kapitel


## 2. Theoretische Grundlagen
*Kurzer Abriss der Technologien, um das Verständnis für die späteren Entscheidungen zu schaffen.*

*   **2.1 Microservices Architektur:** Prinzipien und Abgrenzung zum Monolithen (Warum?)
*   **2.2 Containerisierung (Docker):** Vorteile für Deployment und Isolation
*   **2.3 ALPR (Automatic License Plate Recognition):** Grundfunktionsweise der Kennzeichenerkennung (Technologie, OCR, Anbieter)


## 3. Hardwareauswahl und Systemumgebung

*   **3.1 Anforderungsanalyse an die Hardware:**
    *   Umgebungsbedingungen (Außenbereich (Luftbild), Wetter, Lichtverhältnisse)
    *   Leistungsanforderungen (Verarbeitungsgeschwindigkeit, Netzwerk)
*   **3.2 Evaluierung der Komponenten:**
    *   **Kamera:** Vergleich verschiedener Modelle (z.B. Synology vs. andere IP-Cams)
        *   *Kriterien:* Auflösung, Nachtsicht, API-Verfügbarkeit, Kosten
    *   **Server/Recheneinheit:** (z.B. Raspberry Pi vs. Mini-PC vs. Cloud vs. NAS)
*   **3.3 Begründung der Entscheidung:**
    *   Detaillierte Darlegung, warum genau diese Hardware gewählt wurde (Kosten-Nutzen-Analyse, technische Notwendigkeit)
*   **3.4 Netzwerkinfrastruktur:** Wie sind Kamera und Server verbunden


## 4. Systementwurf und Architektur
*Das Konzept VOR der Programmierung.*

*   **4.1 Gesamtarchitektur:**
    *   Diagramm der Microservices (Auth, Data Collection, Analytics, Notification, Web)
    *   Kommunikationswege (REST API, interne Kommunikation)
*   **4.2 Datenbankdesign:**
    *   ER-Diagramm (Entity Relationship)
    *   Erklärung der wichtigsten Entitäten (`VehicleObservation`, `User`, `Preferences`)
*   **4.3 Sicherheitskonzept:**
    *   Authentifizierung (Entpoint-Sicherheit)
    *   Datenschutz (Umgang mit Kennzeichen-Daten)
    *   Data Lifecycle


## 5. Implementierung

*   **5.1 Data Collection Service:**
    *   Ablaufdiagramm: Von der Kamera-Triggerung bis zum Speichern in der DB.
    *   Besonderheit: Integration der Kamera-API (Code-Snippet: Wichtige Logik aus `camera_handler.py`).
    *   Verarbeitung von "Municipalities" (Bezirkserkennung).
*   **5.2 Notification Service:**
    *   Trigger-Logik für Benachrichtigungen (wann wird eine Mail gesendet?).
*   **5.3 Datenbank-Management:**
    *   Einsatz von ORM (SQLAlchemy) und Migrationen (Alembic) zur Schema-Verwaltung.
*   **5.4 Grafana:**
    *   Aufbau, Darstellungen
*   **5.5 Wichtige Algorithmen/Lösungen:**
    *   Herausragende Code-Teile


## 6. Infrastruktur, Deployment und Betrieb

*   **6.1 Container-Orchestrierung:**
    *   Erläuterung der `docker-compose` Strategie (Dev vs. Prod).
*   **6.2 CI/CD Pipelines:**
    *   Automatisierung mit GitHub Actions (Build & Test), Deployment
*   **6.3 Monitoring & Logging:**
    *   Strategien beim Monitoring und Logging
*   **6.4 Backup-Strategie:**
    *   Erklärung der Backup-Skripte und des Wiederherstellungsprozesses (Disaster Recovery).
*   **6.5 Documentation as Code:**
    *   MkDocs, Dokumentation im Repo


## 7. Qualitätssicherung und Tests
*   **7.1 Teststrategie:** Unit-Tests (Pytest) und Integrationstests. (Test Coverage).
*   **7.2 Validierung:** Überprüfung der Hardware/Software-Kombination in der Praxis (Erkennungsrate bei Regen/Nacht, Strategien gegen Falscherkennungen).


## 8. Fazit und Ausblick
*   **8.1 Zusammenfassung der Ergebnisse.** Überblick, Trefferrate, Reflexion
*   **8.2 Kritische Reflexion:** 
    *   Was lief gut, was würde man heute anders machen (Hardware oder Software)? 
    *   Wurden alle Ziele (Funktional und Nicht-Funktional umgesetzt)
*   **8.3 Ausblick:** Erweiterungsmöglichkeiten (z.B. KI-Modelle direkt auf der Hardware, App-Anbindung)

---

## II. Verzeichnisse (Post-Content)
*   **Abbildungsverzeichnis**
*   **Quellcodeverzeichnis** (falls Listings im Text referenziert sind)
*   **Glossar** (Erklärung von Begriffen wie ALPR, JWT, Docker Container)
*   **Literaturverzeichnis**


## III. Anhang
*   Große Diagramme
*   Konfigurationsdateien (Auszüge)
