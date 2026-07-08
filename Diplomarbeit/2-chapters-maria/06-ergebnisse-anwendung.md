# Ergebnisse und Anwendung im Projekt

Dieses Kapitel beschreibt die konkrete Umsetzung des Backends und seine
Einbindung in das Gesamtprojekt BIS-Ares.

## Entwicklungsumgebung und Projektstruktur

Umgesetzt wurde das Backend in TypeScript mit Node.js und Express. Die
Projektstruktur folgt der gewählten Schichtenarchitektur: je ein
Verzeichnis für Routen, Services, Datenbankzugriffe, Middleware und
Tests. Als Paketmanager dient *npm*, als Testrunner *Jest*. Über
TypeScript-Compiler und *ESLint* werden Typisierung und einheitlicher
Code-Stil sichergestellt.

## Authentifizierung und Autorisierung

Die Anmeldung erfolgt über `POST /api/v1/auth/login`. Nach Prüfung von
Benutzername und Passwort (bcrypt-Vergleich) stellt der Server ein JWT
aus, das Rolle und Benutzerkennung als Claims enthält. Eine
Auth-Middleware liest das Token bei jedem geschützten Request, verifiziert
die Signatur und stellt die Rolle für die nachfolgende Autorisierung
bereit. Rollenprüfungen sind als wiederverwendbare Guard-Funktionen
umgesetzt, sodass Endpunkte deklarativ geschützt werden können.

## Vorgangsverwaltung

Vorgänge werden über die Ressource `/api/v1/cases` abgebildet:

- `GET /api/v1/cases` liefert eine gefilterte, rollenabhängige Liste;
- `POST /api/v1/cases` legt einen neuen Vorgang an;
- `GET /api/v1/cases/{id}` ruft einen einzelnen Vorgang ab;
- `PATCH /api/v1/cases/{id}` aktualisiert Felder oder löst einen
  definierten Zustandsübergang aus;
- `DELETE /api/v1/cases/{id}` entfernt Vorgänge (nur durch Aufsicht
  und nur im Sinne einer Lösch-Stornierung).

Jede Änderung wird mit Zeitstempel, auslösender Person und Art der
Änderung im Audit-Log hinterlegt, sodass Vorgänge nachvollziehbar bleiben.
Eine Antwort auf `GET /api/v1/cases/42` liefert beispielsweise:

```json
{
  "id": 42,
  "title": "Anfrage Bürgerservice",
  "status": "in_progress",
  "assignee": "maier",
  "createdAt": "2026-03-01T09:12:00Z",
  "updatedAt": "2026-03-04T14:30:00Z"
}
```

## Validierung und Fehlerbehandlung

Eingehende Anfragen werden anhand von Schemata validiert; scheitert die
Prüfung, antwortet der Server mit HTTP-Status 422 und einer strukturierten
Fehlerliste. Eine zentrale Fehler-Middleware fängt darüber hinaus alle
unerwarteten Fehler ab und wandelt sie in ein einheitliches Antwortformat
um, ohne interne Details preiszugeben.

## Auswertungen

Auswertungen laufen über den Endpunkt `/api/v1/reports`. Sie aggregieren
Vorgänge nach Zeiträumen, Organisationseinheiten und Status. Weil
Auswertungen potenziell datenintensiv sind, werden sie serverseitig
gefiltert und paginiert; große Ergebnismengen werden in Blöcken
ausgeliefert.

## Tests

Die Teststrategie umfasst drei Ebenen:

- **Unit-Tests** für Services und Hilfsfunktionen;
- **Integrationstests** für Routen gegen eine Testdatenbank;
- **Vertragstests** für die API gegenüber Frontend und Datenbank-Teil.

Besonderes Gewicht liegt auf den Vertragstests, weil sie sicherstellen,
dass die abgestimmten Schnittstellen stabil bleiben -- eine zentrale
Voraussetzung für die verteilte Teamarbeit.

## Anwendung im Gesamtprojekt

Das Backend ist die Verbindung zwischen Samanehs Frontend und Negins
Datenbank. Die API-Verträge wurden früh abgestimmt und versioniert
gepflegt, sodass alle drei Teile weitgehend unabhängig voneinander
entwickelt werden konnten. Änderungen an den Verträgen wurden über
Change Requests nachverfolgt.

## Caching und Performance

Lesezugriffe, die sich selten ändern, werden serverseitig zwischengespeichert,
um Datenbanklast zu reduzieren. Auswertungen verwenden einen
kompakt vorberechneten Bestand, statt bei jeder Anfrage neu zu
aggregieren. Pagination verhindert, dass große Ergebnismengen
ungefiltert übertragen werden. Wo sinnvoll, kommen zusammengesetzte
Indizes auf Datenbankseite zum Einsatz, die mit dem Datenbank-Teil
abgestimmt wurden.

## Dokumentation der Schnittstelle

Die API ist in maschinenlesbarer Form (OpenAPI) beschrieben; daraus wird
eine für Menschen lesbare Dokumentation erzeugt. Jeder Endpunkt ist mit
Zweck, Parametern, erwarteten Antworten und Fehlern hinterlegt. Diese
Dokumentation ist die verbindliche Grundlage für das Frontend und wird
gemeinsam mit den Verträgen versioniert gepflegt.

## Deployment und Betrieb

Die Anwendung wird containerisiert ausgeliefert; ein Build erzeugt ein
reproduzierbares Image. Umgebungsvariablen steuern die Konfiguration zur
Laufzeit. Ein einfaches Health-Checking ermöglicht der
Betriebsumgebung, den Zustand der Anwendung abzufragen und bei Bedarf
neu zu starten. Ein durchgängiges Deployment-Pipeline ist als
Weiterführung vorgesehen, im Rahmen dieser Arbeit aber nur
ansatzweise umgesetzt.

## Konkrete Endpunkte im Überblick

Die umgesetzte API umfasst Ressourcen für Anmeldung, Vorgänge,
Einträge und Auswertungen. Anmelden und Token-Erneuerung laufen unter
`/api/v1/auth/*`; die Vorgangsverwaltung unter `/api/v1/cases`; einzelne
Einträge unter `/api/v1/cases/{id}/entries`; Auswertungen unter
`/api/v1/reports`. Alle Antworten folgen einem einheitlichen Format:
bei Erfolg ein `data`-Feld mit dem Ergebnis, bei Fehler ein `errors`-Feld
mit strukturierten Einträgen. Dadurch kann das Frontend die Behandlung
von Ergebnissen und Fehlern an zentraler Stelle vereinheitlichen.

## Verhalten bei Fehlern

Fehler sind nicht die Ausnahme, sondern der Normalfall, den es sauber
zu behandeln gilt. Validierungsfehler werden gesammelt zurückgemeldet,
damit das Frontend alle Probleme einer Anfrage auf einmal anzeigen kann.
Authentifizierungsfehler führen zum Abmelden und Zurückleiten des
Clients. Unerwartete Serverfehler werden protokolliert, nach außen aber
nur in einer generischen Form ausgeliefert -- interne Details wie
Stacktraces verlassen niemals das Backend.

## Erprobte Szenarien

Die Anwendung wurde anhand repräsentativer Szenarien erprobt:
Anmeldung verschiedener Rollen, Anlegen und Bearbeiten von Vorgängen,
Statuswechsel, Auswertungen sowie das Verhalten bei ungültigen und
unberechtigten Zugriffen. Die Vertragstests stellten sicher, dass
Schnittstellenänderungen sofort auffallen. Insgesamt verhielt sich das
Backend über alle Szenarien hinweg stabil und vorhersehbar.
