# Instructions and Notes for ConTeXt Exam Environment

## Building

1. Install the latest Context from
https://wiki.contextgarden.net/Introduction/Installation
You can add the bin directory to your path or specify it in the Makefile.

2. The Makefile in this directory demonstrates how to render the pdfs

3. There are two examples, ps-xx (a basic template you can use that shows how the environment works, and ps-11 (a full example showing tikz, circuitikz, external figures, math alignment, etc, taken from my Fall class). The expected_output directory contains the pdfs as they render for me.

## Authoring

The way I set this up is the ps-xx.tex file is where the main markup goes. You can use the solutions mode to selectively render solutions. There are then two "driver" files problemset-xx.tex and problemset-xx-solutions.tex that enable the environment, setup solutions or not, then just includes the ps-xx.tex file. This makes it easy to build the version students get and the solutions for graders, TAs, and eventually students, all at the same time.

## Resources

ConTeXt can take some getting used to. It is more verbose than LaTeX but works esssentially the same. Searching for documentatation can be tricky because of the name (use "ConTeXt" in parens to get more relevent results), and the AI LLMS are hit and miss in being helpful.

The best resource is the ConTeXt Garden Wiki and the manuals linked there, in particularly the "Not So Short Introduction".





