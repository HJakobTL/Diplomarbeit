# Lösungsansätze: Anforderungsanalyse und Frontend-Konzeption

## Anforderungsanalyse für BIS-Ares
### Projektbeschreibung

BIS-Ares ist eine Webanwendung zur Dokumentation und Auswertung von
Vorgängen des Bürgerservices. Ziel des Projekts ist es, eine zentrale
Plattform bereitzustellen, über die Einsatzdaten strukturiert erfasst,
verwaltet und ausgewertet werden können.

Die Anwendung soll verschiedene Arbeitsabläufe des Bürgerservices
digital unterstützen und dadurch den Verwaltungsaufwand reduzieren.
Gleichzeitig sollen Informationen schneller verfügbar sein und die
Nachvollziehbarkeit von Einsätzen verbessert werden.

Das Gesamtsystem besteht aus einem Frontend, einem Backend sowie einer
Datenbank. Das

Frontend dient als Benutzeroberfläche und ermöglicht die Interaktion
mit dem System. Das Backend verarbeitet die Anfragen und stellt die
Geschäftslogik bereit, während die Datenbank für die Speicherung der
Informationen verantwortlich ist.

Im Rahmen dieser Diplomarbeit liegt der Fokus auf dem Frontend-Bereich
des Systems. Dabei werden die Benutzeroberfläche, die Navigation sowie
die Benutzerfreundlichkeit analysiert und umgesetzt. Ziel ist es, eine
moderne und übersichtliche Weboberfläche zu entwickeln, die den
Arbeitsalltag der Benutzer unterstützt und eine effiziente Bedienung
ermöglicht. Besonderes

Augenmerk wird auf die Login-Seite, das Dashboard sowie das
Protokoll-Formular gelegt, da diese Bereiche zu den wichtigsten
Komponenten des Frontends gehören.

### Benutzergruppen

Damit die Anwendung den Anforderungen der späteren Benutzer
entspricht, müssen die unterschiedlichen Benutzergruppen bereits
während der Entwicklung berücksichtigt werden.

**Sachbearbeiter:innen:** Sachbearbeiter:innen stellen die wichtigste
Benutzergruppe des Systems dar.

Sie erfassen neue Protokolle, dokumentieren Vorfälle und führen
Abfragen durch. Für diese Benutzergruppe steht eine einfache und
effiziente Bedienung im Vordergrund. Die Benutzeroberfläche muss daher
übersichtlich gestaltet sein und einen schnellen Zugriff auf häufig
verwendete Funktionen ermöglichen.

**Sonderermittler:** Sonderermittler arbeiten mit sensiblen
Informationen und benötigen Zugriff auf spezielle Protokolle. Die
Benutzeroberfläche muss bestimmte Inhalte abhängig von der jeweiligen
Rolle darstellen oder ausblenden. Zusätzlich müssen vertrauliche
Informationen klar gekennzeichnet und geschützt werden.

**Administratoren:** Administratoren sind für die Verwaltung von
Benutzern, Rollen und Stammdaten verantwortlich. Sie benötigen
zusätzliche Funktionen zur Administration des Systems. Dazu gehören
unter anderem die Benutzerverwaltung sowie die Pflege von Systemdaten.

Da die einzelnen Benutzergruppen unterschiedliche Aufgaben erfüllen,
muss das Frontend flexibel aufgebaut sein und die jeweiligen
Anforderungen unterstützen.

### Funktionale Anforderungen

Aus den Projektanforderungen ergeben sich verschiedene Funktionen, die
durch das Frontend unterstützt werden müssen.

Zu den wichtigsten Funktionen gehören:

- Anmeldung am System über eine Login-Seite

- Anzeige eines Dashboards nach erfolgreicher Anmeldung

- Erstellung und Bearbeitung von Protokollen

- Eingabe und Validierung von Formulardaten

- Hochladen von Dokumenten

- Such- und Filterfunktionen

- Rollenabhängige Anzeige von Informationen

