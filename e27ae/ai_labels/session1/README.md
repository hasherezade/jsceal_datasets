# Session 1 — normalized LLM function-name dataset

This directory contains the Session 1 supporting material for the sample
`e27ae65977287bdfb7b0e15fd3603f85`.

The material is intended to make the LLM-assisted naming experiment inspectable:
it provides the complete normalized rename maps and selected View8 function-tree
exports carrying the names proposed by each model.

## Contents

- [`names_greedy_bulk_claude-sonnet-4-6.normalized.csv`](names_greedy_bulk_claude-sonnet-4-6.normalized.csv) — 21,160 headerless mappings generated with Claude Sonnet 4.6.
- [`names_greedy_bulk_gpt54mini.normalized.csv`](names_greedy_bulk_gpt54mini.normalized.csv) — 21,246 headerless mappings generated with GPT-5.4-mini.
- [`trees/`](trees/) — model-specific View8 tree exports organized by capability.

## Reading the mapping CSV files

Each CSV is headerless:

```text
normalized_name_before_model_rename,model_proposed_name
```

The normalized suffix, for example `0x10000be07`, is the stable identity used to
match a function across the two model outputs. The semantic portion of a function
name is a model proposal, not ground truth.

## Reading the tree exports

The `.txt` files are static View8 pseudocode, not recovered executable JavaScript.
Top-level semantic directories describe why a tree was selected. Numeric
subdirectories are View8 split buckets: their names record the number of functions
in that generated subtree and are not semantic categories.

The trees were regenerated from normalized, model-renamed deobfuscated data.
Subtree cardinalities can differ between model-specific outputs or from historical
exports. Cross-model comparisons should therefore use the normalized function
suffix rather than a proposed name or numeric bucket.

## Scope

The reorganized tree collection supports inspection of the original Session 1
naming experiment. The curated Puppeteer workflow under
[`trees/sonnet-4.6/extra_refs/`](trees/sonnet-4.6/extra_refs/) is supplementary
capability evidence added afterward; it is not part of the original 40 split jobs
or the 142-root manual naming assessment.

The rename CSV files are model-output maps. They do not, by themselves, encode a
human ground-truth verdict about whether any proposed name is correct.
