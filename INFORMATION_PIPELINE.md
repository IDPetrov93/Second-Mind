# INFORMATION PIPELINE

## Purpose

This document defines how KOS transforms observations into structured knowledge.

The pipeline describes logical transformations only.

Implementation details are intentionally excluded.

---

# Pipeline

Reality

↓

Observation

↓

Document Registration

↓

Information Normalization

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

Knowledge

↓

Analysis

↓

Insight

↓

Human

---

## Stage 1 — Observation

Input

External reality.

Output

Observed document.

Purpose

Detect potentially relevant information.

No interpretation occurs.

---

## Stage 2 — Document Registration

Input

Observed document.

Output

Registered document with metadata.

Metadata includes:

- Source
- Timestamp
- URL
- Media Type
- Language
- Hash

Purpose

Create an immutable historical record.

The document itself is never modified.

---

## Stage 3 — Information Normalization

Input

Registered document.

Output

Normalized textual representation.

Purpose

Convert information into a common internal format.

No semantic interpretation occurs.

---

## Stage 4 — Statement Extraction

Input

Normalized information.

Output

Individual statements.

Purpose

Separate direct observations from quotations.

A statement may represent:

- Author statement
- Quoted speech
- Numerical value
- Caption
- Title

Statements preserve their original wording.

---

## Stage 5 — Claim Extraction

Input

Statements.

Output

Atomic claims.

Purpose

Convert statements into independently evaluable claims.

One statement may generate zero, one or many claims.

---

## Stage 6 — Claim Classification

Input

Claims.

Output

Typed claims.

Possible categories include:

- Factual
- Financial
- Political
- Scientific
- Legal
- Opinion
- Prediction
- Historical

A claim may belong to multiple categories.

---

## Stage 7 — Evidence Collection

Input

Typed claims.

Output

Claims linked to supporting and contradicting evidence.

Purpose

Collect all relevant evidence.

Evidence never determines truth.

---

## Stage 8 — Evaluation

Input

Claims with evidence.

Output

Confidence assessment.

Purpose

Estimate confidence using available evidence.

Confidence is never certainty.

---

## Stage 9 — Knowledge

Input

Evaluated claims.

Output

Knowledge objects.

Purpose

Represent the current best understanding.

Knowledge remains revisable.

---

## Stage 10 — Analysis

Input

Knowledge.

Output

Patterns, relationships and inconsistencies.

Purpose

Generate higher-level understanding.

---

## Stage 11 — Insight

Input

Analysis.

Output

Human-readable insights.

Purpose

Support human reasoning.

Insights never become decisions.

---

# Core Principles

Documents are immutable.

Statements preserve original wording.

Claims are the primary processing unit.

Evidence is linked to claims.

Knowledge is revisable.

Humans remain responsible for decisions.
