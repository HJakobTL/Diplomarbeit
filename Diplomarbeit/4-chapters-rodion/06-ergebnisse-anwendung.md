# Ergebnisse und Anwendung im Projekt

## Umsetzung des Frontends
### Entwicklungsumgebung und Auswahl von Angular

Für die Entwicklung des Frontends wurde Angular als Framework verwendet.
Die Benutzeroberfläche wurde mit HTML, TypeScript und Tailwind CSS
umgesetzt. Die Entwicklung erfolgte lokal auf einem MacBook mit macOS.

#### Verwendete Werkzeuge

Bei der Umsetzung kamen konkrete Werkzeuge zum Einsatz, die im Folgenden
kurz beschrieben werden:

- **Visual Studio Code** als Editor mit Erweiterungen für Angular,
  TypeScript und Tailwind CSS.
- **Node.js und npm** zur Verwaltung der Abhängigkeiten und zum Starten
  der lokalen Entwicklungsumgebung.
- **Angular CLI** (`ng serve`, `ng build`, `ng generate`) zum Erzeugen
  von Komponenten sowie zum Starten und Bauen der Anwendung.
- **Angular 19** als Framework, ergänzt durch **Angular Router**,
  **Reactive Forms** und den **HttpClient** für die Kommunikation mit
  dem Backend.
- **Tailwind CSS** für ein einheitliches, utility-basiertes Styling.
- **Git** für die Versionsverwaltung und die Zusammenarbeit im Team.
- **Biome** für Linting und Formatierung sowie **Jest** und
  **Playwright** für automatisierte Tests.

Das Frontend-Projekt befand sich im Ordner „frontend“ des
Gesamtprojekts „Diplomprojekt-25-26“. Über die Angular CLI wurde die
Anwendung lokal gestartet und im Browser getestet. Dadurch konnten
Änderungen an Komponenten, Formularen und Layouts direkt überprüft
werden.

#### Begründung der Angular-Auswahl

Die Entscheidung für Angular wurde anhand mehrerer Kriterien getroffen,
die für ein langfristig wartbares Projekt wie BIS-Ares besonders
wichtig sind:

- **Dokumentation:** Angular bietet eine umfangreiche und offizielle
  Dokumentation. Dadurch konnten neue Themen schnell nachgeschlagen und
  einheitlich umgesetzt werden.
- **Skalierbarkeit:** Durch die komponentenbasierte Architektur kann die
  Anwendung schrittweise um neue Bereiche erweitert werden, ohne die
  bestehende Struktur zu verändern.
- **Wartbarkeit:** Die klare Trennung von Vorlage, Logik und Diensten
  erleichtert das spätere Anpassen einzelner Teile und reduziert
  Fehlerquellen.
- **TypeScript-Unterstützung:** Angular basiert vollständig auf
  TypeScript. Die statische Typisierung half, Fehler bereits während der
  Entwicklung zu erkennen.
- **Struktur:** Angular gibt eine feste Projektstruktur mit Modulen,
  Komponenten und Services vor. Diese Vorgaben sorgten für einen
  einheitlichen Aufbau des gesamten Frontends.

Wichtige Funktionen wie Routing, Formularverarbeitung und
HTTP-Kommunikation bringt Angular bereits mit. Dadurch mussten weniger
zusätzliche Bibliotheken eingebunden werden, was die Wartbarkeit
zusätzlich verbesserte.

### Umsetzung der Login-Seite

Die Login-Seite bildet den Einstiegspunkt in das System BIS-Ares.
Benutzer müssen sich zunächst authentifizieren, bevor sie auf die
Funktionen der Anwendung zugreifen können.

Bei der Gestaltung der Login-Seite wurde besonderer Wert auf
Einfachheit und Übersichtlichkeit gelegt. Die Oberfläche enthält
ausschließlich die notwendigen Eingabefelder für Benutzername und
Passwort. Zusätzlich wurden Validierungen implementiert, um fehlerhafte
Eingaben bereits vor dem Absenden des Formulars zu erkennen.

Das folgende Code-Snippet zeigt die zentralen Schritte der
Login-Funktion: Die Anmeldedaten werden an das Backend gesendet, bei
Erfolg im `AuthService` gespeichert und der Benutzer wird
weitergeleitet. Tritt ein Fehler auf, wird eine Fehlermeldung
angezeigt.

