---
name: write-spec
description: Write a source-grade, behavior-precise specification for one thin slice of work before building it, then validate the implementation against it. Use when the user wants to spec a feature, write / draft / refine a spec, carve a feature into a buildable slice, define acceptance criteria, decompose a large feature into slices, or check that an implementation matches its spec. Pairs with the grilling / grill-with-docs skills (to elicit the decisions) and domain-modeling (for the glossary and ADRs).
---

# Write Spec

Write the spec first; let the code follow. A source-grade spec is **behavior-oriented**
(*what* the system does, observed from outside — not *how*), **complete on the edges**
(empty, loading, error, boundary states), and pinned by **acceptance criteria that don't get
to vary**. Those criteria are the defense against non-determinism — generated code differs
run to run, but whether it meets each criterion is true or false. Aim for that bar even if you
operate spec-*anchored* (spec kept in sync with code) rather than literal spec-*as-source*.

## When not to use

The discipline earns its keep when **ambiguity is expensive** — a behavior several parts
depend on, a contract others build against, anything handed to an agent or a teammate. For a
**trivial or reversible change** (copy tweak, one-line fix, rename), skip it and write the
code. A spec you write only to delete is the ceremony that makes people resent the practice.

## Process

### 1. Carve a slice — a product is not a spec
Cut **one thin vertical slice** a real user can do a real thing with and that you can finish;
park the rest in *Future slices*. If you can't state it in a sentence, it's too big. The slice
**is** the buildable unit — there's no separate "tasks" doc. Too big for one slice? Don't write
a bigger spec — decompose it (see *Decomposing a big change*).

### 2. Elicit decisions — don't invent them
Every guess is a latent spec bug.
- **List what's locked first.** Read the constraining ADRs, `CONTEXT.md`, `CLAUDE.md`, and
  prior specs; reuse, don't relitigate. Reusing a prior slice's machinery resolves decisions
  for free (reuse "create a session" and its validation, error codes, and edge rules come with
  it). Grill only what's genuinely open.
- **One decision at a time** (`grilling` / `grill-with-docs`), with a recommended answer,
  **foundational first** — data-model shape, ownership, the actor model before the details. A
  late answer that breaks an early one means re-grilling.
- **When a "why" reveals a new capability, make it a decision — don't absorb it.** "They should
  be able to confirm the time works" smuggles in a feature; choose: this slice, or a new parked one?
- As decisions harden: language → `CONTEXT.md`, hard-to-reverse decisions → ADRs in `docs/adr/`
  (both via `domain-modeling`), project-wide guardrails → `CLAUDE.md` (the "constitution"). The
  spec **references** these, never duplicates them; keep implementation choices out of the glossary.

### 3. Write it source-grade
Fill in [spec-template.md](./spec-template.md).
- **Behavior, not implementation** — observable effects ("clicking a row opens its detail"), not
  mechanisms ("use a resolver"). The line is genuinely hard; when a technical detail matters, put
  it in the **interface contract** or an **ADR**, not smuggled into the prose.
- **Cover every state** — empty, loading, error, not-found, locked, role differences.
- **No weasel "or."** "Shown resolved, *or* moved out of the list" is an unmade decision — the
  implementer picks, and it won't register as a gap. Pick one, or promote it to a *Decision*.
- **Pin the contract** — if the slice crosses a boundary (API / CLI / events / public function):
  inputs, outputs, and **every rejection with its code**, in a deterministic order.
- **Map spec → files** — the artifacts it governs, so the footprint is reviewable.

### 4. Acceptance criteria are the heart
Numbered; each **literally true or false** against the running system. Good: "rejects a write to
a past session (409) and mutates nothing." Weak: "past sessions handled correctly." Write the
rejection cases, not just the happy path.

### 5. Validate against the spec
Build, then walk **every criterion** — by running the system, not just reading the code. Where
the implementation **guessed**, that's a **spec bug**: fix the **spec first**, then the code.
Green build + green tests ≠ validated. Some criteria can't be reached end-to-end (the precondition
is itself rejected by the real interface) — validate those at the lowest level you can and **say
so**; don't imply you exercised live what you only unit-tested.

### 6. Watch for ripples
A new field / status / rule reaches *backwards*: a new `status` forces an old view to render it,
a new state forces an old guard to reject it, and it breaks existing **tests and fixtures**. Name
the ripples in the spec instead of discovering them in the code.

## Decomposing a big change

Two altitudes. A **slice spec** ([spec-template.md](./spec-template.md)) is the buildable unit —
model, contract, criteria. An **epic spec** ([epic-spec.md](./epic-spec.md)) is the **map only**:
feature goals, the ordered slice list with dependencies, links to the children — never a slice's
contracts or criteria (that rebuilds the sprawl spec tooling is hated for).

- **1–3 linear slices:** skip the epic; track decomposition in each slice's *Future slices* plus
  a flat `specs/README.md` index.
- **Bigger / branching:** a folder per epic (`OVERVIEW.md` + `004a-….md`, `004b-….md`).

Record a genuine sequencing rationale as an **ADR**; the OVERVIEW points at it.
