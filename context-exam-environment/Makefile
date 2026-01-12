
# set this to the fulll path if needed
CONTEXT=context

TARGETS = problemset-xx.pdf problemset-xx-solutions.pdf \
          problemset-11.pdf problemset-11-solutions.pdf

all: $(TARGETS)

problemset-xx.pdf: problemset-xx.tex ps-xx.tex exam.tex
	$(CONTEXT) --purgeall $< --result=$@

problemset-xx-solutions.pdf: problemset-xx-solutions.tex ps-xx.tex exam.tex
	$(CONTEXT) --purgeall $< --result=$@

problemset-11.pdf: problemset-11.tex ps-11.tex exam.tex
	$(CONTEXT) --purgeall $< --result=$@

problemset-11-solutions.pdf: problemset-11-solutions.tex ps-11.tex exam.tex
	$(CONTEXT) --purgeall $< --result=$@

clean:
	$(RM) $(TARGETS)