```typescript
onSubmit(): void {
  if (this.isLoading) return;
  this.isLoading = true;

  this.http.post<any>(`${environment.authApiUrl}/api/v1/login`, {
    username: this.username.trim(),
    password: this.password
  }).subscribe({
    next: (response) => {
      this.authService.login(response);
      this.router.navigate(['/redirect-home']);
    },
    error: () => {
      this.errorMessage = 'Invalid username or password';
      this.isLoading = false;
    }
  });
}
```

### Umsetzung des Dashboards

Nach erfolgreicher Anmeldung wird der Benutzer zum Dashboard
weitergeleitet. Das Dashboard dient als zentrale Startseite der
Anwendung und bietet einen Überblick über die wichtigsten Kennzahlen.

Bei der Gestaltung wurde darauf geachtet, dass häufig verwendete
Informationen schnell erfassbar sind. Wichtige Kennzahlen werden in
übersichtlichen Karten dargestellt und logisch gruppiert.

Das folgende Code-Snippet zeigt eine solche Kennzahl-Karte. Über die
Grid-Klassen von Tailwind CSS werden mehrere Karten nebeneinander
angeordnet.

```html
<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
  <div class="bg-gray-800 p-6 rounded-xl shadow-lg">
    <h3 class="text-lg font-semibold mb-2">Aktive Benutzer</h3>
    <p class="text-3xl font-bold text-green-400">{{ activeUsers }}</p>
  </div>
</div>
```

### Umsetzung der Sidebar-Navigation

Die Sidebar stellt das wichtigste Navigationselement innerhalb der
Anwendung dar. Über sie können Benutzer zwischen den verschiedenen
Bereichen des Systems wechseln.

Bei der Entwicklung wurde besonderer Wert auf eine intuitive
Benutzerführung gelegt. Alle Hauptfunktionen sind dauerhaft sichtbar
und können mit wenigen Klicks erreicht werden. Zusätzlich kann die
Sidebar bei zukünftigen Erweiterungen problemlos um weitere Menüpunkte
ergänzt werden.

Das folgende Code-Snippet zeigt den grundlegenden Aufbau der Sidebar mit
Navigationspunkten und einem Logout-Button.

```html
<aside class="w-64 bg-gray-800 p-6 flex flex-col justify-between">
  <div>
    <h1 class="text-2xl font-bold mb-8">Ares Dashboard</h1>
    <nav class="space-y-4">
      <a routerLink="/dashboard" class="block hover:text-white">Startseite</a>
      <a routerLink="/berichte" class="block hover:text-white">Berichte</a>
    </nav>
  </div>
  <button (click)="logout()" class="bg-red-600 px-4 py-2 rounded-md">
    Abmelden
  </button>
</aside>
```

### Umsetzung des Protokoll-Formulars

Das Protokoll-Formular stellt eine der wichtigsten Komponenten des
Frontends dar. Über dieses Formular können Einsatzdaten strukturiert
erfasst und gespeichert werden.

Für die Umsetzung wurden die Reactive Forms von Angular verwendet. Die
Eingabefelder wurden logisch gruppiert und Pflichtfelder über
Validatoren gekennzeichnet. Dadurch können fehlerhafte oder
unvollständige Eingaben bereits während der Datenerfassung erkannt
werden.

Das folgende Code-Snippet zeigt die Definition des Formulars mit
Validatoren für die wichtigsten Pflichtfelder.

```typescript
this.protokollForm = this.fb.group({
  klassifizierung: ['ALLGEMEIN', Validators.required],
  vorfallsdatum: ['', Validators.required],
  vorfallszeit: ['', Validators.required],
  kurzBeschreibung: ['', Validators.required]
});
```

Im Template werden die Formularfelder über `formControlName` an das
Formular gebunden. Pflichtfelder werden bei fehlerhafter Eingabe
hervorgehoben und mit einer kurzen Meldung versehen.

```html
<input type="date" formControlName="vorfallsdatum"
       class="block w-full border rounded px-3 py-2" />
<div *ngIf="protokollForm.get('vorfallsdatum')?.touched
            && protokollForm.get('vorfallsdatum')?.invalid"
     class="error-message">
  Vorfallsdatum ist Pflichtfeld
</div>
```

