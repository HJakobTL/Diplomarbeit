# Management Summary {.unnumbered .unlisted}

## Zielsetzung und Aufgabenstellung

Das Gesamtprojekt **BIS-Ares** realisiert ein Bürger-Informationssystem
für den Magistrat der Stadt Wien (MA~35). Ausgangslage ist eine
insellastige, teils papiergestützte Vorgangsbearbeitung, die
Medienbrüche, Redundanzen und eine erschwerte Auswertung nach sich
zieht. Ziel ist eine integrierte Webanwendung, mit der
Sachbearbeiter:innen Vorgänge des Bürgerservices durchgängig digital
erfassen, verwalten und auswerten können.

## Fachliches und wirtschaftliches Umfeld

Träger des Projekts ist die MA~35 (Informationstechnik) als Teil des
Magistrats der Stadt Wien. Einsatzumfeld ist der interne
Bürgerservice-Betrieb mit mehreren Benutzerrollen und einer hohen
Anforderung an Verfügbarkeit, Datenschutz (DSGVO) und
Bedienbarkeit. Die Lösung soll langfristig erweiterbar und wartbar
sein.

## Zusammenfassung der Projektergebnisse

Es entstand eine in drei Schichten gegliederte Anwendung:

- **Frontend** (Angular, Tailwind CSS): responsives Designsystem mit
  Login, Dashboard, Sidebar-Navigation und Protokoll-Formular;
- **Backend** (Node.js/Express): REST-API mit Authentifizierung,
  Rollenkonzept und Validierung;
- **Datenbank** (PostgreSQL): normalisiertes, versioniertes
  Datenmodell mit Migrationsskripten.

Die Schnittstellen zwischen den Schichten wurden vertraglich zwischen
den drei Teilbereichen abgestimmt und mit Integrationstests
abgesichert.

## Schlussfolgerungen und Reflexion zur Teamarbeit

Die dreiteilige Aufstellung hat sich bewährt: klare Schnittstellen
erlaubten weitgehend paralleles Arbeiten, erforderten aber eine enge
Abstimmung insbesondere bei Datenmodell und API-Verträgen. Als Lessons
Learned zeichnen sich ab: frühe Festlegung der API-Verträge, durchgängige
Testabdeckung an den Schnittstellen und ein gemeinsames Glossar zur
Vermeidung von Missverständnissen.
