# Reflexion und Ausblick

## Zusammenfassung der Ergebnisse

Es entstand ein normalisiertes, integres relationales Datenmodell für
BIS-Ares mit PostgreSQL, das Benutzer-, Vorgangs- und
Auswertungsanforderungen abdeckt, Änderungen revisionssicher
protokolliert und über ein Migrationskonzept reproduzierbar auslieferbar
ist.

## Kritische Würdigung

Das Modell deckt den Funktionskern zuverlässig ab; Grenzen bleiben
bestehen: Für sehr große Datenmengen wären weitergehende Maßnahmen
wie Partitionierung und Replikation nötig. Auch das Berechtigungssystem
auf Datensatzebene ist im Prototyp nur ansatzweise umgesetzt.

## Lessons Learned

- **Schema ist Vertrag:** Was das Datenmodell nicht sauber vorgibt, muss
  später mühsam in den anderen Schichten korrigiert werden.
- **Trigger statt Vertrauen:** Revisionssicherheit verlässlich in der
  Datenbank zu verankern, ist robuster als jede Anwendungsbibliothek.
- **Migrationen von Anfang an:** Wer Schemänderungen früh versioniert,
  vermeidet das Chaos manuell angepasster Umgebungen.
- **Indizes sind keine Kosmetik:** durchdachte Indizes entscheiden über
  brauchbare Auswertungen.

## Zukünftige Arbeiten

Sinnvolle Weiterentwicklungen sind Partitionierung großer Tabellen,
Replikation für Lesezugriffe, eine feingranulare,
datensatzbasierte Berechtigung (Row-Level Security) sowie der Anschluss
an ein Verzeichnisdienst-basiertes Identity-Management.

## Rückblick auf den Bearbeitungsprozess

Im Rückblick zeigt sich, dass der Zeitaufwand für den reinen
Modellentwurf kleiner ausfiel als erwartet, die Absicherung durch
Trigger, Auditing und Migrationen jedoch deutlich mehr Zeit benötigte.
Unterschätzt hatte ich außerdem, wie eng das Datenmodell mit den
Erwartungen des Backends verwoben ist: Jede Änderung an Feldern oder
Beziehungen wirkte unmittelbar auf API-Verträge und das Frontend zurück.
Positiv überrascht hat, wie konsequent Constraints und Trigger
Fehlerquellen beseitigt haben, lange bevor diese in den anderen Schichten
überhaupt sichtbar werden konnten. Für künftige Projekte würde ich das
Datenmodell noch früher mit allen Beteiligten abstimmen und
konsequenter begleitend dokumentieren.
