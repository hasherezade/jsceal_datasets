# Claude Sonnet 4.6 tree exports

This directory contains View8 pseudocode trees printed from the normalized
deobfuscated sample after applying function names proposed by **Claude Sonnet 4.6**.

The corresponding complete rename map is
[`names_greedy_bulk_claude-sonnet-4-6.normalized.csv`](../../names_greedy_bulk_claude-sonnet-4-6.normalized.csv).

Names are comprehension aids rather than ground truth. Use each function's
normalized `0x100...` suffix as its stable identity.

This model directory contains **184 text exports**.

## Subdirectories

- [`browser/`](browser/) — Browser-related collection, configuration, extension targeting, and automation trees. (29 text exports).
- [`credentials/`](credentials/) — Windows credential-recovery components selected for inspection. (17 text exports).
- [`desktop/`](desktop/) — Desktop-oriented surveillance and collection components. (12 text exports).
- [`exchanges/`](exchanges/) — Selected cryptocurrency-exchange workflows. (11 text exports).
- [`execution/`](execution/) — Program-entry and bootstrap material. (5 text exports).
- [`extra_refs/`](extra_refs/) — Supplementary capability evidence added after the original naming experiment. (6 text exports).
- [`proxy/`](proxy/) — Local interception-proxy, routing, certificate, and configuration components. (97 text exports).
- [`telegram/`](telegram/) — Telegram data and session collection. (7 text exports).

## Supplementary material

The [`extra_refs/`](extra_refs/) directory contains a curated Puppeteer
workflow added after the original naming experiment. It must not be counted
as one of the original experiment's split jobs or assessed roots.

## Cross-model view

The corresponding GPT-5.4-mini collection is
[`../gpt-5.4mini/`](../gpt-5.4mini/). Compare functions by normalized suffix.
