
HTMLOPTIONS= -s -t html -V lang=en --embed-resources --mathml

PDFOPTIONS= -s -t context+tagging --template context.template

DOCXOPTIONS= -t docx -V lang=en --embed-resources

all: lecture2.html lecture2.pdf lecture2.docx

lecture2.html: lecture2.md fig2_1.tikz
	pdflatex fig2_1.tikz
	pdf2svg fig2_1.pdf fig2_1.svg 
	pandoc $(HTMLOPTIONS) --default-image-extension=svg lecture2.md -o lecture2.html

lecture2.pdf: lecture2.md fig2_1.tikz context.template
	pdflatex fig2_1.tikz
	pandoc $(PDFOPTIONS) --default-image-extension=pdf lecture2.md -o lecture2.pdf

lecture2.docx: lecture2.md fig2_1.tikz
	pdflatex fig2_1.tikz
	pdftocairo -png fig2_1.pdf -r 300 -singlefile
	pandoc $(DOCXOPTIONS) --default-image-extension=png lecture2.md -o lecture2.docx

clean:
	$(RM) *.log *.aux *.pdf

realclean: clean
	$(RM) *.png *.svg *.html *.docx




