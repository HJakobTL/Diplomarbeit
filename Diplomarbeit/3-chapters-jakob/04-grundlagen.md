# Grundlagen

Dieses Kapitel fasst die Konzepte zusammen, auf denen das Datenmodell von
BIS-Ares aufbaut.

## Relationale Datenbanken

Eine relationale Datenbank speichert Daten in Tabellen (Relationen), deren
Zeilen einzelne Datensätze und deren Spalten Attribute bilden. Beziehungen
zwischen Tabellen werden über Schlüssel abgebildet. Die Stärke dieses
Modells liegt in seiner mathematischen Fundierung und der Fähigkeit, Daten
widerspruchsfrei und effizient abzufragen.

## Das relationale Modell und Normalisierung

Normalisierung zielt darauf ab, Redundanzen und Anomalien zu vermeiden.
Die wichtigsten Normalformen sind:

- **1NF:** jedes Feld enthält nur atomare Werte;
- **2NF:** jedes Nicht-Schlüssel-Attribut hängt vom gesamten
  Primärschlüssel ab;
- **3NF:** keine transitiven Abhängigkeiten -- jedes Attribut hängt nur
  vom Primärschlüssel ab.

Für BIS-Ares wird mindestens die 3NF angestrebt; an ausgewählten Stellen
wird zugunsten der Performance kontrolliert denormalisiert und
begründet.

## Schlüssel und Beziehungen

Jede Tabelle besitzt einen Primärschlüssel. Beziehungen werden über
Fremdschlüssel realisiert: Eine Spalte verweist auf den Primärschlüssel
einer anderen Tabelle. Dadurch stellt die Datenbank Referenzielle
Integrität sicher -- ein Vorgang kann nicht einer nicht existierenden
Person zugeordnet werden.

## Transaktionen und ACID

Eine Transaktion bündelt mehrere Operationen zu einer Einheit, die
entweder vollständig oder gar nicht ausgeführt wird. Die
ACID-Eigenschaften garantieren:

- **Atomizität:** alles oder nichts;
- **Konsistenz:** die Datenbank bleibt in einem gültigen Zustand;
- **Isolation:** parallele Transaktionen stören sich nicht;
- **Dauerhaftigkeit:** committete Änderungen bleiben erhalten.

Gerade im öffentlichen Betrieb, wo Vorgänge nicht verloren gehen dürfen,
sind diese Eigenschaften unverzichtbar.

## PostgreSQL

PostgreSQL ist ein ausgereiftes, quelloffenes objektrelationales
Datenbanksystem. Für BIS-Ares sprachen:

- strikte Einhaltung von Standards (SQL) und hohe Datenintegrität;
- mächtige Datentypen (z.\,B. Aufzählungen, JSONB);
- Transaktionssicherheit und feingranulare Rechteverwaltung;
- gute Werkzeuge für Backups, Migrationen und Skalierung.

## Datenintegrität und Constraints

Neben Fremdschlüsseln stellt PostgreSQL weitere Integritätsbedingungen
bereit: `NOT NULL`, `UNIQUE`, `CHECK` und `ENUM`. Sie verlagern
Validierung in die Datenbank und schützen so auch vor Fehlern, die das
Backend oder Frontend übersehen hat.

## Indizes und Abfrageperformance

Indizes beschleunigen das Suchen und Sortieren, kosten aber Schreibzeit
und Speicher. PostgreSQL bietet mehrere Indexarten, insbesondere den
Standard-B-Baum-Index für Gleichheits- und Bereichsanfragen sowie
zusammengesetzte Indizes für häufig kombinierte Spalten. Die Kunst
besteht darin, genau dort zu indizieren, wo Abfragen profitieren, und
an anderer Stelle auf überflüssige Indizes zu verzichten. Der
Zugriffsplan (`EXPLAIN`) gibt Aufschluss darüber, ob eine Abfrage
tatsächlich den Index nutzt oder eine teure Volltabelleprüfung
durchführt.

## Sichten und materialisierte Sichten

Sichten (`VIEW`) kapseln wiederkehrende Abfragen hinter einer
benannten, virtuellen Tabelle. Sie erleichtern die Wartung und
ermöglichen eine rollengerechte Sicht auf die Daten. Materialisierte
Sichten (`MATERIALIZED VIEW`) speichern das Ergebnis physisch und sind
deshalb für aufwendige Auswertungen geeignet, die nicht bei jedem Zugriff
neu berechnet werden sollen; sie werden periodisch aktualisiert.

## Datenschutz in der Datenbank

Datenschutz beginnt nicht erst im Frontend. In der Datenbank werden alle schützenswerten Felder gekennzeichnet,
Zugriffsrechte rollenbasiert vergeben und Zugriffe nachvollziehbar
protokolliert. Wo möglich, werden personenbezogene Daten pseudonymisiert
abgelegt; eine Löschung erfolgt nicht durch physisches Entfernen, sondern
im Rahmen der vorgesehenen Aufbewahrungs- und Löschkonzepte.

## ER-Modellierung als Denkhilfe

Bevor eine Tabelle angelegt wird, empfiehlt sich das Denken in
Entität-Beziehung-Modellen (ER). Entitäten sind die Dinge der Wirklichkeit
-- hier Benutzer, Organisationseinheiten, Vorgänge --; Beziehungen
beschreiben, wie sie miteinander verbunden sind. Aus dem ER-Modell
entstehen durch systemisches Übersetzen die Tabellen und
Fremdschlüssel. Der Vorteil des Modells liegt weniger im Ergebnis als im
Prozess: Wer Beziehungen und Kardinalitäten (1:1, 1:n, m:n) bewusst
klärt, erkennt Entwurfsfehler früh und vermeidet spätere, teure
Restrukturierungen.

## SQL -- die Sprache der Datenbank

SQL (Structured Query Language) ist die Standardsprache relationaler
Datenbanken. Sie gliedert sich in DDL (Definition, z.\,B. `CREATE TABLE`),
DML (Manipulation, z.\,B. `INSERT`, `UPDATE`) und Abfragen (`SELECT`).
Für BIS-Ares werden SQL-Kenntnisse an drei Stellen vorausgesetzt: beim
Anlegen des Schemas, beim Formulieren von Auswertungen und beim
Schreiben von Migrationen. PostgreSQL hält sich eng an den Standard und
erweitert ihn um bewährte Zusätze wie `JSONB` und Window-Funktionen.
