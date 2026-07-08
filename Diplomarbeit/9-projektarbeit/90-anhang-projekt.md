# Anhang zur Projektarbeit

## A. Auszug aus dem API-Vertrag

| Methode | Endpunkt | Beschreibung |
|---|---|---|
| POST | `/api/auth/login` | Anmeldung, Ausgabe eines JWT |
| GET | `/api/cases` | Liste der Vorgänge (rollenabhängig) |
| POST | `/api/cases` | Neuen Vorgang anlegen |
| GET | `/api/cases/{id}` | Einzelnen Vorgang abrufen |
| PATCH | `/api/cases/{id}` | Vorgang aktualisieren / Status ändern |
| GET | `/api/reports` | Auswertungen abrufen |

## B. Datenmodell (Auszug)

- `users` -- Benutzerkonten mit Rolle und Referenz auf `departments`.
- `departments` -- Organisationseinheiten des Bürgerservices.
- `cases` -- Vorgänge mit Status, Priorität, Sachbearbeiter:in und
  Zeitstempeln.
- `case_entries` -- Einzelposten/Protokolleinträge je Vorgang.
- `audit_log` -- revisionssicheres Protokoll aller Änderungen.

## C. Begleitende Unterlagen

Die vollständigen Projektdokumente (Kooperationsvertrag, Lasten- und
Pflichtenheft, Detailspezifikation, Protokolle, Zeitschreibung) liegen
versioniert im Git-Repository des Gesamtprojekts unter `docs/` vor
(siehe Einleitung zum Gesamtprojekt).
