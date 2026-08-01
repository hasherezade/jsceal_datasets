# Local HTTPS interception proxy

Local interception-proxy, routing, certificate, and configuration components.

Model-specific names in this directory were proposed by **Claude Sonnet 4.6**.
They should be interpreted as hypotheses; the normalized function suffix is the
stable identifier.

This subtree contains **97 text exports**.

## Cross-model counterpart

[`GPT-5.4-mini` version](../../gpt-5.4mini/proxy/)

## Subdirectories

- [`certificates/`](certificates/) — Certificate lifecycle used by the local HTTPS interception proxy. (25 text exports).
- [`configuration/`](configuration/) — Host and operating-system proxy configuration. (3 text exports).
- [`entrypoints/`](entrypoints/) — Selected entry points into proxy creation and configuration. (9 text exports).
- [`google/`](google/) — Google- and OAuth-related proxy routes and supporting modules. (13 text exports).
- [`http2/`](http2/) — HTTP/2 proxy agent, connection, authentication, and error handling. (8 text exports).
- [`router/`](router/) — General proxy/router initialization. (3 text exports).
- [`server/`](server/) — Local proxy-server bootstrap, initialization, and startup. (33 text exports).
- [`sessions/`](sessions/) — Session-specific proxy components. (3 text exports).
