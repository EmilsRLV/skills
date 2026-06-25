# Spec NNN: <Feature / slice name>

- **Status:** Draft | Accepted | Implemented
- **Author:** <name>
- **Date:** YYYY-MM-DD
- **Domain:** link the relevant `CONTEXT.md` glossary terms and any ADRs that constrain
  this slice (`docs/adr/NNNN-*.md`).
- **Builds on:** prior specs this one depends on (if any).

Numbering: scan the specs directory for the highest number and increment. Sections that
don't apply to a slice can be dropped — but say so, don't silently omit (e.g. "no interface
boundary in this slice").

## 1. Summary

One paragraph: what this slice is and the behaviour it adds. If it needs more than a
paragraph, the slice is probably too big — cut it.

## 2. Goals & non-goals

**Goals** — the specific outcomes this slice must achieve.
**Non-goals** — what it deliberately does *not* do, so scope stays honest. The explicit
*no*s are as valuable as the yeses.

## 3. Assumptions

Constraints taken as given, and any prototype concessions (no auth, single tenant,
last-write-wins, seeded data, etc.). State them so they read as decisions, not oversights.

## 4. Rules

The invariant business rules this slice enforces (timing, validity, permissions). Each
should be phrased so it's checkable. Omit the section if the slice has none. Note any
*non*-rules you deliberately chose not to enforce.

## 5. Data model

The shape of the data this slice reads or writes — the interfaces/types and how they map to
stored data. Mark which collections are read-only vs mutable. If you're *changing* an
existing model, show only the delta and call out what stays the same.

## 6. Interface contract

Only if the slice crosses a boundary (HTTP API, CLI, events, a public function). Specify
each operation: method/name, inputs, success output, and **every rejection case with its
code/error**. Where more than one rejection can apply, define a **deterministic order**.
If there's no boundary, write "No interface boundary in this slice."

## 7. Behaviour

What the user sees and what the system does, step by step. Cover the **empty, loading,
error, and boundary states** — not just the happy path. Note **role/permission differences**
explicitly. If you make a judgement call the reader might dispute, mark it (e.g. "Decision
D1 — flip if your team disagrees; it changes criteria N–M only").

## 8. Acceptance criteria

Numbered. Each statement is **true or false** against the running system — no "should feel
nice". Include the negative/rejection cases, not just the happy path. These define *done*.

1. ...
2. ...

## 9. File map (spec → artifacts)

The files this spec governs — the concrete footprint. Makes the spec reviewable and shows
what an implementation should touch.

```
path/to/file        # what it's responsible for
...
```

## 10. Future slices (parked, not forgotten)

Everything deliberately deferred, so the cut scope is a record rather than a loss. Link the
ADRs that already model the parked work, if any.
