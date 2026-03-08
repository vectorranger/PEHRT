# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

PEHRT (Pipeline for Electronic Health Record Data Harmonization for Translational Research) is a Quarto-based documentation website that provides a framework for processing EHR data. It contains tutorials, function documentation, and Jupyter notebooks — not a traditional software package.

## Build Commands

```bash
# Render the Quarto website
quarto render

# Preview locally with live reload
quarto preview

# Render a single page
quarto render <file>.qmd
```

The rendered site outputs to `_site/`. Quarto uses `execute: freeze: auto` so code cells are only re-executed when source changes.

## Architecture

- **Quarto website** configured in `_quarto.yml` with cosmo theme
- **Three modules** forming the pipeline:
  - **Module 1 (Data Preprocessing):** Five Jupyter notebooks (`EHR-Pipeline-Part1-5.ipynb`) covering data cleaning, code rollup, NLP, and cohort creation — Python/Pandas
  - **Module 2 (Representation Learning):** `m2.qmd` — SVD-PMI embeddings (R with `nlpembeds` package), PLM-based embeddings (Python with `text_encode.py`), BONMI multi-institution embedding, and validation via AUC
  - **Module 3 (Automated Harmonization):** `m3.qmd` — joint BONMI embedding training and validation combining BONMI + NLP embeddings
- **Function documentation** as `.qmd` files (e.g., `BONMI_function.qmd`, `rollup_function.qmd`, `clean_data_by_batch_function.qmd`)
- **TUTORIAL/** directory contains standalone preprocessing notebooks
- **Dual-language:** R (managed via `renv.lock`, R 4.4.1) and Python (`requirements.txt`: numpy, pandas, jupyter)

## Key R Packages

- `nlpembeds` — co-occurrence matrices, PMI, SVD embeddings
- `kgraph` — knowledge graph fitting and evaluation
- `dplyr` — data manipulation

## Key Python Dependencies

- `torch` — PLM-based embedding generation
- `text_encode.py` — `TextEncoder` class wrapping HuggingFace models (CODER, SapBERT, BioBERT, PubMedBERT)
