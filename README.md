# Pubmed-max

**Content-first PubMed-centric medical retrieval and evidence synthesis pipeline.**

The product goal is simple: **increase core medical evidence density with full traceability**.

## Core data status (2026-02-09)

| Task | Core non-empty values | Core possible values | Coverage |
|---|---:|---:|---:|
| Task 1 (Survival endpoints) | 64 | 128 | 50.00% |
| Task 2 (Tumor control endpoints) | 43 | 176 | 24.43% |
| Task 3 (Safety/QoL endpoints) | 56 | 112 | 50.00% |

## Delta vs previous release

| Metric | Delta |
|---|---:|
| Task 1 core non-empty values | 0 |
| Task 2 core non-empty values | 0 |
| Task 3 core non-empty values | 0 |

This means the latest release improved runtime robustness and publication quality, but **did not increase core data values**.

## What this repository includes

- `src/paper_hub.py` - unified retrieval, source routing, quality scoring, audit output
- `src/workbook_builder.py` - workbook generation with review-oriented formatting
- `src/dimensions_catalog.yaml` - dynamic dimension registry
- `src/source_registry.yaml` - source reliability and institution registry
- `reports/CORE_DATA_STATUS_2026-02-09.md` - content-first KPI snapshot
- `reports/COMPARISON_2026-02-09.md` - engine/path comparison
- `examples/` - workbook and audit examples

## Product principles

1. Content metrics are primary KPIs.
2. Every value must be traceable to evidence.
3. Quality gate should never be lowered for easier fill rates.
4. Reliability improvements are necessary, but not counted as core content progress.

## Current focus

- Increase Task 2 and Task 3 core coverage with high-grade evidence.
- Keep evidence mapping and auditability at 100%.
