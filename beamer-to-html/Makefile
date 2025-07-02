# build html from tex files and tikz or png figures

# set final output file
TARGET=lecture2.html

# list figure svg files
DEPS=

OPTIONS= -s -t revealjs -V lang=en  --mathml

.SECONDARY: # prevent removal of intermediate files

all: $(TARGET)

%.pdf: %.tikz
	pdflatex $<

%.svg: %.pdf
	pdf2svg $< $@

%.html: %.tex $(DEPS) 
	pandoc $(OPTIONS) $< -o $@

view: $(TARGET)
	open $<

clean:
	$(RM) *.log *.aux *.pdf

realclean: clean
	$(RM) *.svg *.html




