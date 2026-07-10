# Einleitung

## Ausgangslage und Motivation

BIS-Ares löst eine bisher inselbasierte und teils papiergestützte
Vorgangsdokumentation des Bürgerservices ab. Was auf den ersten Blick wie
einfrontendthema wirkt, hängt in Wirklichkeit an einer Frage: Wie und wo
werden die Vorgänge dauerhaft, widerspruchsfrei und nachvollziehbar
gespeichert? Genau diese Frage steht im Zentrum dieser Arbeit.

## Problemstellung

Die Daten müssen unterschiedlichen, teils widersprüchlichen Anforderungen
genügen: Sie sollen schnell abrufbar, dabei aber vollständig und
revisionssicher sein; sie sollen Beziehungen zwischen Personen,
Organisationseinheiten und Vorgängen sauber abbilden; und sie müssen so
strukturiert werden, dass Erweiterungen ohne aufwendige Umbauten möglich
bleiben. Eine schlecht modellierte Datenbank rächt sich spätestens dann,
wenn sich Anforderungen ändern.

## Zielsetzung der Arbeit

Ziel ist der Entwurf und die Implementierung einer relationalen
Datenbank für BIS-Ares mit PostgreSQL. Im Mittelpunkt stehen:

- ein normalisiertes, widerspruchsfreies Datenmodell;
- eine konsistente Abbildung der Benutzer-, Vorgangs- und
  Auswertungsanforderungen;
- Maßnahmen zur Datenintegrität (Constraints, Transaktionen);
- ein Versionskonzept für Schemänderungen (Migrationen);
- ein Audit-Konzept zur revisionssicheren Nachvollziehbarkeit.

## Vorgehensweise

Die Arbeit folgt dem in den Vorgaben vorgesehenen Aufbau: Grundlagen,
Lösungsansätze, Ergebnisse und Anwendung im Projekt sowie Reflexion.
