# GPT-5.4-mini tree exports

This directory contains View8 pseudocode trees printed from the normalized
deobfuscated sample after applying function names proposed by **GPT-5.4-mini**.

The corresponding complete rename map is
[`names_greedy_bulk_gpt54mini.normalized.csv`](../../names_greedy_bulk_gpt54mini.normalized.csv).

Names are comprehension aids rather than ground truth. Use each function's
normalized `0x100...` suffix as its stable identity.

This model directory contains **181 text exports**.

## Subdirectories

- [`browser/`](browser/) — Browser-related collection, configuration, extension targeting, and automation trees. (29 text exports).
- [`credentials/`](credentials/) — Windows credential-recovery components selected for inspection. (17 text exports).
- [`desktop/`](desktop/) — Desktop-oriented surveillance and collection components. (12 text exports).
- [`exchanges/`](exchanges/) — Selected cryptocurrency-exchange workflows. (11 text exports).
- [`execution/`](execution/) — Program-entry and bootstrap material. (5 text exports).
- [`proxy/`](proxy/) — Local interception-proxy, routing, certificate, and configuration components. (100 text exports).
- [`telegram/`](telegram/) — Telegram data and session collection. (7 text exports).

## Cross-model view

The corresponding Claude Sonnet 4.6 collection is
[`../sonnet-4.6/`](../sonnet-4.6/). Compare functions by normalized suffix.
