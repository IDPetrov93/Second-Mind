# ADR-001

## Title

Architecture is driven by concepts.

## Status

Accepted

## Reason

Shared vocabulary must exist before architecture.

Every future document must reuse existing concepts whenever possible.

---

# ADR-002

## Title

Human remains the final decision maker.

## Status

Accepted

## Reason

The KOS Core supports understanding.

It does not make decisions.

Decision-support systems are optional plugins.

---

# ADR-003

## Title

Architecture before implementation.

## Status

Accepted

## Reason

Technology choices must emerge from architecture rather than define it.

---

# ADR-004

## Title

Statements precede Claims.

## Status

Accepted

---

## Context

Documents are containers of information.

Documents themselves cannot be evaluated.

Before any claim can be verified, KOS must first identify the original statements contained within a document.

Statements preserve the original meaning and wording.

Claims are structured representations extracted from statements.

---

## Decision

The primary processing flow shall be:

Document

↓

Statement

↓

Claim

Statements become immutable historical records.

Claims become the primary evaluation objects.

---

## Consequences

- Documents are containers.
- Statements preserve provenance.
- Claims may be generated from one or more statements.
- One statement may produce multiple claims.
- Evidence is attached to claims, not documents.

# ADR-005

## Title

Claim is the smallest meaningful (atomic) processing unit of KOS.

## Status

Accepted

## Reason

A processing unit qualifies as smallest and meaningful only if it is:

- evaluable — able to carry Confidence
- atomic — cannot be decomposed further without losing evaluability
- traceable — bound to a Source
- load-bearing — required for Knowledge to exist

Information fails atomicity. It arrives at arbitrary granularity and is not yet evaluated.

Entity fails evaluability. Identity carries no Confidence of its own.

Relation fails atomicity. It is defined as a connection between two or more Entities or Claims, and is therefore structurally composite, not smaller than Claim.

Statement fails both evaluability and atomicity in the relevant sense. Statement is atomic only linguistically — it cannot be split without altering original wording — but by its own definition "may contain zero, one or multiple claims," so it is not atomic propositionally. Statement also carries no Confidence or Extraction Fidelity of its own; only the Claims structured from it do. Statement is necessary as an immutable provenance anchor (ADR-004), but it is not the unit of evaluation.

Claim satisfies all four criteria. A bare proposition without provenance is smaller still, but it cannot be evaluated and is therefore pre-architectural — it does not yet belong to KOS.

Therefore the Claim is the smallest meaningful processing unit of KOS. Every Claim must represent exactly one atomic, evaluable proposition. A statement that bundles multiple propositions is not one Claim — it must be decomposed into separate Claims during Structuring (see KNOWLEDGE_LIFECYCLE.md, Stage 3).

This decision supersedes the "should" language in the prior Claim definition in CONCEPTS.md, which is amended accordingly.

---

# ADR-006

## Title

Relation reliability is derived, not independently assigned.

## Status

Accepted

## Reason

CONCEPTS.md previously listed Relation as a bearer of independently assigned Confidence, while KNOWLEDGE_MODEL.md already excluded Relation from Confidence. This was an unresolved contradiction between the two documents.

Given ADR-005, Claim is the sole atomic, evaluable unit. Allowing Relation to also carry independently assigned Confidence would create two competing sources of reliability for the same underlying evidence, and would violate the Knowledge Model's own Structural Consistency principle ("every concept has a single responsibility").

Therefore a Relation's reliability is derived from the Confidence of the Claims and Entities it connects. Relations do not carry independently assigned Confidence. CONCEPTS.md and KNOWLEDGE_MODEL.md are amended to agree on this point.

This is the most reversible of the three decisions in this session — it removes a capability (independent relation confidence) rather than adding one, and can be revisited if a concrete case emerges where derived confidence is insufficient.

---

# ADR-007

## Title

FOUNDING_PRINCIPLES.md is merged into PROJECT_CONSTITUTION.md and removed.

## Status

Accepted

## Reason

Both documents answered the same question at the same level of abstraction ("what does this project value"). Six of ten Founding Principles duplicated existing Constitution content word-for-concept (simplicity, modularity, vendor lock-in, human-centrality). Duplication across governance documents carries the same drift risk that produced the Confidence contradiction resolved in ADR-006 — two places asserting the same thing eventually disagree.

The four non-redundant principles (Core over Features, Knowledge over Generation, Transparency over Magic, Everything is reversible unless proven otherwise) were moved into PROJECT_CONSTITUTION.md's Engineering Principles. The remaining six were dropped as duplicates, not lost — their content survives in the Constitution's existing text.

Every dependency must justify its existence; this applies to documents, not only to code and libraries.

---

# ADR-008

## Title

Extraction Fidelity is a distinct concept from Confidence.

## Status

Accepted

## Reason

The Knowledge Lifecycle's Structuring stage (Information → Claim) was implicitly treated as error-free: Confidence measured whether a Claim was reliable given evidence, but nothing measured whether the Claim was an accurate representation of the Information it was extracted from in the first place.

This is a real gap, not a hypothetical one, if extraction is performed by an LLM or any other non-deterministic process — extraction errors are independent of source truthfulness and would otherwise silently corrupt the Confidence chain.

Extraction Fidelity is introduced as a separate, mandatory value carried by every Claim, alongside Confidence. This ADR does not define how Extraction Fidelity is computed — that is deferred, consistent with "never invent missing information."

---

# ADR-009

## Title

Entity Resolution is acknowledged as an open, unresolved architectural question.

## Status

Proposed

## Reason

CONCEPTS.md previously stated Entities "have stable identities" without addressing how two references are determined to refer to the same Entity. This silently assumed a solved problem.

This ADR does not solve Entity Resolution. It only records that the project has not yet decided how it works, adds it to Pending Concepts, and blocks it from being treated as settled. Status is Proposed, not Accepted, because no resolution strategy has been evaluated yet — it requires its own dedicated session and likely its own document.

---

# ADR-010

## Title

Phase 1 requires explicit exit criteria.

## Status

Proposed

## Reason

PROJECT_STATE.md's Known Risks named "premature implementation" and "overengineering" but nothing prevented the opposite failure mode: indefinite conceptual refinement with no defined point at which Phase 1 (Foundation) is considered complete enough to proceed.

Exit criteria are added to PROJECT_STATE.md. Status is Proposed because the specific criteria are a first draft and should be challenged, not assumed correct on arrival.
