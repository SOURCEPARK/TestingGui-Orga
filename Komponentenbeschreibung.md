# 🧩 Projektübersicht: Test Runner System

## 🗂 Allgemeine Architektur

Das System besteht aus:

- **Frontend (GUI)**: Wird vom User über einen Reverse Proxy aufgerufen.
- **Backend-Service**: Verarbeitet Heartbeats, verwaltet Testdaten, kommuniziert mit GitHub und speichert Daten in einer Datenbank.
- **Testrunner**: Melden sich regelmäßig (z. B. alle x Sekunden) beim Backend mit einem Heartbeat.
- **Reverse Proxy + Docker**: Steuert den Zugriff auf Frontend und Backend. Alle Services laufen containerisiert in einem Docker-Netzwerk.

---

## 🔁 Ablauf (vereinfacht)

1. **Testbeschreibungen** werden aus einem GitHub-Repository geladen (z. B. via Polling, Webhook oder beim Aufruf des GUIs).
2. Diese enthalten **Metadaten** und Anweisungen für die Ausführung durch Testrunner.
3. **Testrunner** melden sich regelmäßig beim Backend (**Heartbeat**), damit ihr Status bekannt ist.
4. Das System **ordnet Tests passenden Testrunnern zu**, basierend auf verfügbaren Ressourcen und Umgebungen.
5. Während der Ausführung sendet der Testrunner **regelmäßige Updates**, die im Frontend angezeigt werden.
6. Nach Abschluss kann ein **Bericht heruntergeladen** werden.

---

## 🧱 Komponenten & Zuständigkeiten

### 🔹 Frontend (Paul & Victoria)

- Anzeige von:
  - Aktiven/verfügbaren Testrunnern
  - Laufenden und vergangenen Tests
  - Teststatus & Ergebnisberichten
- Interaktionen:
  - Tests starten
  - Bericht herunterladen
- Kommuniziert direkt via HTTP mit dem Backend

### 🔹 Backend (Teamkollegen)

- Bereitstellung des Heartbeat-Endpunkts
- Verwaltung von Teststatus & Ergebnissen in einer PostgreSQL-Datenbank
- Abrufen und Speichern von Testbeschreibungen aus GitHub
- Bereitstellung von Daten-Endpunkten für das Frontend

### 🔹 Docker & Reverse Proxy (Paul & Victoria)

- Dockerisierung aller Services
- Aufbau eines gemeinsamen Docker-Netzwerks
- Bereitstellung einer `docker-compose.yml`
- Optional: Volumes für Datenpersistenz außerhalb der Container
- Reverse Proxy regelt:
  - Zugriffe auf das GUI (Frontend)
  - Anfragen an das Backend (z. B. von Testrunnern oder später vom Systemen des Kunden)

---

## 🧩 Offene Fragen

- Wie genau werden die Tests aus dem GitHub-Repo geladen? => Refresh-Button (zeigt Datum des letzten Refreshs an)
- Datenbankdesign & Schema müssen noch entworfen werden

---

## ✅ Teamverteilung (Vorschlag)

- **Frontend & Docker/Proxy**: Paul & Victoria
- **Backend & Datenbank**: Die drei weiteren Teammitglieder
- **Victoria** übernimmt zusätzlich die organisatorische Koordination
