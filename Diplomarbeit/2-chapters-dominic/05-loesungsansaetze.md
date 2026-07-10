# Lösungsansätze

Dieses Kapitel entwickelt die Anforderungen an das Backend und begründet
die wichtigsten Entwurfsentscheidungen.

## Anforderungen an das Backend

Aus dem Lastenheft ergeben sich sowohl funktionale als auch nichtfunktionale
Anforderungen an die Anwendungsschicht. Zu den funktionalen gehören die
Anmeldung, die Verwaltung von Vorgängen sowie Auswertungen; zu den
nichtfunktionalen gehören Verfügbarkeit, Performance, Sicherheit und
Wartbarkeit.

### Funktionale Anforderungen

- **Anmeldung und Sitzungsverwaltung:** Benutzer melden sich mit
  Zugangsdaten an und erhalten ein JWT.
- **Vorgangsverwaltung:** Vorgänge können angelegt, gelesen, geändert und
  in ihrem Status weitergeschaltet werden.
- **Rollenkonzept:** Verschiedene Rollen sehen und bearbeiten unterschiedliche
  Bestandteile.
- **Auswertungen:** Aggregierte Auswertungen können abgerufen werden.
- **Revisionssicherheit:** Jede ändernde Operation wird im
  Audit-Protokoll hinterlegt.

### Nichtfunktionale Anforderungen

- **Verfügbarkeit:** die Anwendung soll auch unter Last stabil reagieren;
- **Performance:** typische Anfragen sind in unter 300\,ms beantwortet;
- **Sicherheit:** DSGVO-konforme Verarbeitung, TLS, kein Speichern
  klartextiger Passwörter;
- **Wartbarkeit:** klare Schichten, automatisierte Tests,
  Dokumentation der API.

## Benutzergruppen

- **Sachbearbeiter:innen** erfassen und bearbeiten Vorgänge;
- **Aufsicht** führt Freigaben und Auswertungen durch;
- **Administration** verwaltet Benutzer, Rollen und
  Systemeinstellungen.

## Entwurfsentscheidungen

### Schichten im Backend

Das Backend ist intern weiter unterteilt:

1. **Routingschicht** (Controller): nimmt HTTP-Anfragen entgegen und
   delegiert;
2. **Serviceschicht:** enthält die Geschäftslogik;
3. **Zugriffsschicht auf die Datenbank:** kapselt Persistenz;
4. **Querschichten:** Authentifizierung, Validierung, Fehlerbehandlung,
   Protokollierung als Middleware.

### Begründung der Technologieauswahl

Node.js in Kombination mit Express wurde gewählt, weil beide leichtgewichtig,
gut dokumentiert und im Team bereits bekannt sind. Als Programmiersprache
kommt TypeScript zum Einsatz, dessen statische Typisierung Fehler früh
sichtbar macht. Als Datenbank wird -- in Abstimmung mit dem Datenbank-Teil
-- PostgreSQL verwendet; als Schnittstelle zwischen Anwendung und Datenbank
dient ein objektrelationaler Mapper, der im nächsten Kapitel begründet wird.

### API-Design

Die Schnittstelle wird als versionierte REST-API ausgeführt
(`/api/v1/...`). Antworten folgen einem einheitlichen Format mit Feldern
für Daten und Fehler. Statuswechsel an Vorgängen werden nicht über
willkürliche `PATCH`-Aufrufe, sondern über dedizierte
Zustandsübergänge abgebildet, um fehlerhafte Übergänge auszuschließen.

### Sicherheitskonzept

Passwörter werden mit einem modernen Hashverfahren (bcrypt) gespeichert,
JWT werden mit begrenzter Gültigkeit ausgestellt und bei Bedarf über
Refresh-Tokens erneuert. Sensible Endpunkte sind zusätzlich mit
Rate-Limiting abgesichert; jeder Schreibzugriff landet im Audit-Log.

## Konfiguration und Umgebungen

Konfiguration -- Datenbankverbindungen, Geheimnisse, Ports -- wird
strikt über Umgebungsvariablen gesteuert; es gibt keine hardcodierten
Zugangsdaten im Code. Für Entwicklung, Test und einen abbildbaren
Produktivbetrieb werden getrennte Konfigurationen gepflegt. Dadurch
bleibt nachvollziehbar, welche Einstellung in welcher Umgebung gilt, und
Geheimnisse verlassen nie die jeweils vorgesehene Stelle.

## API-Versionierung

Schnittstellen ändern sich im Lauf der Zeit. Um Brüche für das Frontend
beherrschbar zu halten, wird die API versioniert
(`/api/v1/...`). Brechen Änderungen die Kompatibilität, entsteht eine
neue Version; alte Versionen bleiben Übergangszeit erhalten. So kann das
Frontend schrittweise umgestellt werden, ohne dass ein einseitiger
Eingriff den Betrieb stört.

## nichtfunktionale Zielgrößen

Aus den Anforderungen wurden messbare Zielgrößen abgeleitet: typische
Lesezugriffe unter 300\,ms, Schreibzugriffe unter 500\,ms, eine
Verfügbarkeit von 99\,% im Prototypbetrieb sowie eine
Testabdeckung an den Schnittstellen von mindestens 80\,%. Diese Größen
sind nicht als Garantie, sondern als Leitplanke für Entwurf und Tests zu
verstehen.

## Ablauf einer typischen Anfrage

Um den Entwurf greifbar zu machen, sei der Weg einer typischen Anfrage
skizziert. Der Client schickt `GET /api/v1/cases?status=in_progress` mit
JWT im Header. Nacheinander durchläuft die Anfrage: Protokollierung,
CORS-Prüfung, JWT-Verifikation, Rollenprüfung, Eingabevalidierung und
schließlich die Routenfunktion. Diese delegiert an den zuständigen
Service, der die Geschäftslogik ausführt und den Datenbankzugriff
anfordert. Das Ergebnis wandert als typisiertes Objekt zurück, wird in
JSON serialisiert und -- samt passendem Statuscode -- an den Client
gegeben. Tritt irgendwo ein Fehler auf, bricht die Kette ab und die
zentrale Fehler-Middleware erzeugt eine einheitliche Antwort.

## Bewertung der Lösungsansätze

Die gewählten Ansätze -- Schichtentrennung, tokenbasierte
Authentifizierung, versionierte REST-Schnittstelle, Validierung an den
Rändern -- ergänzen sich sinnvoll. Alternativen wie eine
sitzungsbasierte Authentifizierung wurden erwogen, jedoch verworfen, weil
sie einen serverseitigen Sitzungsspeicher erfordern und die
Skalierbarkeit erschweren. Auch GraphQL kam als Alternative zu REST zur
Debatte; wegen der überschaubaren, gut abgrenzbaren Ressourcen und der
gerordenen Datenzugriffe fiel die Wahl jedoch auf REST. Die getroffenen
Entscheidungen sind im Pflichtenheft begründet dokumentiert.
