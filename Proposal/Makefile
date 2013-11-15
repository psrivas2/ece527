#
# Generated name of proposal file
#
TARGET=Proposal

# Targets
#
default: pdf

pdf: $(TARGET).pdf

ps:  $(TARGET).ps

dvi: $(TARGET).dvi

html: $(TARGET).html

.PRECIOUS: $(TARGET).dvi $(TARGET).ps $(TARGET).pdf

clean:
	rm -f *.aux *.bbl *.dvi *.lof *.log *.toc *.lot *.blg

veryclean:
	rm -f *.aux *.bbl *.dvi *.lof *.log *.toc *.lot *.blg *.dvi *.ps *.pdf *.html


# Programs and paths
# This makefile assumes pdflatex and bibtex are in your path
# 
BIBTEX   = bibtex
LATEX    = pdflatex
DVIPS    = dvips -tletter
PS2PDF   = ps2pdf
PS2EPS	 = ps2eps
L2H      = latex2html -white -antialias -local_icons -long_titles 1 \
              -show_section_numbers
POPTS     = --shell-escape

# Source files
# 
TEXFILES = ${wildcard *.tex} ${wildcard Tables/*.tbl}
BIBFILES = ${wildcard *.bib}
FIGFILES = ${wildcard Figures/*.eps ${wildcard Figures/*.ps}}

# Commands
# 
%.pdf: %.tex $(TEXFILES) $(FIGFILES) $(BIBFILES)
	-$(RM) -f *.aux
	$(LATEX) $*.tex
	-$(BIBTEX) $*
	$(LATEX) $*.tex
	$(LATEX) $*.tex
	@/bin/echo ""
	@/bin/echo "++++++++++++++++++++++++++++++++++++++++++++++++++++++++++"
	@/bin/echo "               ++++ ANY UNDEFINED REFERENCES ++++"
	-@grep -i undef $(TARGET).log || echo "No undefined references."
	@/bin/echo "                 ++++ ANY EMPTY REFERENCES ++++"
	-@egrep -i -n -e 'cite{ *}' -e 'ref{ *}' $(TEXFILES) $(FIGFILES) || echo "No empty references."
	@/bin/echo "++++++++++++++++++++++++++++++++++++++++++++++++++++++++++"
	@/bin/echo ""

%.eps: %.ps
	$(PS2EPS) -f $<

%.ps: %.dvi
	$(DVIPS) -o $@ $<

%.pdf: %.ps
	$(PS2PDF) $<

%.html: %.tex %.dvi
	${L2H} $*

$(TARGET)-bib.ps: $(TARGET).ps
	psselect 17-99 $(TARGET).ps > $(TARGET)-bib.ps

$(TARGET)-sum.ps: $(TARGET).ps
	psselect 1 $(TARGET).ps > $(TARGET)-sum.ps

$(TARGET)-prop.ps: $(TARGET).ps
	psselect 2-16 $(TARGET).ps > $(TARGET)-prop.ps
