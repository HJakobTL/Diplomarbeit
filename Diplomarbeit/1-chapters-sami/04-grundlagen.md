# Grundlagen zu UI/UX-Design, Frontend-Frameworks und Design-Systemen

## Grundlagen von UI/UX-Design
### User Interface (UI)

Das User Interface (UI) beschreibt die sichtbare Oberfläche einer
Anwendung, mit der Benutzer direkt interagieren. Dazu gehören unter
anderem Schaltflächen, Formulare, Menüs, Tabellen, Farben,
Schriftarten und andere grafische Elemente.

Ein gut gestaltetes User Interface hilft dabei, Informationen
übersichtlich darzustellen und die Bedienung einer Anwendung zu
vereinfachen. Benutzer sollen wichtige Funktionen schnell finden
können, ohne lange nach ihnen suchen zu müssen.

Bei der Entwicklung moderner Webanwendungen spielt das UI eine
wichtige Rolle, da es den ersten Eindruck einer Anwendung beeinflusst.
Eine unübersichtliche oder komplizierte Oberfläche kann dazu führen,
dass Benutzer Fehler machen oder die Anwendung nur ungern verwenden.
Das UI-Design folgt bewährten Richtlinien und Prinzipien, die über
Jahrzehnte entwickelt wurden. Jakob Nielsen und Rolf Molich haben zehn
Usability-Heuristiken formuliert, die bis heute Gültigkeit haben
[@molich1990improving; @nielsen1994enhancing]: Sichtbarkeit des
Systemstatus, Übereinstimmung zwischen System und realer Welt,
Benutzerkontrolle und

Freiheit, Konsistenz und Standards, Fehlervermeidung, Wiedererkennung
statt Erinnerung, Flexibilität und Effizienz, ästhetisches und
minimalistisches Design, Hilfe bei Fehlererkennung und -diagnose sowie
Hilfe und Dokumentation.

Im Projekt BIS-Ares wurde daher besonderes Augenmerk auf eine klare
Struktur, ein konsistentes Design und eine einfache Bedienbarkeit
gelegt. Ziel war es, die wichtigsten Funktionen schnell zugänglich zu
machen und die tägliche Arbeit des Bürgerservices zu unterstützen.

### User Experience (UX)

Die User Experience (UX) beschreibt das gesamte Nutzungserlebnis eines
Benutzers während der Verwendung einer Anwendung. Dabei geht es nicht
nur um das Aussehen der Oberfläche, sondern auch darum, wie einfach,
verständlich und effizient die Anwendung verwendet werden kann.

Eine positive User Experience entsteht, wenn Benutzer ihre Aufgaben
ohne Schwierigkeiten erledigen können und die Anwendung logisch
aufgebaut ist. Kurze Wege, verständliche Bezeichnungen und ein
konsistentes Verhalten der Benutzeroberfläche tragen wesentlich dazu
bei. Nach Jakob Nielsen definiert sich Usability durch fünf
Qualitätskomponenten: Erlernbarkeit, Effizienz, Merkbarkeit,
Fehlertoleranz und Zufriedenheit [@nielsen2012usability101]. Die Nielsen Norman Group belegt zudem, dass Investitionen in Usability die
gewünschten Qualitätsmetriken einer Website mehr als verdoppeln können
[@nielsen2012usability101]. Im Web ist Usability eine überlebensnotwendige
Bedingung: Wenn eine Website schwer zu bedienen ist, verlassen die
Nutzer sie. Es gibt kein Benutzerhandbuch für Websites – der erste
Impuls bei Schwierigkeiten ist der Wechsel zu einer Alternative. UX
umfasst jedoch mehr als bloße Usability. Sie bezieht emotionale
Aspekte, Markenwahrnehmung, Vertrauen und die gesamte Customer Journey
mit ein. Methoden wie User Research, Personas, Customer Journey Maps
und Usability-Tests helfen dabei, die Bedürfnisse, Erwartungen und
Schmerzpunkte der Nutzer systematisch zu verstehen und in das Design
einfließen zu lassen [@ixdf_ui].

Für die Entwicklung von BIS-Ares war die User Experience besonders
wichtig, da die Anwendung im Arbeitsalltag eingesetzt werden soll. Die
Benutzer müssen Informationen schnell erfassen, Protokolle erstellen
und relevante Daten finden können. Deshalb wurde versucht, unnötige
Schritte zu vermeiden und die Navigation möglichst einfach zu
gestalten.

