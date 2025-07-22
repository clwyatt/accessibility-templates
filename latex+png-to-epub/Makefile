# build html from tex file and png figures

SOURCE= $(wildcard *.tex)
TARGET= $(SOURCE:%.tex=%.epub)

# depend on all png files
DEPS= $(wildcard *.png)

OPTIONS= -s -t epub -V lang=en --mathml

all: $(TARGET)

%.epub: %.tex $(DEPS) 
	pandoc $(OPTIONS) $< -o $@

clean:
	$(RM) $(TARGET)




