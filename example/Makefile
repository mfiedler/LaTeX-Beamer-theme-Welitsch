# Copyright 2013 by Michael Fiedler <michael.fiedler87@gmx.de>
#
# This file may be distributed and/or modified
#
# 1. under the LaTeX Project Public License and/or
# 2. under the GNU Public License.

CONVERT_GRAYSCALE_CMD = gs -sDEVICE=pdfwrite -sColorConversionStrategy=Gray -dProcessColorModel=/DeviceGray -dCompatibilityLevel=1.4 -dNOPAUSE -dAutoRotatePages=/None -dBATCH
LATEXFILES = example.tex
THEMEFILE = beamerthemeWelitsch.sty
IMAGEFILES = welitsch_coat_of_arms.pdf
BIBLIOGRAPHYFILE = literature.bib
PDFOUTPUT = $(LATEXFILES:.tex=.pdf)
PDFOUTPUT_GRAYSCALE = $(PDFOUTPUT:.pdf=.bw.pdf)
ALLPDFOUTPUT = $(PDFOUTPUT) $(PDFOUTPUT_GRAYSCALE)

.PHONY: all clean dist-clean

all: $(PDFOUTPUT) $(PDFOUTPUT_GRAYSCALE)

%.pdf: %.tex
	pdflatex $<
	bibtex $(<:tex=aux)
	pdflatex $<
	pdflatex $<

example.pdf: $(@:.pdf=.tex) $(THEMEFILE) $(BIBLIOGRAPHYFILE) $(IMAGEFILES)

%.bw.pdf: %.pdf
	$(CONVERT_GRAYSCALE_CMD) -sOutputFile=$@ $<

dist-clean: clean
	rm -f $(ALLPDFOUTPUT)

clean:
	rm -f *.snm *.nav *.aux *.bbl *~ *.toc *.out *.blg *.fdb_latexmk *.log
