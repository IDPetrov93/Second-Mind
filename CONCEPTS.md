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

Information that supports or contradicts one or more claims.

Evidence changes confidence.

Evidence does not create truth.

The same evidence may support competing claims.

Evidence may support or contradict multiple claims.

---

## Claim

A single statement that can be evaluated.

Every claim should represent a single evaluable proposition.

Examples:

- "Bitcoin reached a new all-time high."
- "The Federal Reserve increased interest rates."

Every claim should be traceable to one or more sources.

A claim may be:

- supported
- disputed
- unknown

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

A measurable estimate of how reliable a claim, relation or derived knowledge is, based on available evidence.

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

# Pending Concepts

The following concepts are intentionally left undefined.

They will only be introduced when required by the architecture.

- Memory
- Reasoning
- Timeline
- Workflow
- Task
- Observation
- Fact
- Document
- Collection
- Knowledge Graph
- Reality Model