### Zusammenhang zwischen UI und UX

User Interface und User Experience stehen in engem Zusammenhang und
beeinflussen sich gegenseitig. Ein modernes und ansprechendes Design
allein reicht nicht aus, wenn die Anwendung schwierig zu bedienen ist.
Gleichzeitig kann eine funktionale Anwendung von Benutzern als
unattraktiv wahrgenommen werden, wenn die Gestaltung veraltet oder
unübersichtlich wirkt.

Aus diesem Grund müssen UI und UX bereits während der Planung
gemeinsam betrachtet werden. Ziel ist es, eine Oberfläche zu
entwickeln, die sowohl optisch ansprechend als auch einfach zu
bedienen ist.

Gutes UI-Design ist „unsichtbar” – es lenkt den Benutzer nicht von
seiner eigentlichen Aufgabe ab, sondern unterstützt ihn dabei, seine
Ziele effizient zu erreichen. Die Wahl der richtigen Farben,
Schriftarten und Abstände trägt wesentlich zur Wahrnehmung der Marke
und zur Vertrauensbildung bei [@ixdf_ui].

Im Rahmen des Projekts BIS-Ares wurden beide Aspekte berücksichtigt.
Die Benutzeroberfläche sollte professionell wirken und gleichzeitig
eine schnelle und fehlerfreie Bedienung ermöglichen.

### Responsive Design

Moderne Webanwendungen werden heute auf unterschiedlichen Geräten
verwendet. Neben klassischen Desktop-Computern greifen viele Benutzer
auch über Tablets oder Smartphones auf Anwendungen zu. Aus diesem
Grund muss eine Benutzeroberfläche flexibel auf verschiedene
Bildschirmgrößen reagieren können.

Dieses Konzept wird als Responsive Design bezeichnet. Ziel ist es,
Inhalte und Bedienelemente so darzustellen, dass sie unabhängig vom
verwendeten Gerät gut lesbar und einfach bedienbar bleiben.

Für die Umsetzung von Responsive Design werden häufig Technologien wie
Flexbox, CSS

Grid und moderne CSS-Frameworks eingesetzt. Im Projekt BIS-Ares wurde
Tailwind CSS verwendet, da es zahlreiche Hilfsklassen für responsive
Layouts bereitstellt und dadurch die Entwicklung vereinfacht.

Bereits während der Planung des Frontends wurde darauf geachtet, dass
wichtige Funktionen auch auf kleineren Bildschirmen problemlos genutzt
werden können. Besonders Formulare und Navigationsbereiche müssen
übersichtlich dargestellt werden, um eine effiziente Nutzung der
Anwendung zu ermöglichen.

### Designprinzipien für Webanwendungen

Bei der Entwicklung moderner Benutzeroberflächen haben sich
verschiedene Designprinzipien etabliert, die die Bedienbarkeit und
Verständlichkeit einer Anwendung verbessern [@nielsen2020heuristics].

Ein wichtiges Prinzip ist die Konsistenz. Gleiche Elemente sollten
innerhalb der gesamten

Anwendung gleich aussehen und sich gleich verhalten. Dadurch können
Benutzer schneller lernen, wie das System funktioniert.

Ein weiteres Prinzip ist die Einfachheit. Benutzer sollten nur die
Informationen sehen, die für die aktuelle Aufgabe relevant sind.
Überladene Oberflächen können die Orientierung erschweren und zu
Fehlern führen.

Auch Feedback spielt eine wichtige Rolle. Nach einer Aktion sollte die
Anwendung dem Benutzer eine Rückmeldung geben, beispielsweise durch
Erfolgsmeldungen, Fehlermeldungen oder visuelle Hervorhebungen.

Darüber hinaus wurde auf eine klare visuelle Hierarchie geachtet.
Wichtige Informationen und Funktionen werden deutlich hervorgehoben,
während weniger wichtige Inhalte im Hintergrund bleiben.

Die Interaction Design Foundation betont die Bedeutung von
Einfachheit, klarer Hierarchie und Lesbarkeit, Konsistenz und
Barrierefreiheit [@ixdf_ui]. Diese
Designprinzipien wurden bei der Entwicklung des Frontends von
BIS-Ares berücksichtigt, um eine möglichst intuitive und
benutzerfreundliche Bedienung zu erreichen.


## Frontend-Frameworks im Vergleich
### Angular

