FILE ?= papers/sample_note.tex
OUTDIR ?= output

.PHONY: sample note index clean check-tools

check-tools:
	@command -v latexmk >/dev/null 2>&1 || { echo "Missing tool: latexmk"; exit 1; }
	@command -v xelatex >/dev/null 2>&1 || { echo "Missing tool: xelatex"; exit 1; }
	@command -v biber >/dev/null 2>&1 || { echo "Missing tool: biber"; exit 1; }

sample: check-tools
	latexmk -cd -xelatex -interaction=nonstopmode -file-line-error -outdir=../$(OUTDIR) papers/sample_note.tex

note: check-tools
	latexmk -cd -xelatex -interaction=nonstopmode -file-line-error -outdir=../$(OUTDIR) $(FILE)

index: check-tools
	latexmk -cd -xelatex -interaction=nonstopmode -file-line-error -outdir=../$(OUTDIR) indexes/reading_index.tex

clean: check-tools
	latexmk -cd -c -outdir=../$(OUTDIR) $(FILE)
