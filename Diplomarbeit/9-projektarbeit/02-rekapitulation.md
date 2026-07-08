# Rekapitulation

## Zusammenfassung der Ergebnisse

Das Gesamtprojekt BIS-Ares wurde in den drei Teilbereichen Frontend,
Backend und Datenbank vollständig umgesetzt und zu einer integrierten
Gesamtanwendung zusammengeführt. Die definierten Funktionspunkte --
Anmeldung mit Rollenkonzept, Erfassung und Bearbeitung von Vorgängen,
Dashboard-Übersicht sowie Auswertungen -- liegen als funktionierender
Prototyp vor.

## Reflexion zu Ziel und Ergebnis

Die in Lasten- und Pflichtenheft formulierten Kernziele wurden erreicht.
Einschränkend ist festzuhalten, dass der Funktionsumfang im Rahmen einer
Diplomarbeit auf ein tragfähiges Kernspektrum begrenzt blieb; eine
Produktivsetzung beim Kooperationspartner erfordert noch ergänzende
Themen wie Betriebskonzept, ausfallsichere Infrastruktur und eine
umfassende Penetration-Test-Reihe.

## Reflexion zur Teamarbeit

Die Aufteilung in Frontend, Backend und Datenbank ermöglichte weitgehend
paralleles Arbeiten. Als herausfordernd erwiesen sich -- wie erwartet --
die Schnittstellen: Änderungen am Datenmodell oder an der API wirkten
unmittelbar auf mehrere Teilbereiche. Ein früh abgestimmter, versionierter
API-Vertrag sowie gemeinsame Integrationstests haben hier
entscheidend zur Stabilität beigetragen.

## Lessons Learned

- **API-Verträge früh und verbindlich festlegen** und versioniert
  pflegen.
- **Gemeinsames Glossar** aller Fachbegriffe vermeidet Missverständnisse
  zwischen den Teilbereichen.
- **Integrationstests an den Schnittstellen** frühzeitig einrichten, um
  Regressionen sofort zu erkennen.
- **Regelmäßige, kurze Abstimmungen** (Daily/Weekly) halten das
  Gesamtbild bei verteilten Teilarbeiten konsistent.