Angular ist ein Frontend-Framework, das für die Entwicklung moderner
Webanwendungen verwendet wird. Es basiert auf TypeScript und bietet
viele Funktionen, die man für größere Anwendungen braucht. Dazu gehören
zum Beispiel Komponenten, Routing, Services, Formulare und die
Kommunikation mit dem Backend.

Ein großer Vorteil von Angular ist die klare Struktur. Die Anwendung
wird in einzelne Komponenten aufgeteilt. Dadurch bleibt der Code
übersichtlicher und einzelne Teile können später leichter geändert oder
erweitert werden.

Für das Projekt BIS-Ares ist diese Struktur wichtig, weil die Anwendung
aus mehreren Bereichen besteht. Dazu gehören zum Beispiel Login,
Dashboard, Navigation und das Protokoll-Formular. Angular hilft dabei,
diese Bereiche sauber voneinander zu trennen.

### React

React ist eine JavaScript-Bibliothek zur Entwicklung von
Benutzeroberflächen. Sie wird häufig für moderne
Single-Page-Applications verwendet. Auch bei React wird die Oberfläche
in einzelne Komponenten aufgeteilt.

Ein Vorteil von React ist die große Flexibilität. Viele Dinge können
frei entschieden werden, zum Beispiel welche Bibliotheken für Routing,
Formulare oder State Management verwendet werden. Dadurch kann React
sehr gut an unterschiedliche Projekte angepasst werden.

Gleichzeitig bedeutet diese Flexibilität aber auch, dass man selbst mehr
Entscheidungen treffen muss. Bei größeren Projekten ist deshalb eine
klare Struktur besonders wichtig. Ohne feste Regeln kann der Code
schnell unübersichtlich werden.

Für BIS-Ares wäre React grundsätzlich möglich gewesen. Da das Projekt
aber mehrere klar getrennte Bereiche wie Login, Dashboard, Navigation
und Protokoll-Formular enthält, war eine stärker vorgegebene Struktur
hilfreicher.

### Vue.js

Vue.js ist ein Frontend-Framework für die Entwicklung von
Weboberflächen. Es ist besonders dafür bekannt, dass der Einstieg
vergleichsweise einfach ist. Die Schreibweise ist klar und viele
Funktionen lassen sich schnell verstehen.

Auch Vue.js arbeitet mit Komponenten. Dadurch können Teile der
Benutzeroberfläche getrennt entwickelt und später wiederverwendet
werden. In sogenannten Single File Components können Struktur, Logik
und Styling gemeinsam organisiert werden.

Ein Vorteil von Vue.js ist, dass es für kleinere und mittlere Projekte
sehr angenehm zu verwenden ist. Für sehr große Anwendungen muss jedoch
besonders darauf geachtet werden, dass die Projektstruktur einheitlich
bleibt.

Für BIS-Ares wäre Vue.js ebenfalls möglich gewesen. Da das Projekt
aber langfristig erweitert werden soll und mehrere Bereiche sauber
getrennt werden müssen, wurde Angular als passendere Lösung gewählt.

### Vergleich und Auswahl

Bei der Auswahl eines Frontend-Frameworks wurden mehrere Kriterien
betrachtet. Wichtig waren vor allem Dokumentation, Wartbarkeit,
Skalierbarkeit, TypeScript-Unterstützung und eine klare
Projektstruktur.

Angular bietet im Vergleich zu React und Vue.js eine sehr feste
Struktur. Das war für BIS-Ares ein Vorteil, weil die Anwendung aus
mehreren Bereichen besteht und später erweitert werden soll. Angular
bringt außerdem viele wichtige Funktionen bereits mit, zum Beispiel
Routing, Formularverarbeitung, Services und HTTP-Kommunikation.

React und Vue.js sind ebenfalls moderne und gute Lösungen. React ist
sehr flexibel, benötigt aber oft zusätzliche Bibliotheken. Vue.js ist
einfacher zu lernen und gut verständlich, gibt aber bei größeren
Projekten weniger feste Strukturen vor.

Für BIS-Ares wurde deshalb Angular gewählt. Die klare Architektur,
die gute Dokumentation und die starke TypeScript-Unterstützung passen
gut zu den Anforderungen des Projekts.


## UI/UX-Muster, Design-Systeme und Best Practices
### UI-Design-Patterns