### Responsive Umsetzung

Da die Anwendung auf unterschiedlichen Geräten verwendet werden kann,
wurde bereits während der Entwicklung auf Responsive Design geachtet.
Layout, Navigation und Formulare passen sich automatisch an
verschiedene Bildschirmgrößen an.

Tailwind CSS bietet hierfür Breakpoint-Präfixe wie `md:` oder `lg:`, mit
denen sich Layouts gezielt für größere Bildschirme anpassen lassen. Das
folgende Code-Snippet zeigt ein Raster, das auf kleinen Bildschirmen
einspaltig und auf größeren Bildschirmen mehrspaltig dargestellt wird.

```html
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  <!-- Karten passen sich der Bildschirmgröße an -->
</div>
```

Durch diese responsive Gestaltung bleibt die Anwendung sowohl auf
Desktop-Computern als auch auf Tablets und kleineren Bildschirmen gut
benutzbar und bietet eine konsistente Benutzererfahrung.


## Testen und Evaluation
### Ziel der Testphase

Nach der Umsetzung des Frontends war es notwendig, die entwickelten
Komponenten systematisch zu überprüfen. Ziel der Testphase war es,
sowohl die technische Funktionalität als auch die
Benutzerfreundlichkeit der Oberfläche zu bewerten.

Im Vordergrund stand dabei die Frage, ob die wichtigsten Bereiche des
Frontends – insbesondere Login, Navigation und Protokoll-Formular –
zuverlässig funktionieren und für die Benutzer verständlich aufgebaut
sind. Gleichzeitig sollte überprüft werden, ob Eingaben korrekt
verarbeitet werden und ob mögliche Fehlerfälle sinnvoll behandelt
werden.

Die Testphase diente somit nicht nur der Fehlersuche, sondern auch der
Bewertung, ob die gewählte Gestaltung und Struktur des Frontends im
praktischen Einsatz geeignet ist.

### Funktionale Tests

Im Rahmen der funktionalen Tests wurde überprüft, ob die wichtigsten
Frontend-Funktionen wie vorgesehen arbeiten. Dabei standen vor allem
jene Bereiche im Fokus, die für die tägliche Nutzung des Systems von
zentraler Bedeutung sind.

Zu den getesteten Funktionen gehörten unter anderem:

- Anmeldung über die Login-Seite

- Anzeige des Dashboards nach erfolgreichem Login

- Navigation über die Sidebar

- Eingabe und Validierung im Protokoll-Formular

- Reaktion auf fehlerhafte oder unvollständige Eingaben

Besonders wichtig war dabei die Überprüfung der Login-Funktion. Es
wurde getestet, ob Benutzer mit gültigen Zugangsdaten korrekt
weitergeleitet werden und ob bei falschen Eingaben passende
Fehlermeldungen erscheinen. Ebenso wurde kontrolliert, ob
Pflichtfelder im Protokoll-Formular korrekt validiert werden und ob
der Benutzer auf fehlende Angaben hingewiesen wird.

Durch diese Tests konnte sichergestellt werden, dass die wichtigsten
Frontend-Funktionen technisch stabil umgesetzt wurden.

### Usability und Benutzerfreundlichkeit

Neben den funktionalen Tests spielte auch die Benutzerfreundlichkeit
eine wichtige Rolle. Da

BIS-Ares im Arbeitsalltag verwendet werden soll, muss die Oberfläche
möglichst klar und verständlich aufgebaut sein.

Usability-Tests sind eine grundlegende Methode zur Validierung der
Benutzerfreundlichkeit. Nach Jakob Nielsen reichen bereits fünf
Testnutzer aus, um die wichtigsten Usability-Probleme zu
identifizieren [@nielsen2000fiveusers]. Die Tests sollten iterativ
durchgeführt werden: Testen eines frühen Prototyps, Beheben der
gefundenen Probleme, erneutes Testen. Methoden wie A/B-Testing
erlauben es, verschiedene Designvarianten systematisch zu vergleichen
und die effektivere Lösung zu identifizieren.

Bei der Bewertung der Usability von BIS-Ares wurden insbesondere
folgende Punkte berücksichtigt:

- Sind wichtige Funktionen schnell auffindbar?

- Ist die Navigation logisch aufgebaut?

- Werden Eingaben verständlich beschriftet?

