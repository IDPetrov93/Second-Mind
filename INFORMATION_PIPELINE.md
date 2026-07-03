# INFORMATION PIPELINE

## Purpose

Describe how observations become knowledge.

The pipeline defines logical transformations only.

Implementation details are intentionally excluded.

---

Reality

↓

Observation

↓

Document Registration

↓

Normalization

↓

Statement Extraction

↓

Claim Extraction

↓

Claim Classification

↓

Evidence Collection

↓

Evaluation

↓

Knowledge Update

↓

Analysis

↓

Insight

↓

Human

---

## Stage 1 — Observation

Observe potentially relevant information.

No interpretation occurs.

---

## Stage 2 — Document Registration

Register an immutable document.

Assign:

- Document ID
- Source
- Timestamp
- Language
- Hash
- Attribution (optional — if this Document derives from, or reports on, another Document or a cited Source rather than being a direct first-hand account, that link must be recorded here; see CONCEPTS.md, ADR-014). How this link is detected in the first place — from explicit citation, from content matching, or otherwise — is not yet defined (Attribution Discovery, see ADR-017). Until it is, Attribution may need to be asserted rather than automatically discovered.

The original document must never be modified.

---

## Stage 3 — Normalization

Convert the document into a common internal representation.

No semantic interpretation occurs.

---

## Stage 4 — Statement Extraction

Extract immutable Statements.

Statements preserve the original wording.

Statements preserve provenance.

Statements are never modified.

---

## Stage 5 — Claim Extraction

Transform Statements into structured Claims.

One Statement may generate:

- zero Claims
- one Claim
- many Claims

Claim Extraction is a **lossy transformation** (see ADR-011).

Every extracted Claim must reference its originating Statement.

The original Statement must always be preserved to allow future re-extraction using improved extraction methods.

Every Claim receives an initial **Extraction Fidelity** estimate.

Extraction Fidelity measures how faithfully the Claim represents the originating Statement.

Extraction Fidelity is **not** Confidence.

Where the originating Document carries an Attribution, it must also receive a **Citation Fidelity** estimate — how faithfully it represents the Document or Source it cites. This is separate from both Extraction Fidelity and Confidence (see CONCEPTS.md, ADR-016).

Claims become independently evaluable.

Where a Claim describes something occurring at a specific point or period in time, it must be anchored to an Event (see CONCEPTS.md, Event). Anchoring rule: a Claim is anchored to the same Event as another Claim only if both trace, through Provenance/Attribution, to the same Primary Document. A Claim tracing to a different Primary Document is a different Event, even on the same topic (Event Resolution, see ADR-020).

---

## Stage 6 — Claim Classification

Assign one or more semantic categories.

Examples:

- Financial
- Political
- Scientific
- Legal
- Opinion
- Prediction
- Historical

Classification guides later validation.

---

## Stage 7 — Evidence Collection

Collect supporting and contradicting evidence.

Evidence is never discarded.

Evidence is attached to Claims.

Documents connected by Attribution to the same origin must not be counted as independent evidence — they are echoes (see ADR-014).

Claims anchored to different Events must not be treated as corroborating or duplicate evidence for each other, even when topically similar (see ADR-020). Where related Events form a sequence (e.g. an unfolding policy direction), that continuity is a Relation between Events, not shared Evidence.

---

## Stage 8 — Evaluation

Estimate Confidence using currently available evidence.

Evaluation never determines truth.

Confidence may increase or decrease over time.

---

## Stage 9 — Knowledge Update

Create or update Knowledge Objects.

Knowledge always remains revisable.

Knowledge never loses provenance.

---

## Stage 10 — Analysis

Discover patterns, relationships and inconsistencies across Knowledge.

---

## Stage 11 — Insight

Generate human-readable observations.

Insights support reasoning.

Insights never become decisions.

---

# Core Principles

Documents are immutable.

Statements are immutable.

Claims are independently evaluable.

Knowledge is revisable.

Every object preserves provenance.

Every transformation is explainable.
