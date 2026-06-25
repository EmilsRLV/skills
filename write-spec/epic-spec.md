# Epic NNN: <Feature name>

- **Status:** Planning | In progress | Done
- **Author:** <name>
- **Date:** YYYY-MM-DD
- **Domain:** link the relevant `CONTEXT.md` glossary terms and any ADRs that shape this feature.

> This is an **epic spec** — the map for a feature that's too big for one slice. It is a
> table of contents with a rationale. It does **not** contain data models, interface
> contracts, or acceptance criteria — those live in the child slice specs. If you find
> yourself writing a contract here, it belongs in a slice.

## 1. Summary

One paragraph: the capability this feature delivers and why, at the feature level.

## 2. Goals & non-goals (feature level)

**Goals** — what the whole feature must achieve once all its slices land.
**Non-goals** — what the feature deliberately won't do, even when complete.

## 3. Slices

The vertical slices this feature decomposes into, in build order. One line of intent each
— no contracts, no criteria. Link each to its slice spec once written.

| # | Slice | Delivers | Status | Spec |
|---|-------|----------|--------|------|
| 1 | <name> | <one-line user-visible outcome> | Draft / Accepted / Implemented | [link](./NNNa-slice.md) |
| 2 | … | … | Not started | — |

## 4. Sequencing & dependencies

Why the slices are ordered this way — the hard dependencies ("slice 2 needs the schedule to
be mutable, which slice 1 delivers"). If the ordering reflects a genuine architectural
decision, record the *why* as an ADR and link it here rather than arguing it in full.

## 5. Open questions

Feature-level unknowns not yet pinned to a slice. As each is resolved (via grilling), it
either becomes a slice, folds into one, or is parked.

## 6. Out of scope / later epics

Capability deliberately deferred beyond this feature.
