# Lösungsansätze

In diesem Kapitel werden die Anforderungen an die Datenbank entwickelt und
die zentralen Modellierungsentscheidungen begründet.

## Anforderungen an die Datenbank

Aus Lasten- und Pflichtenheft ergeben sich Anforderungen an die
Datenhaltung: dauerhaftes Speichern von Benutzern, Organisationseinheiten
und Vorgängen; rollenbasierte Sichtbarkeit; aggregierte Auswertungen;
revisionssichere Protokollierung; Datenschutzkonformität.

## Entitäten und Beziehungen

Aus der Aufgabenanalyse ergeben sich folgende Kernentitäten:

- **users** -- Benutzerkonten mit Rolle und Referenz auf eine
  Organisationseinheit;
- **departments** -- Organisationseinheiten des Bürgerservices;
- **cases** -- Vorgänge mit Status, Priorität, Zuordnung und
  Zeitstempeln;
- **case_entries** -- Einzelposten oder Protokolleinträge je Vorgang;
- **audit_log** -- revisionssicheres Protokoll aller Änderungen;
- **reports_cache** -- materialisierte Auswertungsergebnisse (optional).

Die Beziehungen sind überwiegend klassisch: Ein Benutzer gehört zu
genau einer Organisationseinheit; ein Vorgang hat genau eine
verantwortliche Person und mehrere Einträge; jeder Änderungsschritt ist
einem Vorgang und einem Benutzer zugeordnet.

## Modellierungsentscheidungen

### Status als Aufzählung

Vorgangsstatus werden als PostgreSQL-`ENUM` abgebildet. Dadurch werden
ungültige Zustände bereits durch die Datenbank ausgeschlossen und der
Gültigkeitsbereich bleibt im Schema selbst dokumentiert.

### Zeitstempel und Historie

Jeder Vorgang trägt Erzeugungs- und Änderungszeitstempel. Für eine
vollständige Historie reicht das nicht aus -- deshalb ergänzt die
`audit_log`-Tabelle jede Änderung um Zeitpunkt, auslösende Person und Art
der Änderung.

### Referenzielle Integrität und Löschverhalten

Fremdschlüssel verwenden überwiegend `ON DELETE RESTRICT`, damit
Referenzobjekte nicht versehentlich verschwinden. Vorgänge werden nicht
physisch gelöscht, sondern über einen Status *storniert*, um
Revisionssicherheit zu gewährleisten.

### Indizierung

Häufig abgefragte Spalten (Status, Sachbearbeiter:in, Zeitstempel)
werden indiziert. Auswertungen nutzen gezielt zusammengesetzte Indizes,
um auch bei wachsenden Datenmengen performant zu bleiben.

## Datenbanksicherheit

- Passwörter werden nicht in der Datenbank, sondern nur als Hash
  gespeichert (durch das Backend);
- Zugangsdaten liegen in Umgebungsvariablen, nicht im Code;
- Rollen in PostgreSQL beschränken die Rechte der Anwendung auf das
  nötige Maß;
- Backups werden regelmäßig und verschlüsselt erstellt.

## Migrationskonzept

Schemänderungen werden als versionierte Migrationsskripte gepflegt,
die in definierten Schritten vorwärts und rückwärts ausgeführt werden
können. Dadurch bleibt das Schema nachvollziehbar und in jeder Umgebung
reproduzierbar.

## Benennungs- und Stilkonventionen

Ein konsistentes Schema ist leichter zu lesen und zu pflegen. Für
BIS-Ares wurden Festlegungen getroffen: Tabellennamen im Plural und in
Kleinbuchstaben (`users`, `cases`), Spalten in `snake_case`,
Primärschlüssel durchgehend `id`, Fremdschlüssel benannt nach
referenzierter Tabelle plus `_id` (`assignee_id`). Zeitstempel tragen die
Endung `_at` und verwenden den Typ `TIMESTAMPTZ`. Solche Konventionen
wirken pedantisch, verhindern aber später eine Vielzahl von Missverständnissen.

## Datenmenge und Wachstum

Auch ein Prototyp sollte auf Wachstum ausgelegt sein. Abschätzbar große
Tabellen -- etwa `case_entries` und `audit_log` -- werden so angelegt,
dass sie später partitioniert werden können. Für Auswertungen werden
materialisierte Sichten vorgehalten, die mit wachsender Datenmenge nicht
linear teurer werden. Backups werden unabhängig von der Größe
regelmäßig und verschlüsselt erstellt.

## Testdaten und Datenhygiene

Für Entwicklung und Tests werden realitätsnahe, aber fingierte
Datensätze erzeugt, die keine echten Personen abbilden. Ein Skript
füllt die Testdatenbanken reproduzierbar, sodass alle drei Teilbereiche
gegen denselben Ausgangszustand arbeiten. Veraltete oder
inkonsistente Testdaten werden regelmäßig bereinigt, um
Fehlinterpretationen während der Entwicklung zu vermeiden.

## Bewertung und Entscheidungsalternativen

Der relationale Ansatz mit PostgreSQL stand zur Debatte gegen
dokumentenorientierte Alternativen wie MongoDB. Für BIS-Ares fiel die
Entscheidung zugunsten des relationalen Modells, weil die Daten stark
strukturiert und über Beziehungen verknüpft sind, referenzielle
Integrität unverzichtbar ist und Auswertungen mit Joins und
Aggregationen gut abbildbar sein müssen. Ein dokumentenorientiertes
Modell hätte hier vor allem Nachteile gebracht. Die Entscheidung ist im
Pflichtenheft dokumentiert und mit dem Backend-Teil abgestimmt.

## Erweiterbarkeit

Das Modell ist so entworfen, dass es wächst, ohne gebrochen zu werden.
Neue Vorgangstypen lassen sich anhand zusätzlicher Tabellen oder
konfigurativer Attribute ergänzen, ohne bestehende zu verändern. Neue
Rollen können ergänzt werden, weil die Rechteverwaltung an den Rollen
ansetzt, nicht an fest verdrahteten Endpunkten. Statusarten sind als
Aufzählung hinterlegt und lassen sich -- über eine kontrollierte
Migration -- erweitern. Diese Offenheit ist bewusst eingeplant.
