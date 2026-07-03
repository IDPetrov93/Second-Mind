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

Claim Extraction is a **lossy transformation**.

Every extracted Claim must reference its originating Statement.

The original Statement must always be preserved to allow future re-extraction using improved extraction methods.

Every Claim receives an initial **Extraction Fidelity** estimate.

Extraction Fidelity measures how faithfully the Claim represents the originating Statement.

Extraction Fidelity is **not** Confidence.

Claims become independently evaluable.

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
