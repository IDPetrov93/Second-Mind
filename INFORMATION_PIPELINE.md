# INFORMATION PIPELINE

## Purpose

This document defines how KOS transforms incoming Signals into maintained Knowledge.

Signals are never trusted by default.

Every Signal must pass validation before it is allowed to influence any Topic.

KOS is Topic-centric.

Knowledge—not information—is the primary product of KOS.

---

# Pipeline Overview

```text
External World
       │
       ▼
Signal Detection
       │
       ▼
Signal Validation
       │
       ▼
Topic Identification
       │
       ▼
Knowledge Acquisition
       │
       ▼
Knowledge Validation
       │
       ▼
Knowledge Maintenance
       │
       ▼
Pattern Detection
       │
       ▼
Knowledge Synthesis
```

---

# Stage 1 — Signal Detection

A Signal is an indication that one or more Topics may require investigation.

Possible Signal types include:

- News article
- RSS item
- Official announcement
- Government publication
- SEC filing
- Research paper
- Company blog
- Financial report
- Social media
- Video
- Podcast
- User input

A Signal is only a trigger.

It is never Knowledge.

---

# Stage 2 — Signal Validation

KOS validates every Signal before investigation.

Questions include:

- Did the reported event occur?
- Is the original source identifiable?
- Is the Signal current?
- Is the context preserved?
- Can independent sources corroborate it?

Possible outcomes:

- Validated
- Partially Validated
- Inconclusive
- Rejected

Rejected Signals never modify Knowledge.

---

# Stage 3 — Topic Identification

Determine which Topics are affected.

One Signal may affect multiple Topics.

Topics—not Signals—are maintained by KOS.

---

# Stage 4 — Knowledge Acquisition

Knowledge Acquisition is an investigative process.

Its objective is not merely to verify a Signal.

Its objective is to expand the Signal into sufficient understanding of the affected Topic.

KOS actively searches for:

- official sources
- independent reporting
- historical context
- supporting evidence
- contradicting evidence
- quantitative data
- related Topics
- existing Knowledge

Investigation continues until:

- sufficient understanding has been achieved;
- no additional reliable information can be found; or
- remaining uncertainty has been explicitly identified.

---

# Stage 5 — Knowledge Validation

Collected information is evaluated before becoming Knowledge.

Validation considers:

- factual accuracy
- provenance
- consistency
- supporting evidence
- contradictory evidence
- confidence

Unsupported information never becomes Knowledge.

Conflicting evidence is preserved.

---

# Stage 6 — Knowledge Maintenance

Validated Knowledge is integrated into the appropriate Topic.

Possible outcomes:

- new Knowledge
- updated Knowledge
- corrected Knowledge
- deprecated Knowledge
- additional context
- no meaningful change

Historical continuity is preserved.

---

# Stage 7 — Pattern Detection

KOS analyzes validated Knowledge across Topics.

Patterns emerge only from multiple validated Knowledge Objects.

Patterns describe recurring change.

Patterns are not predictions.

---

# Stage 8 — Knowledge Synthesis

KOS produces an up-to-date understanding of a Topic.

Every synthesis should answer:

- What is currently known?
- What changed?
- Why does it matter?
- What evidence supports this understanding?
- Where does uncertainty remain?
- Which Patterns are emerging?

Plugins consume synthesized Knowledge rather than raw Signals.

---

# Core Principles

- Signals initiate investigation.
- Topics accumulate Knowledge.
- Knowledge evolves continuously.
- Patterns emerge from validated Knowledge.
- Outputs are generated from Knowledge, never directly from Signals.
- Uncertainty is preserved whenever evidence is incomplete.
