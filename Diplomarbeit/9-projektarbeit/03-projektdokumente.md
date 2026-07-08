# Projektdokumente

Die folgenden Projektdokumente wurden im Team erstellt und im
Git-Repository des Gesamtprojekts (Pfad `docs/`, siehe Einleitung)
versioniert. Im Anhang dieses Dokuments sind auszugsweise
Inhalte wiedergegeben.

## Kooperationsvertrag

Zwischen der HTBLVA Wien V, Spengergasse, und dem Magistrat der Stadt
Wien (MA~35) wurde ein Kooperationsvertrag geschlossen, der Gegenstand,
Rechte an den Arbeitsergebnissen, Vertraulichkeit sowie die
Sperrvermerks- bzw. Veröffentlichungsregelungen festlegt.

## Lastenheft

Das Lastenheft beschreibt die Anforderungen aus Auftraggebersicht,
insbesondere:

- Funktionsumfang der Vorgangsverwaltung (Anlegen, Bearbeiten,
  Statuswechsel, Auswertung);
- Benutzerrollen (Sachbearbeitung, Aufsicht, Administration);
- DSGVO-konforme Verarbeitung und Revisionssicherheit;
- nichtfunktionale Anforderungen an Verfügbarkeit, Performance und
  Bedienbarkeit.

## Pflichtenheft

Das Pflichtenheft übersetzt die Anforderungen in eine technische
Umsetzungsbeschreibung: Drei-Schichten-Architektur (Frontend -- Backend
-- Datenbank), REST-Schnittstelle, Authentifizierung über JWT, Datenmodell
in dritter Normalform.

## Detailspezifikation

Die Detailspezifikation enthält die verbindlichen API-Verträge (Endpunkte,
Request/Response-Schemata, Fehlercodes) sowie das vollständige
Datenmodell mit Beziehungen und Kardinalitäten.

## Projektplanung

Geplant wurde in einwöchigen Sprints mit jeweils definierten Zielen,
einem gepflegten Backlog und Meilensteinen: *Kickoff*, *Schnittstellen
abgestimmt*, *Feature-complete*, *Integrationstests*, *Abgabe*.

## Protokolle

Begleitend wurden erstellt: *Minutes of Meeting* der wöchentlichen
Statusrunden, *Statusberichte* sowie dokumentierte *Change Requests* an
den API-Verträgen.

## Zeitschreibung / Begleitprotokoll

Die Arbeitszeiten wurden je Teilbereich und Aufgabe kontinuierlich
erfasst; die Auswertung bildet die Grundlage des
Projekt-Controllings und ist im Git-Repository unter
`docs/zeitschreibung/` hinterlegt.
