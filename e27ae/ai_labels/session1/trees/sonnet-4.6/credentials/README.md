# Credential recovery

Windows credential-recovery components selected for inspection.

Model-specific names in this directory were proposed by **Claude Sonnet 4.6**.
They should be interpreted as hypotheses; the normalized function suffix is the
stable identifier.

This subtree contains **17 text exports**.

## Cross-model counterpart

[`GPT-5.4-mini` version](../../gpt-5.4mini/credentials/)

## Subdirectories

- [`dpapi/`](dpapi/) — DPAPI and master-key recovery logic used to decrypt protected browser material. (8 text exports).
- [`lsa-secrets/`](lsa-secrets/) — LSA secret, boot-key, and NTLM-related recovery logic. (9 text exports).
