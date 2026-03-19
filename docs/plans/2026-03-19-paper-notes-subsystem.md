# Paper Notes Subsystem Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add an independent LaTeX paper-notes subsystem for structured reading notes, literature digestion, and proposal-material accumulation.

**Architecture:** Create a self-contained `notes/` workspace at the repository root so the subsystem does not interfere with the thesis and proposal sources. Use a shared LaTeX preamble, one reusable note template, one fully worked sample note, an isolated bibliography database, and a simple `Makefile` for repeatable XeLaTeX and biber compilation.

**Tech Stack:** LaTeX, XeLaTeX, ctex, biblatex with `gb7714-2015`, biber, latexmk

---

### Task 1: Reserve a clean workspace for the note subsystem

**Files:**
- Create: `notes/README_notes.md`
- Create: `notes/templates/preamble.tex`
- Create: `notes/templates/paper_note_template.tex`
- Create: `notes/papers/sample_note.tex`
- Create: `notes/bib/references.bib`
- Create: `notes/figures/README.md`
- Create: `notes/output/.gitkeep`
- Create: `notes/Makefile`

**Step 1: Create the directory tree**

Run: `mkdir -p docs/plans notes/templates notes/papers notes/bib notes/figures notes/output`

**Step 2: Add shared LaTeX infrastructure**

Write a reusable preamble with:
- Chinese and English mixed-typesetting support
- academic page layout
- math, tables, figures, hyperlinks
- `biblatex` + `gb7714-2015`

**Step 3: Add reusable note template**

Write a standalone `.tex` template with:
- editable metadata block
- required note sections
- citation example
- clear comments for repeated use

**Step 4: Add a fully worked sample note**

Write a realistic EEG foundation-model note that includes:
- one formula
- one figure placeholder
- at least one citation
- explicit “对我课题的启发” content

### Task 2: Document usage and maintenance

**Files:**
- Create: `notes/README_notes.md`
- Create: `notes/figures/README.md`
- Create: `notes/Makefile`

**Step 1: Explain directory responsibilities**

Document what each subdirectory stores and which files are meant to be edited directly.

**Step 2: Explain the authoring workflow**

Document:
- which template to copy
- which metadata fields to update first
- how to add BibTeX entries
- how to compile via `latexmk` or manual XeLaTeX + biber

**Step 3: Explain knowledge reuse**

Document how to extract background, method, and motivation text into later proposal or review documents.

### Task 3: Verify the subsystem

**Files:**
- Verify: `notes/papers/sample_note.tex`

**Step 1: Run compilation**

Run: `make -C notes sample`
Expected: `notes/output/sample_note.pdf` generated successfully

**Step 2: Review warnings**

Check for missing files, unresolved citations, or font/package issues that would block typical TeX Live usage.

**Step 3: Record final delivery**

Summarize:
- created files
- rationale for bibliography solution
- exact file to copy for new notes