- Sind Fehlermeldungen nachvollziehbar formuliert?

- Ist das Formular übersichtlich gegliedert?

Die Überprüfung zeigte, dass eine klare Struktur im Frontend
wesentlich dazu beiträgt, die Bedienung zu vereinfachen. Besonders bei
Formularen ist es wichtig, dass Benutzer sofort erkennen, welche
Angaben erforderlich sind und welche Informationen optional eingegeben
werden können.

Auch die durchgängige Gestaltung der Benutzeroberfläche wirkte sich
positiv auf die Orientierung aus. Wiederkehrende Elemente wie Buttons,
Eingabefelder und Navigationspunkte wurden konsistent gestaltet,
wodurch sich Benutzer schneller im System zurechtfinden kön-

nen.

### Technische Tests im Frontend

Zusätzlich zur visuellen und funktionalen Überprüfung wurden auch
technische Aspekte des Frontends betrachtet. Dazu gehörte unter
anderem die Kontrolle, ob die Komponenten fehlerfrei geladen werden,
ob Formulare korrekt reagieren und ob die Anwendung auf
unterschiedlichen Bildschirmgrößen nutzbar bleibt.

Angular bietet ein umfassendes Test-Ökosystem. Unit-Tests mit Jasmine
und Karma testen einzelne Komponenten, Services und Pipes isoliert.
Integrationstests prüfen das Zusammenspiel mehrerer Komponenten.
End-to-End-Tests (E2E) mit Cypress oder Playwright simulieren reale
Benutzerinteraktionen und testen die gesamte Anwendung in einem echten
Browser.

Die Code-Qualität wird durch TypeScripts statische Typisierung,
Linting (ESLint) und CodeFormatierung (Prettier) sichergestellt.

Bei der Entwicklung von BIS-Ares wurde darauf geachtet, dass das
Frontend modular aufgebaut ist. Dadurch können einzelne Komponenten
leichter getestet, angepasst und erweitert werden. Dieser Aufbau
erleichtert nicht nur die Entwicklung, sondern auch die spätere
Wartung.

Ein weiterer wichtiger Punkt war die Überprüfung der
Eingabevalidierung. Durch clientseitige

Prüfungen konnten fehlerhafte Eingaben früh erkannt werden, noch bevor
Daten an das Backend übermittelt werden. Dies verbessert sowohl die
Benutzerfreundlichkeit als auch die Datenqualität.

### Bewertung der Ergebnisse

Die Testphase zeigte, dass das Frontend von BIS-Ares die
grundlegenden Anforderungen an Funktionalität, Benutzerfreundlichkeit
und Struktur erfüllt.

Besonders positiv war, dass die wichtigsten Funktionen klar
voneinander getrennt und logisch angeordnet sind. Die Navigation ist
übersichtlich, das Protokoll-Formular ist strukturiert aufgebaut und
die Anwendung unterstützt den Benutzer durch Rückmeldungen bei
fehlerhaften Eingaben.

Aus technischer Sicht erwies sich die Kombination aus Angular und
Tailwind CSS als gut geeignet. Angular ermöglichte einen modularen
Aufbau der Anwendung, während Tailwind CSS die konsistente Gestaltung
der Oberfläche vereinfachte.

Trotzdem zeigte die Evaluation auch, dass einzelne Bereiche in Zukunft
weiter verbessert werden können. Dazu gehören beispielsweise
zusätzliche Optimierungen für mobile Ansichten, weitere Benutzer-Tests
sowie eine noch detailliertere Ausarbeitung einzelner Masken.

### Zusammenfassung

Insgesamt hat die Test- und Evaluationsphase gezeigt, dass das
entwickelte Frontend eine gute Grundlage für die weitere Entwicklung
von BIS-Ares darstellt. Die wichtigsten Funktionen konnten
erfolgreich umgesetzt und überprüft werden.

Die Ergebnisse bestätigen, dass eine frühzeitige Berücksichtigung von
UI- und UX-Prinzipien wesentlich dazu beiträgt, ein
benutzerfreundliches und funktionales Frontend zu entwickeln.
Gleichzeitig wurde deutlich, dass Testing ein wichtiger Bestandteil
des Entwicklungsprozesses ist, um technische Fehler zu erkennen und
die Qualität der Anwendung langfristig zu sichern.
