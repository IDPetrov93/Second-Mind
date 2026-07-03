# TRACEABILITY

## Purpose

Every Knowledge Object inside KOS must be fully explainable.

A user should always be able to answer:

Where did this come from?

---

## Traceability Chain

Knowledge

↓

Claim

↓

Statement

↓

Document

↓

Source

---

Every transformation preserves references to the previous layer.

A Document's link to Source is not always a single hop: where a Document derives from another Document (secondary reporting, an outlet citing an outlet, an article citing a filing), that link is recorded via Attribution, and the chain branches back through it to the ultimate origin (see CONCEPTS.md, Attribution, ADR-014).

No object may lose its provenance.

---

## Design Rule

Loss of provenance always reduces knowledge quality.

---

## Principle

Explainability is more important than intelligence.