- Verwaltung von Benutzern und Stammdaten

Das Frontend muss diese Funktionen übersichtlich darstellen und eine
möglichst einfache Bedienung ermöglichen. Benutzer sollen wichtige
Informationen schnell finden und ihre Aufgaben ohne unnötige
Zwischenschritte erledigen können.

### Nichtfunktionale Anforderungen

Neben den funktionalen Anforderungen spielen auch nichtfunktionale
Anforderungen eine wichtige Rolle.

Ein zentraler Aspekt ist die Benutzerfreundlichkeit. Die Anwendung
soll leicht verständlich sein und eine möglichst kurze
Einarbeitungszeit ermöglichen. Darüber hinaus muss das Frontend auf
unterschiedlichen Bildschirmgrößen nutzbar sein und ein konsistentes
Erscheinungsbild bieten.

Ein weiterer wichtiger Faktor ist die Performance. Seiten und
Formulare sollen schnell geladen werden, damit Benutzer ohne
Verzögerungen arbeiten können.

Auch die Wartbarkeit des Systems wurde berücksichtigt. Durch die
Verwendung von Angular und einer komponentenbasierten Architektur
können einzelne Bereiche unabhängig voneinander erweitert oder
angepasst werden.

Zusätzlich muss das Frontend die Sicherheitsanforderungen des
Gesamtsystems unterstützen. Dazu gehören beispielsweise die
rollenabhängige Anzeige von Funktionen sowie die sichere Kommunikation
mit dem Backend.

### Rolle des Frontends im Gesamtsystem

Das Frontend bildet die direkte Schnittstelle zwischen Benutzer und
System. Alle Funktionen von BIS-Ares werden über die
Benutzeroberfläche bereitgestellt und gesteuert.

Während das Backend die Geschäftslogik verarbeitet und die Datenbank
für die Speicherung der Informationen zuständig ist, übernimmt das
Frontend die Darstellung der Daten sowie die Interaktion mit dem
Benutzer.

Eine zentrale Aufgabe des Frontends besteht darin, komplexe
Informationen verständlich darzustellen und Eingaben möglichst einfach
zu gestalten. Besonders bei umfangreichen Formularen und der
Verwaltung großer Datenmengen spielt die Gestaltung der
Benutzeroberfläche eine wichtige Rolle.

Für das Projekt BIS-Ares wurde daher großer Wert auf eine klare
Navigation, eine konsistente Gestaltung und eine benutzerfreundliche
Bedienung gelegt. Dadurch soll sichergestellt werden, dass die
Anwendung im Arbeitsalltag effizient genutzt werden kann.


## Konzeption des Frontends
### Ziele des Frontend-Designs

Vor Beginn der Implementierung wurden verschiedene Ziele für die
Benutzeroberfläche definiert. Die Anwendung sollte nicht nur
funktional sein, sondern auch eine einfache und intuitive Bedienung
ermöglichen.

Da BIS-Ares von unterschiedlichen Benutzergruppen verwendet wird,
musste die Oberfläche übersichtlich gestaltet werden. Benutzer sollen
wichtige Funktionen schnell finden und ihre Aufgaben ohne lange
Einarbeitungszeit erledigen können.

Die wichtigsten Designziele waren:

- übersichtliche Darstellung von Informationen

- einfache Navigation innerhalb der Anwendung

- konsistente Gestaltung aller Seiten

- Unterstützung verschiedener Bildschirmgrößen

- Reduzierung möglicher Benutzereingabenfehler

- moderne und professionelle Optik

Zusätzlich wurde darauf geachtet, dass neue Funktionen später
problemlos erweitert werden können, ohne das bestehende Design
grundlegend verändern zu müssen.

### Informationsarchitektur

Die Informationsarchitektur beschreibt die Struktur und Organisation
der Inhalte innerhalb der Anwendung.

Bei BIS-Ares wurde versucht, die wichtigsten Funktionen logisch zu
gruppieren und leicht erreichbar zu machen. Benutzer sollen jederzeit
erkennen können, in welchem Bereich der Anwendung sie sich befinden.

