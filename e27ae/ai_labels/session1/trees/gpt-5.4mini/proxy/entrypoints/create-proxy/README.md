# Create Proxy

Proxy-construction and recursive caller paths.

Model-specific names in this directory were proposed by **GPT-5.4-mini**.
They should be interpreted as hypotheses; the normalized function suffix is the
stable identifier.

This subtree contains **5 text exports**.

## Cross-model counterpart

[`Claude Sonnet 4.6` version](../../../../sonnet-4.6/proxy/entrypoints/create-proxy/)

## Subdirectories

- [`host-routes/`](host-routes/) — Registration of host-oriented routes used by proxy creation. (1 text export).
- [`initialize-recursive-caller/`](initialize-recursive-caller/) — Initialization wrapper for recursive proxy construction. (2 text exports).
- [`recursive-caller/`](recursive-caller/) — Recursive proxy-construction helper. (2 text exports).
