# OpenClaw English Documentation — LaTeX Build Makefile
# Uses xelatex for native Unicode support

MAIN    = openclaw-book-en
LITE    = openclaw-book-en-lite
TEX     = xelatex
FLAGS   = -interaction=nonstopmode -halt-on-error -file-line-error
SOURCES      = $(MAIN).tex $(wildcard chapters/*.tex)
LITE_SOURCES = $(LITE).tex $(wildcard chapters-lite/*.tex)

.PHONY: all pdf clean distclean view watch help lite lite-quick lite-view lite-pdf

# Default target: build PDF
all: pdf

# === Full Edition ===

# Build PDF (twice for correct TOC and cross-references)
pdf: $(MAIN).pdf

$(MAIN).pdf: $(SOURCES)
	$(TEX) $(FLAGS) $(MAIN).tex
	$(TEX) $(FLAGS) $(MAIN).tex

# Quick build (single pass, for draft preview)
quick:
	$(TEX) $(FLAGS) $(MAIN).tex

# Open PDF preview (macOS)
view: pdf
	open $(MAIN).pdf

# === Lite Edition ===

# Build Lite PDF (twice)
lite-pdf: $(LITE).pdf

$(LITE).pdf: $(LITE_SOURCES)
	$(TEX) $(FLAGS) $(LITE).tex
	$(TEX) $(FLAGS) $(LITE).tex

# Lite quick build (single pass)
lite-quick:
	$(TEX) $(FLAGS) $(LITE).tex

# Lite: build and open
lite-view: lite-pdf
	open $(LITE).pdf

# lite alias (shortcut)
lite: lite-pdf

# === Common ===

# Watch for file changes and auto-build (requires fswatch: brew install fswatch)
watch:
	@echo "👀 Watching for file changes... (Ctrl+C to quit)"
	@fswatch -o $(SOURCES) | xargs -n1 -I{} make quick

# Watch lite edition files
lite-watch:
	@echo "👀 Watching lite edition files... (Ctrl+C to quit)"
	@fswatch -o $(LITE_SOURCES) | xargs -n1 -I{} make lite-quick

# Clean auxiliary files
clean:
	rm -f $(MAIN).aux $(MAIN).log $(MAIN).out $(MAIN).toc
	rm -f $(MAIN).fdb_latexmk $(MAIN).fls $(MAIN).synctex.gz
	rm -f $(LITE).aux $(LITE).log $(LITE).out $(LITE).toc
	rm -f $(LITE).fdb_latexmk $(LITE).fls $(LITE).synctex.gz

# Deep clean (including PDF)
distclean: clean
	rm -f $(MAIN).pdf
	rm -f $(LITE).pdf

# Help
help:
	@echo "Available targets:"
	@echo ""
	@echo "  === Full Edition ==="
	@echo "  make          — Build PDF (twice, with TOC)"
	@echo "  make quick    — Quick build (single pass, draft preview)"
	@echo "  make view     — Build and open PDF"
	@echo "  make watch    — Watch for file changes and auto-build"
	@echo ""
	@echo "  === Lite Edition ==="
	@echo "  make lite     — Build Lite PDF (twice, with TOC)"
	@echo "  make lite-quick — Lite quick build (single pass, draft preview)"
	@echo "  make lite-view  — Build Lite and open PDF"
	@echo "  make lite-watch — Watch Lite files and auto-build"
	@echo ""
	@echo "  === Common ==="
	@echo "  make clean    — Clean auxiliary files"
	@echo "  make distclean— Clean all generated files (including PDF)"
	@echo "  make help     — Show this help"
