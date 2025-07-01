# build html from tex file and png figures

SOURCE= $(wildcard *.tex)
TARGET= $(SOURCE:%.tex=%.html)

# depend on all png files
DEPS= $(wildcard *.png)

OPTIONS= -s -t html5 -V lang=en --embed-resources --mathml

all: $(TARGET)

%.html: %.tex $(DEPS) 
	pandoc $(OPTIONS) $< -o $@

clean:
	$(RM) $(TARGET)




