# Ergebnisse und Anwendung im Projekt

Dieses Kapitel beschreibt die konkrete Umsetzung der Datenbank und ihre
Einbindung in das Gesamtprojekt BIS-Ares.

## Datenbankarchitektur und Werkzeuge

Umgesetzt wurde die Datenbank in PostgreSQL. Als Sprache für Schema und
Migrationen dient SQL, ergänzt durch ein Migrationstool, das
Versionsnummern aus den Dateinamen ableitet und den Stand in einer
Hilfstabelle festhält. Für Entwicklung und Tests kommen containerbasierte
Instanzen zum Einsatz, die reproduzierbar erzeugt und wieder verworfen
werden können.

## Implementiertes Datenmodell

### Benutzer und Organisationseinheiten

Die Tabelle `users` speichert Kennung, Hash-Referenz, Rolle und
Zeitstempel; `departments` bildet die Organisationseinheiten ab. Ein
Fremdschlüssel in `users` stellt sicher, dass jeder Benutzer zu einer
gültigen Organisationseinheit gehört.

### Vorgänge und Einträge

`cases` hält die Kerninformation je Vorgang. Über den Typ `ENUM` werden
nur erlaubte Statuswerte akzeptiert. `case_entries` speichert einzelne
Einträge und Protokollschritte und referenziert den übergeordneten
Vorgang. Statuswechsel werden als dedizierte Einträge in `case_entries`
nachvollziehbar abgelegt. Ein vereinfachter Auszug der Vorgangstabelle
veranschaulicht die Umsetzung:

```sql
CREATE TYPE case_status AS ENUM
  ('new', 'in_progress', 'waiting', 'done', 'cancelled');

CREATE TABLE cases (
  id          SERIAL PRIMARY KEY,
  title       TEXT NOT NULL,
  status      case_status NOT NULL DEFAULT 'new',
  priority    SMALLINT NOT NULL CHECK (priority BETWEEN 1 AND 5),
  assignee_id INTEGER REFERENCES users(id) ON DELETE RESTRICT,
  created_at  TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at  TIMESTAMPTZ NOT NULL DEFAULT now()
);
```

### Audit-Protokollierung

Jede ändernde Operation wird über Trigger in der Tabelle `audit_log`
mitgeschnitten: Tabellenname, Datensatzkennung, Art der Änderung,
Zeitstempel und auslösende Benutzerkennung. Damit ist die Datenbank
selbst die Quelle der Wahrheit für die Nachvollziehbarkeit -- unabhängig
davon, ob das Backend korrekt protokolliert.

## Integritätssicherung

Constraints sichern die Daten:

- `NOT NULL` auf Pflichtfeldern;
- `UNIQUE` auf Kennungen;
- `CHECK` für erlaubte Wertebereiche (z.\,B. Priorität);
- Fremdschlüssel mit `ON DELETE RESTRICT`.

Transaktionen bündeln zusammengehörige Schritte, insbesondere
Statuswechsel mit ihren Protokolleinträgen.

## Auswertungen

Auswertungen aggregieren Vorgänge nach Zeitraum, Organisationseinheit und
Status. Für wiederkehrende Auswertungen werden materialisierte Sichten
vorgehalten, die periodisch aktualisiert werden. So bleiben auch große
Datenbestände schnell auswertbar.

## Anwendung im Gesamtprojekt

Die Datenbank ist die unterste Schicht von BIS-Ares. Ihre Verträge
(Tabellen, Indizes, Auswertungssichten) wurden mit dem Backend von Maria
abgestimmt; das Frontend von Samaneh profitiert indirekt über eine
durchdachte, rollengerechte Datenbasis. Die Migrationskette stellt
sicher, dass alle drei Teile stets gegen einen konsistenten Datenstand
entwickeln und testen.

## Trigger und Automatik

Wiederkehrende Abläufe, die zwingend bei jeder Änderung ausgeführt
werden müssen, sind als Trigger hinterlegt -- nicht etwa im Backend.
Dazu gehört das Aktualisieren des `updated_at`-Zeitstempels bei jeder
Änderung sowie das Schreiben des `audit_log`. Durch diese Verlagerung in
die Datenbank ist die Nachvollziehbarkeit selbst dann gewährleistet,
wenn später einmal ein anderes Backend oder ein Wartungszugriff auf die
Daten erfolgt.

## Performancemessungen

Anhand eines Testdatenbestands wurden Auswertungen vermessen. Während
kleine Anfragen durch Indizes durchgehend schnell beantwortet werden,
zeigte sich bei der Vollauswertung über viele Vorgänge hinweg der
Vorteil der materialisierten Sichten: lag die direkte Aggregation im
Bereich mehrerer Sekunden, reduzierte die vorberechnete Sicht die
Antwort auf den Bruchteil einer Sekunde. Das bestätigt die Entscheidung,
wiederkehrende Auswertungen zu cachen.

## Backup und Wiederherstellung

Backups werden als logische Exporte und als physische Snapshots
vorgehalten. Eine Wiederherstellung wurde im Rahmen der Arbeit
geprobt: Aus einem Snapshot ließ sich ein konsistender Stand
rekonstruieren; aus dem logischen Export konnten einzelne Tabellen
gezielt zurückgespielt werden. Beide Wege sind dokumentiert und
reproduzierbar, sodass im Ernstfall nicht improvisiert werden muss.

## Anwendung im Gesamtprojekt

Die Datenbank liefert die Datenbasis, auf der sowohl Backend als auch
Frontend aufsetzen. Stabilität und Konsistenz der Datenbank sind damit
Voraussetzung für das Funktionieren des Gesamtsystems -- und rechtfertigen
das besondere Gewicht, das in dieser Arbeit auf Integrität,
Nachvollziehbarkeit und Migrationssicherheit gelegt wurde.

## Konkrete Auswertungen

Umgesetzt wurden mehrere Auswertungen, die im Bürgerservice relevant
sind: Vorgänge je Zeitraum, Vorgänge je Organisationseinheit sowie
Verteilungen nach Status. Jede Auswertung läuft über vorbereitete,
parametrisierte Abfragen, die Injection ausschließen und die Ausführung
vorhersagbar machen. Wiederkehrende Auswertungen greifen auf
materialisierte Sichten zurück und reduzieren so die Last auf der
Datenbank auch bei häufiger Abfrage deutlich.

## Umgang mit Änderungen am Modell

Im Lauf der Entstehung wurden mehrere Änderungen am Modell nötig --
etwa das Nachziehen einer Fremdschlüsselbeziehung und die Erweiterung
des Status-Enums. Jede Änderung erfolgte über eine eigene Migration,
die vorwärts wie rückwärts anwendbar ist. So ließ sich zu jedem
Zeitpunkt ein konsistenter Stand herstellen, ohne dass Umgebungen
manuell nachgezogen werden mussten. Gerade im Team war diese
Disziplin wertvoll, weil alle drei Teile stets denselben Datenstand
vorfanden.

## Erprobte Datenbank-Szenarien

Die Datenbank wurde anhand typischer Szenarien erprobt: Massenladen
von Testdaten, nebenläufige Änderungen am selben Vorgang (korrekt
durch Transaktionen und Sperren gelöst), Löschversuche an referenzierten
Datensätzen (durch `ON DELETE RESTRICT` abgewiesen) sowie die
Prüfung, ob Trigger das Audit-Log konsistent füllen. In allen Fällen
verhielt sich die Datenbank wie entworfen -- ein Beleg dafür, dass die
Modellierungsentscheidungen tragfähig sind.
