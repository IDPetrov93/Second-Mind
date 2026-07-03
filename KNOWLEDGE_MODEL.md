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

Original Documents are immutable.

Derived structures may evolve.

Confidence may change.

Relations may change.

Knowledge may evolve.

Original Documents never change.

---

# Conceptual Structure

The Knowledge Model is a connected network of concepts.

Knowledge emerges from the relationships between concepts rather than from isolated objects.

The model intentionally avoids defining processing order.

Processing is defined by the Core architecture.

---

# Concept Relationships

## Source

Produces Documents.

One Source may produce many Documents.

A Source may be Primary or Secondary; concrete source catalogs and trust rankings live outside core (see CONCEPTS.md, Pending Concepts: Source Trust Configuration).

---

## Attribution

Links a Document to the Source or Document it derives from.

Attribution is structural, not evaluative — it does not itself carry Confidence or trust.

Documents connected by Attribution to the same origin are echoes, not independent corroboration (see ADR-014).

Where Attribution exists, the citing Document also carries a Citation Fidelity value — how accurately it represents what it cites. This is separate from whether the cited Source itself is trustworthy (see CONCEPTS.md, ADR-016).

---

## Document

Originates from exactly one Source.

May carry zero, one, or more Attributions to other Documents or Sources it derives from.

May contain, once processed:

- Statements
- Claims
- Entity references
- Context

Documents are immutable.

Documents are never automatically considered Knowledge.

---

## Statement

The smallest immutable linguistic unit extracted from a Document, preserving original wording (see ADR-004).

Every Statement originates from exactly one Document.

A Statement may produce zero, one or multiple Claims.

Statements are never modified.

---

## Claim

Represents one atomic proposition (see ADR-005).

Every Claim originates from exactly one Statement, which in turn originates from exactly one Document (see ADR-004).

Every Claim carries both an Extraction Fidelity value and a Confidence value — these measure different things and are never merged (see ADR-008).

A Claim may reference multiple Entities.

A Claim may participate in multiple Relations.

---

## Evidence

Evidence is not a standalone object.

Evidence is the role that a Document, or a Claim structured from one, plays when it is used to evaluate one or more other Claims.

The same Document may:

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
- Event → Event (sequence of related, discrete Events)

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

Topical similarity between Claims does not imply they belong to the same Event.

Event Resolution: two Claims are anchored to the same Event only if they trace, through Provenance/Attribution, to the same Primary Document (or the same direct Observation). Different Primary Documents mean different Events, even within the same unfolding situation. Continuity across related Events is expressed via Relation (Event → follows → Event), not by treating them as one Event (see CONCEPTS.md, ADR-020 — this supersedes the punctual-vs-process framing in ADR-018).

---

## Confidence

Confidence represents the current reliability estimate of a Claim or derived Knowledge.

A Relation's reliability is derived from the Confidence of the Claims and Entities it connects; Relations do not carry independently assigned Confidence (see ADR-006).

Confidence must not treat Attribution-linked echoes of the same origin as independent evidence (see ADR-014).

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

Analysis never modifies original Documents.

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

The high-level chain (Reality → Observation → Document → Statement → Claim → Evidence → Knowledge → Insight) is defined once, in **TRACEABILITY.md**. The detailed stage-by-stage pipeline is defined in **INFORMATION_PIPELINE.md**. Neither is repeated here — see the note at the top of this document about why duplication is avoided.
