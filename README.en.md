# Contract Review Agent

[中文版 → README.md](README.md)

Upload a rental contract; the agent flags risky clauses (deposit
forfeiture, arbitrary rent increases, shifted repair duties, ...),
cites the matching statutory text, and suggests revisions.

> **Status: just started. This README is a roadmap, not a feature list.**
> It is the second learning project after
> [MewCode Lite](https://github.com/yang-cloud-0/mewcode), built step by
> step in the open; the "done" list is updated only when a step lands.

## v0.1 scope (one pipeline, nothing more)

1. **Parse** — read contract text (.txt / pasted text first), split into clauses
2. **Retrieve** — BM25 over a small statute knowledge base (Civil Code
   lease articles, hand-curated at article granularity)
3. **Review** — a 3-node LangGraph flow (parse → retrieve → report);
   the model outputs risks plus quoted statutory text
4. **Citation verification** — programmatically check, character for
   character, that every quoted statute actually appears in the
   retrieval results; unverifiable citations are dropped. This is the
   project's most important step: it stops the model inventing law
5. **Evaluate** — 5 hand-labelled samples first; report recall and
   false positives honestly, no inflated numbers

Explicitly out of scope for v0.1: vector retrieval / RRF / reranking,
interrupt + checkpointer human-in-the-loop, complex PDF/Word layout
parsing, and a web UI. Each is added only when the step before it works
and the evaluation says it is needed.

Stack: Python · LangGraph · BM25 · pytest

License: MIT
