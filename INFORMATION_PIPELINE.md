# INFORMATION PIPELINE

## Purpose

This document defines how KOS transforms incoming Signals into maintained Knowledge.

Signals are never trusted by default.

Every Signal must pass validation before it is allowed to influence any Topic.

KOS is Topic-centric.

Knowledge—not information—is the primary product of KOS.

---

# Pipeline Overview

```
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

KOS receives a Signal.

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
- Social media post
- Video
- Podcast
- User input

A Signal is not Knowledge.

A Signal is not Evidence.

A Signal is only a trigger.

---

# Stage 2 — Signal Validation

Before KOS investigates a Topic, the Signal itself must be evaluated.

Validation attempts to answer:

- Did the reported event actually occur?
- Is the Signal current?
- Can the original source be identified?
- Is the information presented in the correct context?
- Do independent sources support the Signal?

Possible outcomes:

- Validated
- Partially Validated
- Inconclusive
- Rejected

Rejected Signals never modify Knowledge.

Rejected Signals may still be archived for traceability.

---

# Stage 3 — Topic Identification

KOS determines which Topics may be affected.

One Signal may affect multiple Topics.

If no suitable Topic exists, KOS may create one through the Bootstrap process defined in the Topic Model.

Topics—not Signals—are the primary objects maintained by KOS.

---

# Stage 4 — Knowledge Acquisition

For every affected Topic, KOS performs investigation.

The objective is understanding.

Not confirmation.

Knowledge Acquisition may include:

- official documentation
- independent reporting
- historical context
- quantitative data
- supporting evidence
- contradicting evidence
- previous Knowledge Objects
- related Topics

KOS actively searches for missing context.

Investigation continues until sufficient understanding is achieved or available evidence is exhausted.

---

# Stage 5 — Knowledge Validation

Information collected during investigation is evaluated before entering the Knowledge Base.

Validation determines:

- factual accuracy
- consistency
- provenance
- supporting evidence
- contradictory evidence
- confidence

Unsupported information does not become Knowledge.

Conflicting information remains explicitly represented.

Uncertainty is preserved.

---

# Stage 6 — Knowledge Maintenance

Validated Knowledge is integrated into the appropriate Topic.

Possible outcomes include:

- new Knowledge Object
- updated Knowledge Object
- deprecated Knowledge
- corrected Knowledge
- additional context
- no meaningful change

Knowledge evolves continuously.

Historical continuity must be preserved.

---

# Stage 7 — Pattern Detection

KOS continuously analyzes maintained Knowledge across Topics.

The objective is to identify recurring or emerging behaviors.

Patterns are created only when supported by multiple validated Knowledge Objects.

Patterns describe change over time.

Patterns are never predictions.

---

# Stage 8 — Knowledge Synthesis

At any point, KOS should be able to produce an up-to-date understanding of a Topic.

Knowledge Synthesis answers:

- What is currently known?
- What recently changed?
- Why does it matter?
- What evidence supports this understanding?
- Where does uncertainty remain?
- Which Patterns are emerging?

Knowledge Synthesis is the primary output of the KOS Core.

Plugins consume synthesized Knowledge rather than raw Signals.

---

# Core Principles

- Signals initiate investigation.
- Topics accumulate Knowledge.
- Knowledge evolves over time.
- Patterns emerge from validated Knowledge.
- Outputs are generated from Knowledge, never directly from Signals.
- Uncertainty is preserved whenever evidence is incomplete.