UI-Design-Patterns sind wiederverwendbare Lösungen für wiederkehrende
Designprobleme. Die Interaction Design Foundation kategorisiert diese
in Navigationsmuster (HamburgerMenü, Breadcrumbs, Tabs), Eingabemuster
(Formulare, Autocomplete, Date Picker), Datenausgabemuster (Tabellen,
Karten, Listen) und Feedbackmuster (Toast-Benachrichtigungen,
Fortschrittsanzeigen, Bestätigungsdialoge) [@ixdf_ui]. UX-Muster wie Progressive Disclosure
(schrittweise Offenlegung von Informationen) und
OnboardingWalkthroughs helfen, komplexe Anwendungen zugänglicher zu
machen. Die Auswahl der richtigen Muster hängt vom jeweiligen Kontext,
der Zielgruppe und der Aufgabenkomplexität ab.

### Kriterien für die Konzeptauswahl

Die Auswahl geeigneter UI/UX-Konzepte sollte auf systematischen
Kriterien basieren. Dazu gehören die Benutzerfreundlichkeit
(Usability-Tests mit der Zielgruppe), die Konsistenz mit bestehenden
Designs und Standards, die Zugänglichkeit (Accessibility gemäß WCAG
2.1) [@w3c2018wcag21], die technische Machbarkeit (insbesondere mit
Angular), die Performance (Ladezeiten, Rendering-Effizienz) und die
Wartbarkeit des resultierenden Codes. Eine gewichtete Bewertung dieser
Kriterien ermöglicht eine objektive Entscheidungsfindung und vermeidet
subjektive Präferenzen.

### Design-Systeme und Fallstudien

Erfolgreiche Unternehmen wie Google (Material Design), Airbnb und
Adobe (Adobe Spectrum) haben umfassende Design-Systeme entwickelt, die
auf jahrelanger Nutzerforschung basieren. Diese Systeme bieten eine
konsistente Designsprache, die sowohl die UI-Konsistenz als auch die
Entwicklungsgeschwindigkeit verbessert. Für Angular-Projekte haben
sich Komponentenbibliotheken wie Angular Material und PrimeNG als Best
Practices etabliert. Sie implementieren die Material
Design-Spezifikation beziehungsweise eine breite Palette von
UI-Komponenten, die out-of-the-box mit Angular harmonieren.

Angular Material ist die offizielle Komponentenbibliothek für Angular
und implementiert Googles Material Design. Sie bietet eine
vollständige Sammlung von UI-Komponenten (Buttons, Cards, Dialoge,
Tabellen, Drawer, Stepper), die nach den Prinzipien der
Zugänglichkeit, Internationalisierung und Performance entwickelt
wurden. PrimeNG ist eine umfangreichere Bibliothek mit über 80
Komponenten und zahlreichen Themen (Themes). Beide Bibliotheken
ermöglichen eine schnelle Entwicklung konsistenter Benutzeroberflächen
und können durch benutzerdefinierte Themes an die Markenidentität
angepasst werden.

### Barrierefreiheit und Performance-Optimierung

Responsive Design stellt sicher, dass die Anwendung auf verschiedenen
Geräten und Bildschirmgrößen optimal dargestellt wird. Angular
unterstützt dies durch die Verwendung von CSS Grid, Flexbox und dem
Angular CDK (Component Dev Kit) für responsive Layouts. Die

Barrierefreiheit (Accessibility, a11y) ist ein zentrales Anliegen: Die
Anwendung muss auch von Menschen mit Behinderungen bedienbar sein.
Angular Material bietet ARIA-Attribute, Tastaturnavigation und
Fokus-Management out-of-the-box. Die Einhaltung der WCAG
2.1Richtlinien (mindestens Stufe AA) [@w3c2018wcag21] ist nicht nur
ethisch geboten, sondern in vielen Ländern auch gesetzlich
vorgeschrieben.

Die Performance einer Angular-Anwendung hat direkten Einfluss auf die
User Experience.

Wichtige Optimierungstechniken umfassen die Change Detection Strategy
auf OnPush (reduziert unnötige Überprüfungen), Lazy Loading von
Modulen (verkürzt die initiale Ladezeit), die Verwendung von trackBy
in ngFor-Schleifen (vermeidet unnötige DOM-Änderungen), die
Optimierung von Bildern und Assets sowie die Implementierung von
virtuellen ScrollingListen für große Datenmengen. Angulars Integration
von Server-Side Rendering (Angular Universal) verbessert sowohl die
initiale Ladezeit als auch die SEO-Performance.
