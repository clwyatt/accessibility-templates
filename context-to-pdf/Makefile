SOURCES=$(wildcard lecture*.tex)
TARGETS=$(SOURCES:.tex=.pdf)

all: $(TARGETS)

%.pdf: %.tex
	context --purgeall $< --result=$@

clean:
	$(RM) $(TARGETS)



