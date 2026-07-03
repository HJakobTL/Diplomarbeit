# Better City 🏙️

**Smart-City-Plattform für urbane Lösungen**

Ein Diplomprojekt an der HTL Spengergasse (Abteilung für Informatik).

Better City bündelt zukunftsweisende Mobilitäts-, IoT-, Energie- und Lifestyle-Module in einem konsolidierten Ökosystem aus einer Web-Plattform und nativen Mobilanwendungen.

---

## 👥 Projektorganisation & Team

**Diplomarbeitsleiter:** Dominic Schmidinger
**Betreuer:** Georg Graf
**Auftraggeber:** *[Wird nachgereicht / Kommt noch]*

### 🛠️ Entwicklerteam

- Rodion Bal
- Jakob Cezawa
- Alexander Biegl
- Dominic Schmidinger

---

## 🏗️ Systemarchitektur & Technologiestack

Das Projekt ist dreigeteilt, um maximale Performance auf allen Endgeräten sowie eine robuste, zentrale Datenverarbeitung zu gewährleisten.

![Systemarchitektur (Platzhalter)](./assets/architecture.png)

> 📌 *Platzhalter-Diagramm – wird durch finale Architekturgrafik ersetzt.*

### 🌐 Frontend (Website)

- **Framework:** Astro (für schnelle Ladezeiten und optimale SEO-Übersichten)
- **Sprachen:** HTML, CSS, JavaScript / TypeScript

### 📱 Mobile Apps

Um das beste native Nutzungserlebnis und eine nahtlose Hardware-Integration (z. B. Sensoren/Kamera) zu garantieren, verzichten wir auf Cross-Platform-Frameworks:

- **iOS:** Apple Swift (Nativ)
- **Android:** Google Kotlin (Nativ)

### ⚙️ Backend & Datenverarbeitung

- **Kern-Schnittstelle:** Python / Java (Universelles Backend für Up- und Downloads)
- **Datenbank:** SQL (Strukturierte Speicherung von Nutzerdaten, Systemständen und Meldungen)
- **Business Logic:** Integrierte Datenauswertung

---

## 🔑 Kernfunktionalitäten (Plattformübergreifend)

### 1. Authentifizierung & Berechtigungen

Sowohl auf der Website (Astro) als auch in den Apps (iOS & Android) gilt ein einheitliches Berechtigungskonzept mit einer integrierten Login-Page:

- **Gast-Nutzer:** Ein Login ist nicht zwingend erforderlich. Gast-Nutzer können die Plattform uneingeschränkt als Übersicht nutzen.
- **Verifiziertes Hochladen:** Für sensible Aktionen (z. B. das Hochladen von Daten oder Beiträgen) ist eine Verifizierung bzw. ein Login vorgeschaltet, um Missbrauch vorzubeugen.

### 2. 🤖 Intelligente KI-Empfehlungs-Engine (KI API)

Das System verfügt über eine lernende Empfehlungs-Komponente. Über eine externe KI-API merkt sich der Algorithmus die Vorlieben und das Verhalten des Nutzers, um maßgeschneiderte, personalisierte Vorschläge im urbanen Raum anzuzeigen.

---

## 🛠️ Verwendete Sprachen & Technologien im Überblick

| Kategorie | Technologien |
|---|---|
| **Programmiersprachen** | Kotlin (Android), Swift (iOS), Python / Java (Backend) |
| **Web-Technologien** | Astro Framework, HTML, CSS |
| **Datenhaltung** | SQL |

---

## 🚀 Projektablauf & Installation

*(Dieser Bereich wird im Laufe der Entwicklung mit den konkreten Build-Befehlen für Astro, iOS/Android und das Backend befüllt.)*

```bash
# Beispiel für den späteren Start des Web-Frontends
npm install
npm run dev
```
