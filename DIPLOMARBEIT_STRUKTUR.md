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

*   **2.1 Containerisierung (Docker):** Vorteile für Deployment und Isolation
*   **2.2 Microservice Architektur:** Prinzipien und Abgrenzung zum Monolithen (Warum?)
*   **2.3 ALPR (Automatic License Plate Recognition):** Grundfunktionsweise der Kennzeichenerkennung (Technologie, OCR, Anbieter)


## 3. Hardware- und Technologieauswahl 

*   **3.1 Anforderungsanalyse an die Hardware:**
    *   Umgebungsbedingungen (Außenbereich (Luftbild), Wetter, Lichtverhältnisse)
    *   Leistungsanforderungen (Verarbeitungsgeschwindigkeit, Netzwerk)
*   **3.2 Evaluierung der Komponenten:**
    *   Kamera: Vergleich verschiedener Modelle (z.B. Synology vs. andere IP-Cams)
        *   Kriterien: Auflösung, Nachtsicht, API-Verfügbarkeit, Kosten
    *   Server/Recheneinheit: (z.B. Raspberry Pi vs. Mini-PC vs. Cloud vs. NAS), Deployment und Hosting
*   **3.3 Argumentation für Software-Technologien**
    *   Container, Docker, Microservices
        Alternativen auflisten und Entscheidung argumentieren.
*   **3.3 Technologieauswahl für die Kennzeichenerkennung:**
    *   Warum Plate Recognizer und nicht open source oder intern.


## 4. Systementwurf und Architektur

*   **4.1 Gesamtarchitektur:**
    *   Diagramm der Microservices (Auth, Data Collection, Analytics, Notification, Web)
    *   Kommunikationswege (REST API, interne Kommunikation)
*   **4.2 Datenbankdesign:**
    *   ER-Diagramm (Entity Relationship)
    *   Erklärung der wichtigsten Entitäten (`VehicleObservation`, `Preferences`)
*   **4.3 Sicherheitskonzept:**
    *   Authentifizierung (Entpoint-Sicherheit)
    *   Datenschutz (Umgang mit Kennzeichen-Daten)
    *   Data Lifecycle


## 5. Implementierung

*   **5.1 Konfiguration Synology Surveillance Station:**
    *   IP Camera config
    *   Deep Video Analytics Config (Bereich etc)
    *   Action Rule config
*   **5.1 Data Collection Service:**
    *   Ablaufdiagramm: Von der Kamera-Triggerung bis zum Speichern in der DB.
    *   Besonderheit: Integration der Kamera-API (Code-Snippet: Wichtige Logik aus `camera_handler.py`).
    *   Verarbeitung von "Municipalities" (Bezirkserkennung).
*   **5.2 Notification Service:**
    *   Trigger-Logik für Benachrichtigungen (wann wird eine Mail gesendet?).
*   **5.3 Grafana:**
    *   Aufbau, Darstellungen


## 6. Infrastruktur, Deployment und Betrieb

*   **6.1 Container-Orchestrierung:**
    *   docker-compose Strategie (Dev vs. Prod).
*   **6.2 CI/CD Pipelines, Deployment + Betrieb:**
    *   Automatisierung mit GitHub Actions (Build & Test), Deployment (Portainer)
*   **6.3 Monitoring & Logging:**
    *   Strategien beim Monitoring und Logging
*   **6.4 Datenbank-Management:**
    *   Tabellenerzeugung, Init-Script, Migrationen (Alembic) zur Schema-Verwaltung.
*   **6.5 Backup-Strategie:**
    *   Erklärung der Backup-Skripte und des Wiederherstellungsprozesses (Disaster Recovery, RPO, RTO).
*   **6.6 Documentation as Code:**
    *   MkDocs, Dokumentation im Repo


## 7. Qualitätssicherung und Tests
*   **7.1 Teststrategie:** Unit-Tests (Pytest) und Integrationstests (FastAPI), Test Coverage
*   **7.2 Validierung:** Überprüfung der Hardware/Software-Kombination in der Praxis (Erkennungsrate bei Regen/Nacht, Strategien gegen Falscherkennungen (Auflistung doppelter Kennzeichen etc)).


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
*   Formeln
*   Große Diagramme
*   Konfigurationsdateien (Auszüge)
*   Arbeitszeitnachweis
