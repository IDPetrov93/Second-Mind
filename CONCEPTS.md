# CONCEPTS

This document defines the official vocabulary of KOS.

Every architectural decision must use these definitions.

If a concept is not defined here, it is not part of the architecture yet.

---

## Information

Any recorded content acquired from a source before it has been evaluated or structured by KOS.

Examples:

- News article
- Tweet
- PDF
- Video
- RSS item
- API response

Information may be true, false or incomplete.

---

## Source

The origin of information.

Examples:

- Reuters
- SEC
- Binance Blog
- GitHub
- Government website

A source is not automatically trustworthy.

One source may produce many pieces of information.

---

## Evidence

Evidence is the role that Information plays when it is used to evaluate one or more Claims.

Evidence is contextual.

The same Information may support one Claim, dispute another, or be irrelevant to many others.

Evidence influences Confidence.

Evidence never establishes truth.

## Claim

A single, atomic, evaluable proposition.

A claim must represent exactly one evaluable proposition. A statement that bundles multiple propositions is not one claim — it must be decomposed into separate claims (see ADR-005).

Examples:

- "Bitcoin reached a new all-time high."
- "The Federal Reserve increased interest rates."

Every claim must be traceable to one or more sources.

A claim may be:

- supported
- disputed
- unknown

---

## Extraction Fidelity

A measurable estimate of how accurately a Claim represents the Information it was extracted from.

Extraction Fidelity is distinct from Confidence. Confidence estimates whether a Claim is reliable given evidence. Extraction Fidelity estimates whether a Claim is an accurate representation of its source at all — a precondition for Confidence to mean anything.

Every Claim must carry both an Extraction Fidelity value and a Confidence value. They are never merged into one number.

This concept exists because Structuring (see KNOWLEDGE_LIFECYCLE.md, Stage 3) is a transformation, not a copy, and transformations can be wrong independent of whether the underlying Information is true. See ADR-008.

---

## Entity

A uniquely identifiable object.

Examples:

- Bitcoin
- NVIDIA
- BlackRock
- SEC
- Jerome Powell

Entities are the primary objects represented by KOS.

Entities have stable identities independent of the information that describes them.

How two references are determined to be the same Entity (Entity Resolution) is not yet defined. This is an open architectural question, not an implementation detail — see Pending Concepts and PROJECT_STATE.md Open Questions.

---

## Relation

A meaningful connection between two or more entities or claims.

Examples:

- NVIDIA → produces → AI chips
- ETF inflows → influence → Bitcoin price

Relations create structure from information.

Every relation has a defined semantic type.

---

## Context

Relevant information surrounding a claim, entity or event.

Context answers questions such as:

- Why does this matter?
- What happened before?
- What is connected to it?

---

## Confidence

A measurable estimate of how reliable a claim or derived knowledge is, based on available evidence.

Confidence is assigned only to claims and to knowledge derived from them. A relation's reliability is derived from the confidence of the claims and entities it connects; relations do not carry independently assigned confidence (see ADR-006).

Confidence is never certainty.

Confidence may increase or decrease over time.

---

## Knowledge

Information that has been evaluated, connected to context and assigned a measurable confidence.

Knowledge may later prove incorrect.

Knowledge is not truth.

Knowledge is our current best understanding.

---

## Analysis

The process of examining knowledge to discover patterns, relationships, inconsistencies or implications.

Analysis consumes knowledge but does not alter its meaning.

Analysis produces insights.

Understanding belongs to the human.

---

## Insight

A useful observation produced through analysis.

Insights help humans reason.

Insights may be uncertain.

Insights are never decisions.

---

## Decision

An action chosen by a human.

The KOS Core never makes decisions.

Decision-support systems may exist as optional plugins.

---

## Event

A change occurring at a specific point or period in time.

Events may generate one or more claims.

Events connect entities across time.

---

## Document

A container that carries one or more pieces of information.

Examples:

- Article
- PDF
- Video
- Podcast
- Tweet
- Database record

Documents are transport media.

Documents are not knowledge.

---

## Observation

The act of detecting information from the external world.

Observation always precedes information processing.

Observation itself does not validate information.

---

## Fact

A claim that corresponds to reality.

Facts exist independently of KOS.

KOS never stores facts directly.

KOS stores knowledge with varying confidence about facts.

## Statement

The smallest immutable linguistic unit extracted from a document.

A statement preserves the original wording.

Statements may contain zero, one or multiple claims.

Statements are never modified.

Examples:

"We generated $1.4 billion from crypto."

"There is nothing illegal."

---

## Claim

A structured representation of one or more assertions extracted from statements.

Claims are independently evaluable.

Claims may be supported or contradicted by evidence.

Claims may evolve as new evidence becomes available.

Claims are not knowledge.

---

## Provenance

The complete traceability chain of information.

Every claim must preserve references to:

- originating statement
- originating document
- originating source

No information inside KOS may lose provenance.

# Pending Concepts

The following concepts are intentionally left undefined.

They will only be introduced when required by the architecture.

- Memory
- Reasoning
- Timeline
- Workflow
- Task
- Collection
- Knowledge Graph
- Knowledge Quality Model
- Provenance Model
- Component Boundaries
- Internal Interface
- Entity Resolution
- Confidence Computation Model (how a Confidence value is actually derived/aggregated is not yet defined anywhere)


  A concept may only be modified through an accepted Architecture Decision Record (ADR).
