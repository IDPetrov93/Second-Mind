# PROJECT STATE

## Current Phase

Phase 1 — Foundation

---

## Current Status

The conceptual foundation of KOS has been established.

Core documents have been created and reviewed.

No implementation has started.

---

## Completed

- README
- Project Constitution (includes former Founding Principles, merged — see ADR-007)
- Vision
- Anti-Goals
- Project Rules
- Concepts
- Knowledge Theory
- Knowledge Model
- Knowledge Lifecycle
- AI Session Protocol
- Smallest processing unit analysis (ADR-004 accepted, ADR-005, ADR-006)
- Claim Extraction formally defined as a lossy transformation (ADR-011 accepted)
- Information Pipeline (INFORMATION_PIPELINE.md) — abstract stage definitions only, not yet walked through a real example
- Traceability (TRACEABILITY.md)

---

## Current Objective

Design how information flows through KOS.

---

## Phase 1 Exit Criteria (ADR-010, Proposed)

Phase 1 is complete when all of the following hold:

- Every concept used in any document is defined in CONCEPTS.md and nowhere contradicted (no repeat of the ADR-006-style drift).
- The Information Processing Pipeline (next task, below) has been walked through manually against at least one real, non-trivial piece of Information end-to-end — not just described abstractly. A clean textbook example does not count.
- Entity Resolution has moved from Proposed (ADR-009) to an accepted approach, or an explicit decision to defer it into Phase 2 has been made and justified.
- Extraction Fidelity (ADR-008) has at least a conceptual definition of how it is produced, even if not how it is computed numerically.
- The Confidence Computation Model gap (see CONCEPTS.md Pending Concepts) has been either resolved or explicitly deferred with a stated reason.

Until these hold, further pure concept-refinement sessions should be treated with suspicion — check this list before opening a new one.

---

## Next Task

INFORMATION_PIPELINE.md already defines the pipeline stages abstractly. What remains is to walk that pipeline manually against at least one real, non-trivial piece of Information end-to-end, per the Phase 1 Exit Criteria — a description on paper is not sufficient. This walkthrough is expected to surface gaps (e.g. Extraction Fidelity, Entity Resolution, Confidence Computation Model) that the abstract version could not.

---

## Open Questions

- How should confidence evolve?
- How should conflicting claims coexist?
- Should knowledge be immutable?
- Should Claims themselves be immutable once created (append-only, with only Confidence changing), or can a Claim be edited? (surfaced by ADR-005)
- Is derived-only Relation confidence (ADR-006) sufficient, or will some relation types need an independent reliability signal?
- How is Entity Resolution actually performed? (ADR-009, open)
- How is Extraction Fidelity actually computed? (ADR-008, open)
- How is a Confidence value actually computed or aggregated? No document defines this.

---

## Known Risks

Premature implementation.

Premature technology selection.

Overengineering.

Indefinite conceptual refinement with no defined stopping point (see Phase 1 Exit Criteria).

---

## Last Updated

2026-07-02 (session 3 — structural cleanup, ADR-007 through ADR-011)
