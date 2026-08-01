# Certificates

Certificate lifecycle used by the local HTTPS interception proxy.

Model-specific names in this directory were proposed by **GPT-5.4-mini**.
They should be interpreted as hypotheses; the normalized function suffix is the
stable identifier.

This subtree contains **25 text exports**.

## Cross-model counterpart

[`Claude Sonnet 4.6` version](../../../sonnet-4.6/proxy/certificates/)

## Subdirectories

- [`addition/`](addition/) — Adding a generated certificate to the proxy's certificate state. (1 text export).
- [`creation/`](creation/) — Certificate construction logic. (9 text exports).
- [`generation/`](generation/) — Key-pair generation used during certificate creation. (3 text exports).
- [`initialization/`](initialization/) — Initialization of certificate and CA-store components. (7 text exports).
- [`installation/`](installation/) — Installation of a certificate into the local trust environment. (2 text exports).
- [`verification/`](verification/) — Checking, refreshing, or ensuring that the required certificate exists. (3 text exports).
