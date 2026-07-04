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
- AI Session Protocol
- Smallest processing unit analysis (ADR-004 accepted, ADR-005, ADR-006)
- Document → Statement → Claim pipeline formalized (ADR-004 rewritten), Claim Extraction defined as lossy transformation (ADR-011)
- Information Pipeline (INFORMATION_PIPELINE.md) — now the single canonical pipeline document; KNOWLEDGE_LIFECYCLE.md retired (ADR-012)
- Traceability (TRACEABILITY.md)
- Information/Document duplication resolved — merged into Document (ADR-013)
- Attribution and Source Primary/Secondary restored after being dropped in a restructuring pass (ADR-014)
- Event anchoring requirement added; Event Resolution named as an open gap (ADR-015, Proposed)
- Citation Fidelity introduced, distinct from Extraction Fidelity and Source trust (ADR-016)
- Attribution Discovery named as unresolved (ADR-017, Proposed)
- Event Resolution scope widened to cover punctual vs. evolving-process Events (ADR-018, Proposed), then fully resolved by anchoring Event identity to Primary Document (ADR-020, Accepted) — superseding ADR-018's framing
- Extraction Fidelity scope clarified to cover entity/subject misattribution (ADR-019, from a fourth walkthrough — Binance/Philippines — that mostly validated prior fixes rather than finding a new hole)
- Relation creation restricted to explicit statement or independent evidence; co-occurrence alone is insufficient (ADR-021, Accepted)
- Validation Strategy and Claim Classification introduced — Claim validation is no longer one-size-fits-all (ADR-022, Accepted; renumbered from a duplicate ADR-011 during a documentation consistency pass — see Known Risks)
- Documentation consistency pass (2026-07-04): fixed a duplicate ADR-011 number (renumbered second instance to ADR-022), corrected ADR-018's status to reflect that ADR-020 supersedes it, promoted ADR-015 to Accepted now that ADR-020 resolves the mechanism it deferred, propagated ADR-021's Relation constraint into CONCEPTS.md and KNOWLEDGE_MODEL.md, defined Claim Classification/Validation Strategy in CONCEPTS.md (used by ADR-022 but never introduced there), and fixed stale/removed filenames in AI_SESSION_PROTOCOL.md's review checklist

---

## Current Objective

Design how information flows through KOS.

---

## Phase 1 Exit Criteria (ADR-010, Proposed)

Phase 1 is complete when all of the following hold:

- Every concept used in any document is defined in CONCEPTS.md and nowhere contradicted (no repeat of the ADR-006-style drift). **Still recurring — this exact drift happened twice more this session (ADR-013's Information/Document duplication, ADR-014's silent Attribution regression). Treat this criterion as failing until a session passes without a new instance.**
- The Information Processing Pipeline has been walked through manually against at least one real, non-trivial piece of Information end-to-end — not just described abstractly. A clean textbook example does not count. **In progress: four walkthroughs done — OpenAI/FT stake report, Jersey Mike's IPO filing, Canada oil pipeline announcement (all 2026-07-03 or 07-02), and Binance/Philippines sandbox approval (2026-07-03). The first three each produced new architecture (ADR-014 through ADR-018); the fourth mostly validated those fixes and needed only a small clarification (ADR-019). That's the first sign of convergence — worth one or two more before treating this criterion as met.**
- Entity Resolution has moved from Proposed (ADR-009) to an accepted approach, or an explicit decision to defer it into Phase 2 has been made and justified. **Still open.** Event Resolution, which joined it as a structurally similar gap, **is now resolved (ADR-020)** — anchored to Primary Document, with one narrower remaining edge case (Independent Multi-Primary Corroboration).
- Extraction Fidelity (ADR-008) has at least a conceptual definition of how it is produced, even if not how it is computed numerically. **Still open.**
- The Confidence Computation Model gap has been either resolved or explicitly deferred with a stated reason. **Still open, and now has an additional hard requirement: it must account for Attribution-linked echoes (ADR-014).**

Until these hold, further pure concept-refinement sessions should be treated with suspicion — check this list before opening a new one.

---

## Next Task

Continue walking INFORMATION_PIPELINE.md manually against further real, non-trivial examples, or resolve another of the remaining open gaps directly (Entity Resolution, Attribution Discovery, Confidence Computation Model, Citation Fidelity Computation Model — Event Resolution is now closed, ADR-020).

---

## Open Questions

- How should confidence evolve?
- How should conflicting claims coexist?
- Should knowledge be immutable?
- Should Claims themselves be immutable once created (append-only, with only Confidence changing), or can a Claim be edited? (surfaced by ADR-005; a real example of a source issuing a post-publication correction was observed during the Jersey Mike's walkthrough — this is not hypothetical)
- Is derived-only Relation confidence (ADR-006) sufficient, or will some relation types need an independent reliability signal?
- How is Entity Resolution actually performed? (ADR-009, open)
- How is Event Resolution actually performed — i.e. when do two claims describe the same real-world Event vs. two distinct ones? **Resolved: anchored to Primary Document (ADR-020).** Remaining narrower question: how should Independent Multi-Primary Corroboration be handled (two independent Primary Sources, no document link, same real occurrence)?
- How is Extraction Fidelity actually computed? (ADR-008, open)
- How is a Confidence value actually computed or aggregated, and how must it discount Attribution-linked echoes? No document defines this. (ADR-014)
- How is Attribution actually discovered/detected, not just recorded? (ADR-017, open)
- How is Citation Fidelity actually measured? (ADR-016, open)

---

### Open Architectural Question

Recent dry-run exercises suggest that some Knowledge Objects represent values that change over time rather than permanent facts.

Examples:

- Percentage of BTC supply in unrealized loss.
- Total BTC holdings of a company.
- Current market capitalization.

It remains undecided whether these should:

- update existing Knowledge Objects;
- create new versions;
- coexist as time-series observations.

No architectural decision has been made.

---

## AQ-001 — Representation of Analytical Assessments

Current architecture models Statements and Claims effectively for factual information.

It is still unclear how KOS should represent:

- expert opinions;
- analytical assessments;
- market interpretations;
- forward-looking statements.

This question remains intentionally unresolved until additional real-world scenarios are analyzed.

---

## AQ-002 — Confidence Granularity

Current architecture contains a single concept of Confidence.

Dry runs increasingly suggest that KOS may need to distinguish between:

- Source Confidence
- Evidence Confidence

The question remains intentionally unresolved until additional scenarios confirm that the distinction is consistently useful.

---

## Known Risks

Premature implementation.

Premature technology selection.

Overengineering.

Indefinite conceptual refinement with no defined stopping point (see Phase 1 Exit Criteria).

Silent regression during restructuring — a restructuring pass can drop a concept that was added for a specific, evidenced reason without anyone noticing until the same real-world case is retested (this happened to Attribution/ADR-011 between sessions). Mitigation: before removing or substantially rewriting a concept, check DECISIONS.md for the ADR that introduced it and confirm the reasoning no longer applies, rather than confirming only that the text looks redundant.

---

## Last Updated

2026-07-04 (documentation consistency pass — no new architecture; fixed a numbering collision and propagated ADR-021/ADR-022 into CONCEPTS.md and KNOWLEDGE_MODEL.md. Previous entry: 2026-07-03, session 4 continued — Event Resolution resolved end-to-end, ADR-020; first of five Resolution-type gaps to reach Accepted)
