# Einleitung

## Ausgangslage und Motivation

Moderne Webanwendungen werden fast durchgängig als mehrschichtige Systeme
geplant: Eine Benutzeroberfläche kommuniziert über eine Programmierschnittstelle
mit einer serverseitigen Anwendung, die wiederum eine Datenbank anbindet.
Gerade im Umfeld öffentlicher Verwaltungen entstehen dabei besondere
Anforderungen an Sicherheit, Nachvollziehbarkeit und Verfügbarkeit. Eine
halbwegs realistische Anwendung kann daher nicht allein aus einem
ansprechenden Frontend bestehen -- sie braucht ein durchdachtes Backend.

## Problemstellung

Das Gesamtprojekt BIS-Ares löst eine bisher inselbasierte und teils
papiergestützte Vorgangsdokumentation des Bürgerservices ab. Aus Sicht des
Backends bedeutet das: Benutzer müssen authentifiziert und je nach Rolle
autorisiert werden, Vorgänge müssen validiert, gespeichert und
revisionssicher protokolliert werden, und die Schnittstelle zum Frontend
muss stabil, versionierbar und gut testbar sein. Fehler im Backend
wirken unmittelbar auf alle anderen Schichten.

## Zielsetzung der Arbeit

Ziel dieser Arbeit ist die Konzeption und Umsetzung des Backends sowie der
REST-Schnittstelle von BIS-Ares mit Node.js und Express. Im Mittelpunkt
stehen:

- eine klar strukturierte, mehrschichtige Serverarchitektur;
- Authentifizierung über JSON-Web-Token und ein rollenbasiertes
  Zugriffskonzept;
- Validierung und Fehlerbehandlung an der Schnittstelle;
- eine versionierte, dokumentierte REST-API;
- ausreichende Testabdeckung an den Schnittstellen zu Frontend und
  Datenbank.

## Vorgehensweise

Die Arbeit ist in die Phasen *Grundlagen*, *Lösungsansätze*, *Ergebnisse
und Anwendung im Projekt* sowie *Reflexion* gegliedert. Zunächst werden
die technischen Grundlagen geklärt, anschließend werden Anforderungen und
Lösungsansätze entwickelt, danach die konkrete Umsetzung beschrieben und
schließlich die Ergebnisse reflektiert.
