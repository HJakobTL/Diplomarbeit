# Diplomarbeit BIS-Ares — Gesamtprojekt (Gemeinschaftswerk)
# Reihenfolge: Vorspann · 3 Individualeile · Projektarbeit

FRONT     := $(sort $(wildcard 0-frontmatter/*.md))
TEIL1     := $(sort $(wildcard 1-chapters-alex/*.md))
TEIL2     := $(sort $(wildcard 2-chapters-dominic/*.md))
TEIL3     := $(sort $(wildcard 3-chapters-jakob/*.md))
TEIL4     := $(sort $(wildcard 3-chapters-rodion/*.md))
TEAM      := $(sort $(wildcard 9-projektarbeit/*.md))
CHAPTERS  := $(FRONT) $(TEIL1) $(TEIL2) $(TEIL3) $(TEIL4) $(TEAM)
ASSETS    := $(wildcard assets/*)

OUTPUT    := Diplomarbeit_Better_City.pdf
TEX       := $(OUTPUT:.pdf=.tex)
PANDOC    := pandoc

.PHONY: all clean

all: $(OUTPUT)

$(TEX): $(CHAPTERS) project.yaml references.bib template.latex iso690-author-date-de.csl
	$(PANDOC) $(CHAPTERS) \
		--metadata-file=project.yaml \
		--template=template.latex \
		--bibliography=references.bib \
		--csl=iso690-author-date-de.csl \
		--citeproc \
		--number-sections \
		--top-level-division=chapter \
		--toc-depth=2 \
		-o $@

$(OUTPUT): $(TEX) $(CHAPTERS) $(ASSETS)
	latexmk -xelatex -interaction=nonstopmode -halt-on-error $(TEX)

clean:
	git clean -fdX
