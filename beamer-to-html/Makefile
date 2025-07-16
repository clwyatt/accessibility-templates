# build html from tex files and tikz or png figures

# set final output file
TARGET=lecture2.html

# list figure files
DEPS= testimage.png

OPTIONS= -s --css=style.css -t revealjs -V lang=en  --mathml

.SECONDARY: # prevent removal of intermediate files

all: $(TARGET)

%.pdf: %.tikz
	pdflatex $<

%.svg: %.pdf
	pdf2svg $< $@

%.html: %.tex style.css $(DEPS) 
	pandoc $(OPTIONS) $< -o $@

view: $(TARGET)
	open $<

clean:
	$(RM) *.log *.aux *.pdf

realclean: clean
	$(RM) *.svg *.html




