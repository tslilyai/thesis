PAPER = thesis
TEX = $(wildcard *.tex)
BIB = $(wildcard *.bib)

.PHONY: all clean

$(PAPER).pdf: $(TEX) $(BIB) 
	latexmk -f -pdf -shell-escape $(PAPER)

clean:
	rm -f *.aux *.bbl *.blg *.log *.out $(PAPER).pdf *.bcf *.run* $(PAPER).f*

abstract.txt: frontmatter/abstract.tex
	cat $< | \
		pandoc -o $@ -f latex -t plain --wrap=none

spell:
	@ for i in *.tex */*.tex; do \
	aspell -l en_us --mode=tex \
					  --add-tex-command="citep p" \
					  --add-tex-command="citet p" \
					  --add-tex-command="Cref p" \
					  --add-tex-command="cref p" \
					  --add-tex-command="crefformat pp" \
					  --add-tex-command="tikzstyle p" \
					  --add-tex-command="usetikzlibrary p" \
					  --add-tex-command="definecolor ppp" \
					  --add-tex-command="newcommand pp" \
					  --add-tex-command="PY pp" \
					  --add-tex-command="cc p" \
					  --add-tex-command="figure p" \
					  --add-tex-command="renewcommand pp" \
					  -p ./aspell.words -c $$i; \
	done

%.pdf: %.md
	pandoc $< -o $@
