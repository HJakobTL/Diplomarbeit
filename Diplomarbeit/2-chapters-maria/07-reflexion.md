# Reflexion und Ausblick

## Zusammenfassung der Ergebnisse

Es entstand eine mehrschichtige Backend-Anwendung mit authentifizierter,
rollenbasierter REST-API, die Vorgänge des Bürgerservices validiert,
revisionssicher protokolliert und auswertet. Die Schnittstellen zu
Frontend und Datenbank sind durch abgestimmte Verträge und automatisierte
Tests abgesichert.

## Kritische Würdigung

Die Kernfunktionen sind stabil umgesetzt; Einschränkungen bleiben
bestehen: Die Anwendung ist ein Prototyp und noch nicht
betriebsreif. Themen wie Hochverfügbarkeit, Backups, ausfallsichere
Infrastruktur und eine umfassende Sicherheitsprüfung fehlen bewusst,
ebenso ein vollständiges Berechtigungssystem über alle Randfälle hinweg.

## Lessons Learned

- **Verträge vor Implementierung:** Wer die API früh und schriftlich
  abstimmt, vermeidet teure Nacharbeit in allen Schichten.
- **Tests an den Rändern:** Gerade die Übergänge zwischen Frontend,
  Backend und Datenbank sind fehleranfällig und verdienen eigene Tests.
- **Typisierung zahlt sich aus:** TypeScript hat mehrere Fehlerklassen
  früh sichtbar gemacht.
- **Dokumentation ist Teil der Umsetzung:** Eine versionierte API-Doku
  ist kein Nice-to-have, sondern die Grundlage der Teamarbeit.

## Zukünftige Arbeiten

Als sinnvolle Weiterführungen bieten sich an: ein SSO-Anschluss an die
bestehende Verwaltungs-IT, eine Erweiterung um ereignisbasierte
Benachrichtigungen, eine umfassende Penetration-Test-Reihe sowie die
Containerisierung und ein durchgängiges Deployment-Pipeline.

## Rückblick auf den Bearbeitungsprozess

Rückblickend lässt sich festhalten, dass der Zeitaufwand realistisch
geschätzt wurde, sich die Aufwendung aber anders verteilte als geplant:
Unterschätzt wurde der Aufwand für Vertragstests und
Fehlersuchen an den Schnittstellen; unterschätzt wurde auch, wie viel
Disziplin eine saubere Fehlersemantik über alle Endpunkte hinweg
erfordert. Positiv überrascht hat dagegen, wie konsequent die
Typisierung mit TypeScript ganze Fehlerklassen vorzeitig sichtbar
machte und so Nacharbeit sparte. Für künftige Projekte würde ich noch
früher mit Vertragstests beginnen und das Fehlerformat vollständig
durchdenken, bevor die ersten Endpunkte stehen.
