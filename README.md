# General Research + PubMed Pipeline

A production-oriented, multi-source research-paper workflow:
**search -> fulltext download -> structured parse -> evidence extraction -> auditable output**.

## Scope

### In scope
- Multi-source literature retrieval and deduplication
- Fulltext-first evidence extraction for core fields
- PDF/XML parsing into structured artifacts
- Field/cell-level evidence mapping
- Structured missing-reason reporting

### Out of scope
- Abstract-only filling for core fields
- Guess-based values without traceable evidence
- User-facing product UI

## Current Source Coverage

### Source registry (`src/source_registry.yaml`)
- Total sources: `29`
- Literature: `5`
- Practice guidelines: `4`
- Regulatory: `4`
- Institutions: `16`
- Tier S: `9`
- Tier A: `19`
- Tier B: `1`

### Search sources (CLI)
- `arxiv`, `pubmed`, `biorxiv`, `medrxiv`, `google_scholar`, `iacr`, `semantic`, `crossref`

## Workflow Logic (Top-Down)
1. Define task contract (input schema, output schema, acceptance criteria).
2. Lock extraction gates (evidence policy, missing-reason taxonomy).
3. Run multi-source retrieval.
4. Execute fulltext download chain.
5. Parse downloaded artifacts.
6. Extract and normalize evidence per target field.
7. Deliver aligned outputs:
   - Result layer
   - Evidence layer
   - Missing-reason layer
8. Run QC for traceability and gate compliance.

## Key Files
- CLI entrypoint: `src/paper_hub.py`
- Workbook/output builder: `src/workbook_builder.py`
- Source registry: `src/source_registry.yaml`
- Dimension catalog: `src/dimensions_catalog.yaml`
- SOP: `SOP_endpoint_extraction_standard.md`

## GROBID Mirror and Fallback
- Default remote mirror: `https://kermitt2-grobid.hf.space`
- Fallback chain:
  1. Primary URL (argument/env)
  2. `GROBID_BACKUP_URLS`
  3. Default mirror
  4. Local fallback `http://localhost:8070`

Environment variables:
- `GROBID_URL` / `GROBID_REMOTE_URL`
- `GROBID_BACKUP_URLS`
- `GROBID_LOCAL_URL`
- `PDF_SOURCE_URL`

## Quick Start

### 1) Retrieve candidates
```bash
python3 src/paper_hub.py search-multi \
  --query "your research question" \
  --sources pubmed,crossref,semantic
```

### 2) Download fulltext candidates
```bash
python3 src/paper_hub.py download-batch \
  --input-jsonl downloads/candidate_papers.jsonl \
  --output-dir downloads
```

### 3) Parse downloaded artifacts
```bash
python3 src/paper_hub.py parse \
  --mode bioc \
  --input-dir downloads \
  --output downloads/parsed_bioc.jsonl
```

## Upload-Safe Policy

### Tracked
- Code (`*.py`), config (`*.yaml`), core docs (`README.md`, `SOP_*.md`)

### Not tracked
- Papers/cache/output artifacts (`*.pdf`, `downloads/`, `reports/`)
- Assignment files (`*.xlsx`, `*.docx`, `*.ppt`, `*.pptx`)
- Local runtime/cache (`*.log`, `__pycache__/`, `.venv/`, `.codex_mem/`, `.claude/`)
- Embedded third-party repos (`paper-search-mcp/`, `paperscraper/`, `pubmed_parser/`)
