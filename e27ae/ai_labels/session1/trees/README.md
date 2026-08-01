# Model-renamed View8 trees

This directory contains equivalent capability-oriented tree collections printed
from two separately renamed versions of the same normalized JSCeal deobfuscation.

| Directory | Model | Text exports |
|---|---|---:|
| [`sonnet-4.6/`](sonnet-4.6/) | Claude Sonnet 4.6 | 184 |
| [`gpt-5.4mini/`](gpt-5.4mini/) | GPT-5.4-mini | 181 |

## Comparison rules

1. Match functions by their normalized suffix, such as `0x10000be20`.
2. Treat the semantic function names as model hypotheses.
3. Do not compare numeric directory names as though they were labels. They record
   View8 subtree sizes and may differ when regenerated graphs differ.
4. Read the root export in a semantic directory first, then open numbered buckets
   for split child subtrees.

The Sonnet collection also contains a curated Puppeteer workflow under
[`sonnet-4.6/extra_refs/`](sonnet-4.6/extra_refs/). That material is supplementary
and has no GPT counterpart in this session.
