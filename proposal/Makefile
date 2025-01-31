TEX_FILES := $(wildcard *.tex) \
	$(wildcard frontmatter/*.tex) 
PLOTS := 
DEPS := $(TEX_FILES) $(wildcard *.bib) $(wildcard fig/*.png) $(PLOTS)

default: proposal.pdf abstract.txt

proposal.pdf: $(DEPS)
	./latexrun --latex-args='-shell-escape' --bibtex-args=-min-crossrefs=100 -W no-overfull -W no-tabfigures proposal.tex

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

clean:
	./latexrun --clean
	rm -f proposal.pdf
