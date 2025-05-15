# Testrunner API Specification

## Überblick

Dieses Repository enthält zwei API-Spezifikationen, die für die Kommunikation zwischen dem Testrunner und unserem Backend verwendet werden:

- **Testrunner Command API** - Schnittstelle, um Tests auf dem Testrunner zu starten, neu zu starten, zu stoppen und deren Status abzufragen. Diese API wird vom Backend verwendet, um Kommandos an den Testrunner zu senden.

- **Testrunner Monitoring API** - Schnittstelle, über die der Testrunner Statusupdates, Abschlussberichte und Heartbeats an das Backend sendet.