Die grundlegende Struktur des Frontends besteht aus folgenden
Bereichen:

- Login

- Dashboard

- Protokollverwaltung

- Such- und Abfragefunktionen

- Benutzerverwaltung

• Stammdatenverwaltung

Durch diese Struktur können die einzelnen Funktionen klar voneinander
getrennt werden. Gleichzeitig bleibt die Navigation übersichtlich und
verständlich.

### Navigationskonzept

Ein zentrales Element des Frontends ist die Navigation. Sie ermöglicht
den Wechsel zwischen den verschiedenen Bereichen der Anwendung.

Bei der Planung wurde besonderer Wert auf eine einfache
Benutzerführung gelegt. Häufig verwendete Funktionen sollten mit
möglichst wenigen Klicks erreichbar sein.

Aus diesem Grund wurde eine Sidebar-Navigation gewählt. Diese bietet
mehrere Vorteile:

- schneller Zugriff auf Hauptfunktionen

- gute Übersicht über alle verfügbaren Bereiche

- einfache Erweiterbarkeit

- konsistentes Verhalten auf allen Seiten

Die Navigation dient gleichzeitig als Orientierungshilfe und
unterstützt die Benutzer bei der täglichen Arbeit mit dem System.

### Farb- und Gestaltungskonzept

Für das Frontend wurde ein modernes und professionelles
Erscheinungsbild angestrebt. Die Gestaltung orientiert sich an den
Anforderungen einer behördlichen Anwendung.

Bei der Auswahl der Farben wurde auf gute Lesbarkeit und ausreichende
Kontraste geachtet. Wichtige Informationen sollen schnell erkannt
werden können.

Zusätzlich wurde eine einheitliche Gestaltung aller Komponenten
verfolgt. Formulare, Buttons, Tabellen und Navigationsbereiche
verwenden ähnliche Designmuster, um ein konsistentes Erscheinungsbild
zu gewährleisten.

Eine klare visuelle Hierarchie hilft dabei, wichtige Inhalte
hervorzuheben und die Orientierung innerhalb der Anwendung zu
erleichtern.

### Auswahl der Technologien

Für die Umsetzung des Frontends wurden Angular und Tailwind CSS
ausgewählt. Die Entscheidung für Angular wurde nicht nur aus
technischer Sicht getroffen, sondern auch aufgrund der Anforderungen
des Projekts.

BIS-Ares soll langfristig erweitert werden können. Deshalb war es
wichtig, ein Framework zu verwenden, das eine klare Struktur vorgibt.
Angular arbeitet mit Komponenten, Services und Routing. Dadurch können
einzelne Bereiche der Anwendung getrennt entwickelt und später
leichter angepasst werden.

Ein weiterer wichtiger Punkt war die Dokumentation. Angular besitzt
eine umfangreiche Dokumentation und viele Beispiele. Das erleichtert
die Entwicklung, besonders wenn Probleme auftreten oder neue
Funktionen umgesetzt werden müssen.

Auch die Skalierbarkeit spielte eine Rolle. Da BIS-Ares mehrere
Funktionen wie Login, Dashboard, Protokollverwaltung und später
weitere Verwaltungsbereiche enthält, muss das Frontend gut erweiterbar
sein. Angular eignet sich dafür gut, weil es für größere Anwendungen
entwickelt wurde.

Tailwind CSS wurde für die Gestaltung der Oberfläche verwendet. Damit
können Layouts und Designs schnell umgesetzt werden, ohne viele eigene
CSS-Dateien schreiben zu müssen. Besonders für responsive Oberflächen
ist Tailwind hilfreich, da viele Klassen für unterschiedliche
Bildschirmgrößen bereits vorhanden sind.

Die Kombination aus Angular und Tailwind CSS war für dieses Projekt
passend, weil Angular die technische Struktur liefert und Tailwind CSS
die Gestaltung der Oberfläche vereinfacht.
