manuscript = paper
references = $(wildcard *.bib)
latexopt   = -halt-on-error -shell-escape -file-line-error

all: all-via-pdf

all-via-pdf: $(manuscript).tex $(references)
	pdflatex $(latexopt) $<
	bibtex $(manuscript).aux
	pdflatex $(latexopt) $<
	pdflatex $(latexopt) $<

clean:
	rm -f *.pdf *.dvi *.toc *.aux *.out *.log *.bbl *.blg *.log *.spl *~ *.spl *.zip *.acn *.glo *.ist *.epub
