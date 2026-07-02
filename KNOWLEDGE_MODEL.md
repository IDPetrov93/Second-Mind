# KNOWLEDGE MODEL

## Purpose

This document defines how KOS internally represents knowledge.

It does not define storage, databases or implementation details.

It defines the conceptual model that every component of the Core must use.

The Knowledge Model is independent of programming language, database technology and infrastructure.

---

# Principles

## Representation over Reality

KOS does not model reality.

KOS models the current best representation of reality based on available knowledge.

The model is expected to evolve as new information and evidence become available.

---

## Knowledge is Derived

Knowledge is never directly collected.

Knowledge is derived from information through evaluation, contextualization and confidence assessment.

---

## Traceability

Every element of knowledge must be traceable.

A human must always be able to answer:

- Where did this come from?
- Which source produced it?
- Which evidence supports it?
- Why is its confidence what it is?

Knowledge without provenance is invalid.

---

## Immutability

Original information is never modified.

Evaluation may change.

Confidence may change.

Relationships may change.

Insights may change.

The original information remains unchanged.

---

## Separation of Concepts

Each concept has a single responsibility.

Information is not Knowledge.

Evidence is not Truth.

Knowledge is not Reality.

Insight is not Decision.

The architecture must never merge these concepts.

---

# Conceptual Structure

The Knowledge Model is composed of interconnected concepts defined in CONCEPTS.md.

The model does not introduce additional concepts.

The relationships between concepts define the structure of knowledge.

A simplified conceptual flow is:

Source

↓

Information

↓

Claim

↓

Evidence

↓

Confidence

↓

Knowledge

↓

Analysis

↓

Insight

---

# Core Invariants

The following rules must always hold.

## Source

Every piece of Information originates from exactly one Source.

---

## Information

Information may contain zero or more Claims.

Information may later prove to be incorrect.

---

## Claim

Every Claim must be traceable to at least one Source.

A Claim may reference multiple Entities.

A Claim may be supported or disputed by multiple pieces of Evidence.

---

## Evidence

Evidence never establishes truth.

Evidence only changes confidence.

Evidence may support multiple Claims.

---

## Entity

Entities have stable identities.

Different sources may describe the same Entity differently.

Identity must remain independent from representation.

---

## Relation

Every Relation has a defined semantic type.

Relations may connect:

- Entity → Entity
- Claim → Claim
- Entity → Claim
- Claim → Entity

---

## Confidence

Confidence is dynamic.

Confidence may increase or decrease over time.

Confidence is never interpreted as certainty.

---

## Knowledge

Knowledge is always derived.

Knowledge is never accepted without traceability.

Knowledge may become obsolete.

---

## Insight

Insights are derived from Analysis.

Insights assist human reasoning.

Insights never trigger actions.

---

# Model Constraints

The Knowledge Model intentionally avoids defining:

- storage format
- database schema
- APIs
- network protocols
- user interfaces
- implementation technologies

These belong to later architectural documents.

---

# Architectural Consequences

All Core components must operate on this model.

No component may redefine the meaning of concepts established in CONCEPTS.md.

New concepts require updates to CONCEPTS.md before they may be used by the architecture.

Implementation decisions must preserve the semantics defined by this model.
