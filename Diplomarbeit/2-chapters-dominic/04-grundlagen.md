# Grundlagen

In diesem Kapitel werden die für das Backend von BIS-Ares wesentlichen
Konzepte und Technologien zusammengefasst.

## Serverseitige Webanwendungen

Eine serverseitige Anwendung übernimmt drei zentrale Aufgaben: Sie nimmt
Anfragen von Clients entgegen, verarbeitet diese unter Einbezug von
Geschäftslogik und Persistenz und liefert Antworten in einem definierten
Format zurück. Im Gegensatz zu statischen Webseiten wird der Inhalt
dynamisch erzeugt und kann Benutzerkontext, Rollen und Datenbankzustand
berücksichtigen.

## Das Client-Server-Modell und Schichtenarchitektur

BIS-Ares folgt einer Drei-Schichten-Architektur:

- **Präsentationsschicht** (Frontend): Darstellung und
  Benutzerinteraktion;
- **Anwendungsschicht** (Backend): Geschäftslogik, Authentifizierung,
  Autorisierung, Validierung;
- **Datenhaltungsschicht** (Datenbank): dauerhaftes, strukturiertes
  Speichern der Daten.

Saubere Schichtentrennung erleichtert Testbarkeit, Austauschbarkeit und
Wartbarkeit -- ein Kriterium, das im öffentlichen Betrieb besonders
relevant ist.

## HTTP und REST

REST (Representational State Transfer) ist ein Architekturstil für
verteilte Systeme, der auf den Standardmethoden von HTTP aufbaut. Die
für BIS-Ares wichtigsten Prinzipien sind:

- **Adressierbarkeit:** Jede Ressource besitzt einen eindeutigen URI, z.\,B.
  `/api/cases/42`.
- **Einheitliche Schnittstelle:** `GET` liest, `POST` legt an, `PATCH`
  ändert, `DELETE` entfernt.
- **Zustandslosigkeit:** Jeder Request enthält alle Informationen zu
  seiner Bearbeitung; der Server speichert keinen Sitzungsstatus
  (Status wird stattdessen über Tokens transportiert).
- **Repräsentationen:** Ressourcen werden üblicherweise als JSON
  ausgetauscht.

REST ist leichtgewichtig, gut skalierbar und mit gängigen Frontend-Frameworks
wie Angular problemlos konsumierbar -- wesentliche Gründe für seine
Wahl in BIS-Ares.

## Node.js und Express

Node.js ist eine Laufzeitumgebung, die JavaScript serverseitig über die
V8-Engine ausführt. Charakteristisch sind ereignisgesteuerte,
nichtblockierende Ein-/Ausgabe und ein großes Modul-Ökosystem über den
Paketmanager *npm*. Für BIS-Ares eignet sich Node.js, weil die gesamte
Webanwendung in einer Sprache (JavaScript/TypeScript) gehalten werden
kann und sich asynchrone Datenbankzugriffe natürlich abbilden lassen.

Express ist ein schlankes Web-Framework auf Node.js. Es stellt
Routing-Middleware, Request/Response-Objekte und eine einfache
Verkettung von Middleware-Funktionen bereit. Middleware ist das zentrale
Erweiterungsprinzip: Jede Anfrage durchläuft eine Kette von Funktionen,
die nacheinander Authentifizierung, Protokollierung, Validierung oder
Fehlerbehandlung übernehmen können.

## Authentifizierung und Autorisierung

Unter *Authentifizierung* versteht man die Prüfung, wer jemand ist;
*Autorisierung* regelt, was diese Person tun darf. Für BIS-Ares wurde
ein tokenbasiertes Verfahren gewählt: Nach erfolgreicher Anmeldung
erhält der Client ein signiertes JSON-Web-Token (JWT), das bei jedem
weiteren Request mitgesendet wird. Die darin enthaltenen *Claims*
ermöglichen ein rollenbasiertes Zugriffskonzept (Sachbearbeitung,
Aufsicht, Administration), ohne dass der Server einen Sitzungsspeicher
pflegen muss.

