# Diplomarbeit (PDF-Build)

Dieser Ordner erzeugt das PDF der Diplomarbeit als **Gemeinschaftswerk**:
Vorspann (`0-frontmatter/`) · ein Kapitelordner pro Person · gemeinsame
Projektarbeit (`9-projektarbeit/`). Der Build läuft über `make`: Markdown
wird von `pandoc` zu LaTeX übersetzt und von `latexmk`/**XeLaTeX** zum PDF
gesetzt.

> Die hier enthaltenen Projektnamen, Themen, Logos und Texte sind
> **Beispielinhalt**. Jedes Team ersetzt sie durch sein eigenes Projekt
> (siehe Abschnitt [An das eigene Projekt anpassen](#an-das-eigene-projekt-anpassen)).

---

## 1. Empfohlener Weg: mit opencode bauen

Am schnellsten, ohne sich um die Werkzeugkette kümmern zu müssen:

1. Repo holen, zum Beispiel:
   ```bash
   git clone https://github.com/HJakobTL/Diplomarbeit.git
   cd Diplomarbeit/Diplomarbeit
   ```
2. Ein Terminal in genau diesem Ordner öffnen und `opencode` im
   **Build-Modus** starten.
3. Diesen Prompt abschicken:
   > Ich möchte `make` erfolgreich ausführen. Installiere alles Notwendige.

`opencode` installiert die benötigten Werkzeuge, löst fehlende Pakete auf
und iteriert, bis `make` das PDF erzeugt.

---

## 2. Was `make` braucht (Referenz)

Unabhängig vom Weg benötigt der Build:

- **`make`** — steuert den Ablauf über das `Makefile`.
- **`pandoc`** (mit `citeproc`) — Markdown → LaTeX, Zitate, CSL-Stil.
- **`latexmk`** und eine TeX-Distribution **mit XeLaTeX** (z. B. TeX Live,
  MacTeX) — compiliert die `.tex`-Datei zum PDF.
- **KOMA-Script** (`scrreprt`) sowie die Pakete `polyglossia`, `fontspec`,
  `microtype`, `amsmath`, `xcolor`, `graphicx`, `tabularx`, `multirow`,
  `longtable`, `booktabs`, `etoc`, `hyperref`, `scrlayer-scrpage`, `calc`.
- **Schriften:** TeX Gyre Pagella, TeX Gyre Heros, DejaVu Sans Mono
  (alle in einer vollen TeX-Distribution enthalten).

### Manuelle Installation je Betriebssystem

**Windows — WSL (empfohlen).** Unter Windows läuft der Build am besten in
WSL. WSL/Ubuntu einrichten (z. B. `wsl --install`), in VS Code mit der
Erweiterung *Remote - WSL* öffnen, dann **innerhalb des
Linux-Dateisystems** arbeiten (nicht unter `/mnt/c/…` — das ist extrem
langsam). Darin:
```bash
sudo apt update
sudo apt install make pandoc texlive-full latexmk
```
Wer native Windows-TeX möchte, kann stattdessen **MiKTeX** plus `pandoc`
nutzen; WSL bleibt aber der empfohlene Weg.

**macOS.** Ein volles TeX installieren (BasicTeX reicht *nicht*):
```bash
brew install --cask mactex-no-gui
brew install pandoc
```

**Linux (Debian/Ubuntu).**
```bash
sudo apt install make pandoc texlive-full latexmk
```

---

## 3. Bauen

```bash
make           # erzeugt das PDF (Name siehe OUTPUT im Makefile)
make clean     # räumt Build-Artefakte weg (siehe Hinweis unten)
```

- Der Name der Ausgabedatei steht im `Makefile` unter `OUTPUT`.
- `make clean` führt `git clean -fdX` aus und löscht damit **alle** von
  Git ignorierten Dateien — also alle Build-Produkte. Nicht committete,
  aber *nicht* ignorierte Dateien bleiben erhalten.

---

## 4. An das eigene Projekt anpassen

Dies ist eine Vorlage. Ein neues Team passt folgende Stellen an:

### A. Stammdaten — `project.yaml`
Die zentrale Metadaten-Datei, die pandoc und das Template verwenden.
Anpassen: `gesamttitel`, `gesamtuntertitel`, `kooperationspartner`,
`schuljahr`. In der Liste `studenten` pro Person `nr`, `name`, `thema`,
`betreuer` und `klasse` setzen — und die **Anzahl** der Einträge ändern,
falls das Team nicht genau drei Personen umfasst.

### B. PDF-Name überall ändern
Der Ausgabename taucht an mehreren Stellen auf und muss konsistent bleiben:
- `Makefile`: Variable `OUTPUT` und den Kommentar-Header.
- `.gitignore`: die beiden Einträge für die `.tex`- und `.pdf`-Ausgabedatei.
- `template.latex`: `pdftitle` und `pdfauthor` sowie der Kommentar-Header.

### C. Kapitelordner pro Person
Jede Person hat einen eigenen Kapitelordner (`1-chapters-*`,
`2-chapters-*`, …). Ordnernamen an die echten Personen anpassen und
dabei die Variablen `TEIL1`/`TEIL2`/`TEIL3` im `Makefile` mitändern, da
die Ordnernamen dort eingetragen sind (keine automatische Erkennung).
In jedem Ordner zusätzlich das `00-teil.md` anpassen, das die Teil-Seite
setzt: `\part{Teil~I\,--\,<Name>: <Thema>}`.

### D. Inhalte ersetzen
Alle `.md`-Dateien sind Beispieltexte und werden durch die eigenen
Inhalte ersetzt:
- `0-frontmatter/` — Kurzfassung (DE), Abstract (EN), Management Summary.
- Pro Personenordner — Vorwort, Danksagung, Einleitung, Grundlagen,
  Lösungsansätze, Ergebnisse/Anwendung, Reflexion, Literaturverzeichnis,
  Abkürzungen, Anhang.
- `9-projektarbeit/` — Einleitung, Rekapitulation, Projektdokumente,
  Anhang (gemeinsamer Team-Teil).

### E. Quellen — `references.bib`
Eigene Literatur eintragen. Der Zitierstil ist durch
`iso690-author-date-de.csl` vorgegeben und bleibt unverändert.

### F. Nur bei anderer Schule — `template.latex` und `assets/`
Die Farben (`spenred`/`htlblue`), die Kopfzeile (`\ihead{...}`) und die
Logos (`assets/logo-*.png`) sind auf die HTBLVA Wien V, Spengergasse,
zugeschnitten. Wer an einer anderen Schule ist, passt Farben, Kopfzeile
und Logos entsprechend an; an der HTL Spengergasse bleibt alles, wie es ist.

---

## 5. Troubleshooting

- **Fehlendes LaTeX-Paket oder Schrift:** unter TeX Live via
  `tlmgr install <paket>`, unter Debian/Ubuntu über das passende
  `texlive-…`-apt-Paket nachinstallieren, dann `make` erneut aufrufen.
- **WSL langsam / Dateifehler:** sicherstellen, dass der Ordner im
  Linux-Dateisystem liegt (`~/…`) und nicht unter `/mnt/c/`.
- **Abhängigkeiten nicht gefunden:** `make clean`, dann `make`.
  Wenn gar nichts mehr geht, den empfohlenen opencode-Weg (Abschnitt 1)
  nutzen.
