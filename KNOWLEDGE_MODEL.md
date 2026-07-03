# KNOWLEDGE MODEL

## Purpose

This document defines the conceptual structure used by KOS to represent knowledge.

The meaning of Knowledge is defined in **KNOWLEDGE_THEORY.md**.

The official terminology is defined in **CONCEPTS.md**.

This document defines how those concepts are connected.

It intentionally excludes implementation details, storage technologies and software architecture.

**Note on the entries below:** each concept has a one-line summary for readability, but that summary is not authoritative. CONCEPTS.md is the only source of truth for what a concept means. If this document and CONCEPTS.md ever disagree, CONCEPTS.md wins and this document is out of date (this has already happened twice — see ADR-006 and the Extraction Fidelity addition — hence this note).

---

# Design Principles

## Conceptual Independence

The Knowledge Model is independent of:

- programming languages
- databases
- storage engines
- APIs
- network protocols
- user interfaces

The model describes concepts, not implementation.

---

## Structural Consistency

Every concept has a single responsibility.

Relationships between concepts define the structure of knowledge.

No concept may redefine another concept.

---

## Traceability

Every connection inside the model must remain traceable.

No derived knowledge may exist without an explainable chain of relationships.

---

## Immutability

Original Information is immutable.

Derived structures may evolve.

Confidence may change.

Relations may change.

Knowledge may evolve.

Original Information never changes.

---

# Conceptual Structure

The Knowledge Model is a connected network of concepts.

Knowledge emerges from the relationships between concepts rather than from isolated objects.

The model intentionally avoids defining processing order.

Processing is defined by the Core architecture.

---

# Concept Relationships

## Source

Produces Information.

One Source may produce many Information objects.

---

## Information

Originates from exactly one Source.

May contain:

- Claims
- Entity references
- Context

Information is immutable.

Information is never automatically considered Knowledge.

---

## Statement

The smallest immutable linguistic unit extracted from Information, preserving original wording (see ADR-004).

Every Statement originates from exactly one Document.

A Statement may produce zero, one or multiple Claims.

Statements are never modified.

---

## Claim

Represents one atomic proposition (see ADR-005).

Every Claim originates from exactly one Statement, which in turn originates from one Information object (see ADR-004).

Every Claim carries both an Extraction Fidelity value and a Confidence value — these measure different things and are never merged (see ADR-008).

A Claim may reference multiple Entities.

A Claim may participate in multiple Relations.

---

## Evidence

Evidence is not a standalone object.

Evidence is the role that Information plays when it is used to evaluate one or more Claims.

The same Information may:

- support multiple Claims
- dispute multiple Claims
- remain unrelated to many Claims

Evidence influences Confidence.

Evidence never establishes truth.

---

## Entity

Represents a uniquely identifiable object.

Entity identity remains stable even when represented differently by multiple sources.

Entities may participate in many Relations.

---

## Relation

Relations connect concepts.

Every Relation has a defined semantic type.

Examples include:

- Entity → Entity
- Claim → Entity
- Claim → Claim
- Information → Claim

Relations define the structure of the Knowledge Model.

---

## Context

Provides additional meaning for interpreting Claims and Knowledge.

Context may include:

- temporal information
- related entities
- related claims
- surrounding events

Context enriches understanding but never replaces evidence.

---

## Event

Represents a change occurring at a specific point or period in time.

An Event may generate one or more Claims.

An Event may connect multiple Entities across time.

Events do not carry independently assigned Confidence. Confidence applies to the Claims an Event generates, not to the Event itself.

---

## Confidence

Confidence represents the current reliability estimate of a Claim or derived Knowledge.

A Relation's reliability is derived from the Confidence of the Claims and Entities it connects; Relations do not carry independently assigned Confidence (see ADR-006).

Confidence changes as Evidence changes.

Confidence is never certainty.

---

## Knowledge

Knowledge is the structured representation produced by connecting Claims, Entities, Relations, Context and Confidence.

The meaning of Knowledge is defined in **KNOWLEDGE_THEORY.md**.

---

## Analysis

Analysis operates on Knowledge.

Analysis discovers:

- patterns
- inconsistencies
- implications
- relationships

Analysis never modifies original Information.

---

## Insight

Insights are produced through Analysis.

Insights assist human reasoning.

Insights never become Decisions.

---

# Model Constraints

The Knowledge Model does not define:

- processing pipelines
- software components
- databases
- APIs
- implementation technologies

Those belong to later architectural documents.

---

# Architectural Rules

Every Core component must operate using this model.

No component may redefine concepts defined in **CONCEPTS.md**.

No component may redefine the meaning of Knowledge defined in **KNOWLEDGE_THEORY.md**.

New concepts must first be introduced in **CONCEPTS.md** before they may be used anywhere else.

Implementation choices must preserve the semantics defined by this model.

---

## Processing Hierarchy

Reality

↓

Observation

↓

Document

↓

Statement

↓

Claim

↓

Evidence

↓

Knowledge

↓

Insight

Each layer represents a logical transformation.

No layer may be skipped.
