# build html from tex files and tikz or png figures

# set final output file
TARGET=clw-tutorial.html

# list figure files
DEPS=

OPTIONS= -s --css=style.css -t revealjs -V lang=en -V transition:none --mathml

all: examples $(TARGET)

%.html: %.md style.css $(DEPS) 
	pandoc $(OPTIONS) $< -o $@

examples: mydoc.html mydoc-v2.html mydoc-v3.html mydoc-v4.html
	mkdir -p output
	cp mydoc*.html output

%.html: %.tex
	pandoc -s -t html5 -V lang=en --embed-resources --mathml $< -o $@

clean:
	$(RM) *.html
