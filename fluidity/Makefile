.PHONY: all clean

# All org files convert to PDF
OBJS := $(patsubst %.org, %.pdf, $(wildcard *.org))

# TeX output and logs
CRAP := $(patsubst %.org, %.pdf, $(wildcard *.org))
CRAP += $(patsubst %.org, %.aux, $(wildcard *.org))
CRAP += $(patsubst %.org, %.log, $(wildcard *.org))
CRAP += $(patsubst %.org, %.out, $(wildcard *.org))
CRAP += $(patsubst %.org, %.toc, $(wildcard *.org))

all: $(OBJS)

clean:
	rm -f $(CRAP)

# Convert the orgs
%.tex: %.org
	emacs --eval '(setq enable-local-variables :all)' \
		$< \
		-f org-export-as-latex \
		-f save-buffers-kill-emacs
%.aux: %.tex
	pdflatex $<

%.bbl: %.aux
	bibtex $<

# Always run twice in case the TOC generation & lastpage complain
%.pdf: %.tex %.bbl
	pdflatex $<
	pdflatex $<