## Validierung und Sicherheit

Eingaben an der Schnittstelle dürfen niemals ungeprüft vertraut werden.
Das Backend validiert daher jeden Request gegen ein Schema
(Whitelist-Prinzip) und lehnt fehlerhafte Anfragen mit einer
aussagekräftigen Fehlermeldung ab. Darüber hinaus werden Maßnahmen wie
Verschlüsselung des Transports (TLS), Schutz vor gängigen Angriffsmustern
(SQL-Injection, Cross-Site-Scripting, Cross-Site-Request-Forgery) und
rate-Limiting an kritischen Endpunkten berücksichtigt.

## Statuscodes und Fehlersemantik

Sinnvolle HTTP-Statuscodes sind Teil einer verständlichen Schnittstelle.
Für BIS-Ares wurde eine einheitliche Fehlersemantik festgelegt: `200` bei
erfolgreichen Lesezugriffen, `201` nach dem Anlegen einer Ressource,
`204` bei erfolgreichen Änderungen ohne Antwortkörper, `400` bei
fehlerhaften Anfragen, `401` bei fehlender und `403` bei unzureichender
Authentifizierung, `404` für unbekannte Ressourcen, `422` bei inhaltlich
missglückter Validierung und `500` bei unerwarteten Serverfehlern. Jede
Fehlerantwort folgt einem einheitlichen Schema mit einem maschinenlesbaren
Code und einer für Menschen verständlichen Meldung.

## Logging und Beobachtbarkeit

Ein Backend, das nicht verrät, was in ihm vorgeht, lässt sich im Betrieb
kaum warten. Deshalb wird jeder Request mit Methode, Pfad, Status,
Dauer und einer Korrelationskennung protokolliert. Fehler erscheinen
mit Stacktrace in einem separaten Kanal, sensible Daten wie Passwörter
oder Token werden vorher herausgefiltert. Auf diese Weise lassen sich
Probleme nachvollziehen, ohne dass die Datenschutzanforderungen
verletzt werden.

## Asynchrone Verarbeitung

Node.js arbeitet ereignisgesteuert und nichtblockierend. Länger
laufende Operationen -- etwa der Versand von Benachrichtigungen oder der
Aufbau größerer Auswertungen -- werden daher nicht im Request-Kontext
abgearbeitet, sondern in Hintergrundprozesse ausgelagert. Das hält die
Schnittstelle ansprechbar und verhindert, dass ein aufwendiger Job andere
Anfragen blockiert.

## Grundlagen zu TypeScript

Als Programmiersprache kommt TypeScript zum Einsatz, ein Streifzug durch
die wesentlichen Konzepte hilft beim Verständnis der Umsetzung.
TypeScript erweitert JavaScript um eine statische Typisierung: Variablen,
Parameter und Rückgabewerte tragen Typen, die vor der Ausführung geprüft
werden. Daraus entstehen Schnittstellenbeschreibungen (`interface`,
`type`), die im gesamten Backend -- von den Routen bis zu den
Datenbankzugriffen -- als verbindliche Vertragssprache dienen. Wer später
eine Schnittstelle ändert, erhält sofort an allen betroffenen Stellen
Hinweise; das reduziert eine ganze Klasse von Laufzeitfehlern, die in
reinem JavaScript erst im Betrieb sichtbar würden.

## Verbindung zur Datenbank

Die Verbindung zur PostgreSQL-Datenbank wird über einen
Verbindungspool verwaltet: Statt für jede Anfrage eine neue Verbindung
aufzubauen, hält das Backend einen Vorrat offener Verbindungen vor und
teilt sie zu. Das ist deutlich effizienter, weil der Verbindungsaufbau
teuer ist. Als Zugriffsschicht dient ein objektrelationaler Mapper, der
Datenbankzeilen auf typisierte Objekte abbildet und so die im vorigen
Abschnitt erwähnten Typen über die gesamte Anwendung hinweg konsistent
hält.
