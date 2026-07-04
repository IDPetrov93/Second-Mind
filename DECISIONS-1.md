# ADR-001

## Title

Architecture is driven by concepts.

## Status

Accepted

## Reason

Shared vocabulary must exist before architecture.

Every future document must reuse existing concepts whenever possible.

---

# ADR-002

## Title

Human remains the final decision maker.

## Status

Accepted

## Reason

The KOS Core supports understanding.

It does not make decisions.

Decision-support systems are optional plugins.

---

# ADR-003

## Title

Architecture before implementation.

## Status

Accepted

## Reason

Technology choices must emerge from architecture rather than define it.

---

# ADR-004

## Title

Statements precede Claims.

## Status

Accepted

---

## Context

Documents are containers of information.

Documents themselves cannot be evaluated.

Before any claim can be verified, KOS must first identify the original statements contained within a document.

Statements preserve the original meaning and wording.

Claims are structured representations extracted from statements.

---

## Decision

The primary processing flow shall be:

Document

↓

Statement

↓

Claim

Statements become immutable historical records.

Claims become the primary evaluation objects.

---

## Consequences

- Documents are containers.
- Statements preserve provenance.
- Claims may be generated from one or more statements.
- One statement may produce multiple claims.
- Evidence is attached to claims, not documents.

# ADR-005

## Title

Claim is the smallest meaningful (atomic) processing unit of KOS.

## Status

Accepted

## Reason

A processing unit qualifies as smallest and meaningful only if it is:

- evaluable — able to carry Confidence
- atomic — cannot be decomposed further without losing evaluability
- traceable — bound to a Source
- load-bearing — required for Knowledge to exist

Information fails atomicity. It arrives at arbitrary granularity and is not yet evaluated.

Entity fails evaluability. Identity carries no Confidence of its own.

Relation fails atomicity. It is defined as a connection between two or more Entities or Claims, and is therefore structurally composite, not smaller than Claim.

Statement fails both evaluability and atomicity in the relevant sense. Statement is atomic only linguistically — it cannot be split without altering original wording — but by its own definition "may contain zero, one or multiple claims," so it is not atomic propositionally. Statement also carries no Confidence or Extraction Fidelity of its own; only the Claims structured from it do. Statement is necessary as an immutable provenance anchor (ADR-004), but it is not the unit of evaluation.

Claim satisfies all four criteria. A bare proposition without provenance is smaller still, but it cannot be evaluated and is therefore pre-architectural — it does not yet belong to KOS.

Therefore the Claim is the smallest meaningful processing unit of KOS. Every Claim must represent exactly one atomic, evaluable proposition. A statement that bundles multiple propositions is not one Claim — it must be decomposed into separate Claims during Claim Extraction (see INFORMATION_PIPELINE.md, Stage 5).

This decision supersedes the "should" language in the prior Claim definition in CONCEPTS.md, which is amended accordingly.

---

# ADR-006

## Title

Relation reliability is derived, not independently assigned.

## Status

Accepted

## Reason

CONCEPTS.md previously listed Relation as a bearer of independently assigned Confidence, while KNOWLEDGE_MODEL.md already excluded Relation from Confidence. This was an unresolved contradiction between the two documents.

Given ADR-005, Claim is the sole atomic, evaluable unit. Allowing Relation to also carry independently assigned Confidence would create two competing sources of reliability for the same underlying evidence, and would violate the Knowledge Model's own Structural Consistency principle ("every concept has a single responsibility").

Therefore a Relation's reliability is derived from the Confidence of the Claims and Entities it connects. Relations do not carry independently assigned Confidence. CONCEPTS.md and KNOWLEDGE_MODEL.md are amended to agree on this point.

This is the most reversible of the three decisions in this session — it removes a capability (independent relation confidence) rather than adding one, and can be revisited if a concrete case emerges where derived confidence is insufficient.

---

# ADR-007

## Title

FOUNDING_PRINCIPLES.md is merged into PROJECT_CONSTITUTION.md and removed.

## Status

Accepted

## Reason

Both documents answered the same question at the same level of abstraction ("what does this project value"). Six of ten Founding Principles duplicated existing Constitution content word-for-concept (simplicity, modularity, vendor lock-in, human-centrality). Duplication across governance documents carries the same drift risk that produced the Confidence contradiction resolved in ADR-006 — two places asserting the same thing eventually disagree.

The four non-redundant principles (Core over Features, Knowledge over Generation, Transparency over Magic, Everything is reversible unless proven otherwise) were moved into PROJECT_CONSTITUTION.md's Engineering Principles. The remaining six were dropped as duplicates, not lost — their content survives in the Constitution's existing text.

Every dependency must justify its existence; this applies to documents, not only to code and libraries.

---

# ADR-008

## Title

Extraction Fidelity is a distinct concept from Confidence.

## Status

Accepted

## Reason

The Knowledge Lifecycle's Structuring stage (Information → Claim) was implicitly treated as error-free: Confidence measured whether a Claim was reliable given evidence, but nothing measured whether the Claim was an accurate representation of the Information it was extracted from in the first place.

This is a real gap, not a hypothetical one, if extraction is performed by an LLM or any other non-deterministic process — extraction errors are independent of source truthfulness and would otherwise silently corrupt the Confidence chain.

Extraction Fidelity is introduced as a separate, mandatory value carried by every Claim, alongside Confidence. This ADR does not define how Extraction Fidelity is computed — that is deferred, consistent with "never invent missing information."

---

# ADR-009

## Title

Entity Resolution is acknowledged as an open, unresolved architectural question.

## Status

Proposed

## Reason

CONCEPTS.md previously stated Entities "have stable identities" without addressing how two references are determined to refer to the same Entity. This silently assumed a solved problem.

This ADR does not solve Entity Resolution. It only records that the project has not yet decided how it works, adds it to Pending Concepts, and blocks it from being treated as settled. Status is Proposed, not Accepted, because no resolution strategy has been evaluated yet — it requires its own dedicated session and likely its own document.

---

# ADR-010

## Title

Phase 1 requires explicit exit criteria.

## Status

Proposed

## Reason

PROJECT_STATE.md's Known Risks named "premature implementation" and "overengineering" but nothing prevented the opposite failure mode: indefinite conceptual refinement with no defined point at which Phase 1 (Foundation) is considered complete enough to proceed.

Exit criteria are added to PROJECT_STATE.md. Status is Proposed because the specific criteria are a first draft and should be challenged, not assumed correct on arrival.

---

# ADR-011

## Title

Claim Extraction is a Lossy Transformation

## Status

Accepted

---

## Context

Claims are structured representations extracted from Statements.

During extraction, wording, grammar and other linguistic information may be simplified or discarded.

---

## Decision

Claim Extraction is officially defined as a lossy transformation.

The originating Statement must always be preserved.

Claims must maintain a reference to their originating Statement.

---

## Consequences

- Claims may be re-extracted in the future.
- Improved extraction algorithms can be applied without losing information.
- Provenance remains complete.

---

# ADR-012

## Title

KNOWLEDGE_LIFECYCLE.md is retired in favor of INFORMATION_PIPELINE.md.

## Status

Accepted

## Reason

Both documents described the same transformation (raw content → Knowledge) with different stage counts and names (8 stages vs. 11), and both were independently cited by ADRs. Two parallel descriptions of the same process is the same drift risk already resolved once for governance documents in ADR-007.

INFORMATION_PIPELINE.md is the more developed of the two — it reflects the Document → Statement → Claim model from ADR-004, includes concrete fields (Document ID, Source, Timestamp, Language, Hash), and is already the document referenced by the newest ADRs. KNOWLEDGE_LIFECYCLE.md is removed; its one remaining cross-reference (in ADR-005) is repointed to INFORMATION_PIPELINE.md, Stage 5.

## Consequences

- One canonical pipeline document instead of two.
- README.md documentation order updated.

---

# ADR-013

## Title

Information is merged into Document; they were near-duplicate concepts.

## Status

Accepted

## Reason

CONCEPTS.md defined both Information ("any recorded content acquired from a source before it has been evaluated or structured," examples: News article, Tweet, PDF, Video, RSS item, API response) and Document ("a container that carries one or more pieces of information," examples: Article, PDF, Video, Podcast, Tweet, Database record) — overlapping examples, near-identical purpose. Meanwhile INFORMATION_PIPELINE.md, TRACEABILITY.md and the Statement/Provenance model introduced by ADR-004 only ever use Document; "Information" had become vocabulary the pipeline itself no longer used, while Evidence and Knowledge in CONCEPTS.md still referenced it.

Document is retained as the single raw-container concept. Information is removed. Evidence is redefined in terms of Document (or a Claim structured from one). Knowledge is redefined in terms of evaluated Claims, which is also more accurate given ADR-004/005 — Knowledge was never meant to emerge directly from raw, unstructured content.

This does not affect KNOWLEDGE_THEORY.md's philosophical use of "information" as a general concept (information vs. knowledge) — that is a theoretical framing, not a structural object, and is unaffected.

## Consequences

- One raw-container concept (Document) instead of two overlapping ones.
- Evidence, Knowledge, and all relationship entries in KNOWLEDGE_MODEL.md updated to reference Document instead of Information.

---

# ADR-014

## Title

Attribution and Source Primary/Secondary distinction are restored, adapted to the Document-based model.

## Status

Accepted

## Reason

A prior session (this ADR's original number, ADR-011, at the time) introduced Attribution and a Primary/Secondary Source distinction, evidenced empirically by a manual walkthrough against a real news item with a multi-hop attribution chain (anonymous sources → FT → six outlets echoing FT). A later restructuring session removed Attribution entirely, reused the ADR-011 number for an unrelated decision (Claim Extraction as a lossy transformation, which stands on its own merits and is not affected by this ADR), and did not replace Attribution with an equivalent mechanism.

A second manual walkthrough, against a real Jersey Mike's Subs IPO filing (two outlets, same day, reporting the same S-1 filing), reproduced the identical failure mode: no way to distinguish independent corroboration from echoes of one report.

Attribution and Source's Primary/Secondary/anonymous distinction are restored, this time expressed against Document (per ADR-013) rather than the retired Information concept. The Source Trust Configuration note — that concrete source catalogs and trust rankings are niche-specific, client-supplied configuration and not core architecture — is restored to Pending Concepts.

## Consequences

- CONCEPTS.md, KNOWLEDGE_MODEL.md, INFORMATION_PIPELINE.md and TRACEABILITY.md all updated to represent Attribution.
- Confidence and Evidence Collection must not count Attribution-linked echoes as independent evidence.
- Future sessions restructuring these documents should check DECISIONS.md before removing a concept that resulted from an empirical walkthrough — losing it silently means the same real-world failure has to be rediscovered from scratch, which is what happened here.

---

# ADR-015

## Title

Claims must be anchored to a specific Event; topical similarity does not imply shared Event identity.

## Status

Accepted — was Proposed pending a resolution mechanism; that mechanism is now defined by ADR-020 (Primary-Document anchoring), so the original reason for Proposed status no longer applies.

## Reason

A manual walkthrough against a real Jersey Mike's Subs IPO story found two genuinely distinct real-world events — a confidential draft S-1 filing (April 2026, ~$12B target valuation, reported via sources familiar with the matter) and a public S-1 filing under ticker JMKE (July 2026) — that a bare claim like "Jersey Mike's Subs files for IPO" cannot distinguish between. Nothing in the pipeline required a Claim to be anchored to a specific Event, and nothing prevented Evidence Collection from treating the two as corroborating or duplicate claims about "the same" filing when they describe two different real corporate actions months apart.

Event already existed as a concept ("a change occurring at a specific point or period in time... may generate one or more claims") but was never operationally used by any pipeline stage — it existed declaratively, not functionally.

This ADR requires Claim Extraction and Evidence Collection to treat Event anchoring as mandatory where time-bound, and explicitly forbids inferring shared Event identity from topical similarity alone. It does not define Event Resolution (how anchoring is actually performed) — that is deferred, consistent with "never invent missing information." Status is Proposed, not Accepted, for the same reason ADR-009 (Entity Resolution) is Proposed: the mechanism is unresolved and needs its own dedicated evaluation.

## Consequences

- CONCEPTS.md (Event), KNOWLEDGE_MODEL.md (Event), and INFORMATION_PIPELINE.md (Stages 5 and 7) updated.
- Event Resolution added to Pending Concepts, alongside Entity Resolution.
- This is the second open Resolution-type gap (Entity Resolution, Event Resolution) — worth noting as a pattern: KOS repeatedly needs a way to determine "is this the same X as that X," for more than one X. That pattern itself may deserve its own future architectural treatment rather than solving each instance separately.

---

# ADR-016

## Title

Citation Fidelity is introduced as distinct from both Extraction Fidelity and Source trust.

## Status

Accepted

## Reason

A manual walkthrough against a real story (Canada's oil pipeline / "energy superpower" announcement) surfaced a document whose content plausibly summarized NYT/FT reporting while itself showing signs of being an unreliable, editorializing aggregator. Attribution, as defined, records that a citation exists; it says nothing about whether the citing Document represents the cited Document or Source fairly. Extraction Fidelity does not cover this either — it measures Claim-vs-Statement accuracy inside one Document, not Document-vs-Document accuracy across an Attribution link.

Without this concept, a Document could carry correct Attribution (it does derive from NYT) and still misrepresent NYT through spin, selective quotation, or distortion, with nothing in the model able to express that gap.

Citation Fidelity is introduced: an estimate of how accurately a Document represents the Document or Source it is Attributed to. It is independent of Source trust (a Document can accurately cite an unreliable Source, or inaccurately cite a reliable one) and independent of Extraction Fidelity (which operates within a single Document, not across one).

This ADR does not define how Citation Fidelity is computed — deferred, consistent with "never invent missing information."

## Consequences

- CONCEPTS.md, KNOWLEDGE_MODEL.md and INFORMATION_PIPELINE.md updated.
- Citation Fidelity Computation Model added to Pending Concepts.
- Claims now carry up to three independent quality signals where applicable: Extraction Fidelity, Citation Fidelity, and Confidence. None may be merged into one number.

---

# ADR-017

## Title

Attribution Discovery is acknowledged as unresolved.

## Status

Proposed

## Reason

Attribution (ADR-014) assumes the link between a Document and what it cites is known. In practice, during the Canada pipeline walkthrough, the input text itself turned out to be a viral social post paraphrasing NYT/FT reporting with no explicit citation marker — a human or a crawler has to recognize that relationship; it is not self-evident from the text alone in general.

This ADR does not solve Attribution Discovery. It records that the project has not yet decided how a citation or derivation relationship is detected — from explicit markers, content similarity, timing, or manual assertion — and blocks it from being treated as solved by the mere existence of the Attribution field. Status is Proposed, consistent with the treatment of Entity Resolution (ADR-009) and Event Resolution (ADR-015): naming a gap is not the same as closing it.

## Consequences

- Added to Pending Concepts.
- Until resolved, Attribution should be treated as something the pipeline can record when told, not something it can reliably detect on its own.

---

# ADR-018

## Title

Event Resolution must distinguish punctual Events from evolving-process Events.

## Status

Superseded by ADR-020 — the "evolving-process Event" framing proposed here was not adopted; ADR-020 resolves the same underlying problem via Primary-Document anchoring instead. Kept for record: the problem this ADR identified (Canada pipeline walkthrough) was real.

## Reason

ADR-015 established that Claims must be anchored to a specific Event and that topical similarity does not imply shared Event identity. The Canada pipeline walkthrough showed a harder version of the same problem than the Jersey Mike's case that produced ADR-015: not two discrete alternatives, but a policy narrative reported repeatedly over five months (February, March, April, July), where the July announcement may be a genuinely new Event (a formal unveiling with a specific $105B figure) or may be the same ongoing Event restated with more detail.

Event, as defined, does not distinguish these two shapes. This ADR amends Event to explicitly recognize both punctual Events (a single discrete occurrence) and evolving-process Events (a direction observed at multiple points in time), and requires that Event Resolution — still unresolved — account for both, rather than implicitly assuming every Event is punctual.

## Consequences

- CONCEPTS.md and KNOWLEDGE_MODEL.md updated.
- Event Resolution's scope (Pending Concepts) is now explicitly wider than "is this the same Event" — it must also answer "is this an update to a known Event or a new one."

---

# ADR-019

## Title

Extraction Fidelity explicitly covers entity/subject misattribution, not only wording drift.

## Status

Accepted

## Reason

A fourth manual walkthrough (Binance / BlockShoals Philippines sandbox approval) was, unlike the previous three, mostly a validation rather than a new failure: the Attribution/echo model correctly describes the 9 outlets involved (all tracing to one X post and one SEC document), and Claim atomicity (ADR-005) already prevents the specific error found, if extraction is done correctly.

The one precise gap: the input sentence assigned the SEC's approval to Binance, when every source names BlockShoals Technologies Inc. as the actual recipient and Binance only as its named partner. This is not a wording paraphrase problem — it is a wrong-subject problem. Extraction Fidelity's definition did not make clear it was meant to catch this class of error as opposed to only loose phrasing.

This ADR does not introduce a new concept — it clarifies the existing scope of Extraction Fidelity. No pipeline change was required beyond this clarification.

## Consequences

- CONCEPTS.md updated with one clarifying sentence.
- This walkthrough is recorded as a validating result, not just a gap report — it's worth noting in PROJECT_STATE.md that not every real-world test needs to produce a new architectural concept; this one mostly confirmed prior fixes were sound.

---

# ADR-020

## Title

Event Resolution is resolved: Event identity is anchored to a Primary Document.

## Status

Accepted

## Reason

ADR-015 required Event anchoring but left the mechanism undefined. ADR-018 observed that some Events look "evolving" rather than punctual (the Canada pipeline policy story, restated across five months) and treated this as a property Event Resolution would need to handle as a special case.

On reexamination, the "evolving process Event" framing was the wrong model, not a harder version of the right one. KOS already has a structural distinction — Primary vs. Secondary Source (ADR-014) — that solves this cleanly without inventing new machinery:

Two Claims are anchored to the same Event if and only if they trace, through Provenance/Attribution, to the same Primary Document (or the same direct Observation, where no Document intervenes). Different Primary Documents mean different Events, full stop — even if they're part of the same unfolding situation, share every Entity involved, and one explicitly follows from the other.

What ADR-018 called an "evolving process Event" is, under this rule, correctly modeled as a sequence of several discrete, punctual Events — one per genuine Primary artifact — connected to each other by Relation (Event → follows → Event, extending Relation to cover Events, not only Entities and Claims). This is simpler than maintaining two kinds of Event, and it reuses a concept (Primary/Secondary Source) the architecture already needed for other reasons, rather than adding new apparatus. It directly follows the Constitution's engineering principle of simplicity before cleverness.

This supersedes ADR-018's framing. ADR-018 is not reverted — the problem it identified (Canada walkthrough) was real — but the fix is this ADR, not "Event has two kinds."

This does not fully close every case. Where two genuinely independent Primary Sources both directly document the same real-world occurrence with no Document-to-Document link between them (e.g. two government agencies each issuing their own statement about one incident), this rule will incorrectly treat them as two different Events. This is a real, smaller gap, renamed Independent Multi-Primary Corroboration and kept in Pending Concepts, rather than papered over. It is a narrower problem than the one this ADR closes: it only applies when no document lineage connects the accounts at all, which is the less common case for the kinds of claims KOS is built to process (regulatory filings, corporate announcements, reported news) — most of which do have exactly one triggering Primary artifact.

## Consequences

- CONCEPTS.md, KNOWLEDGE_MODEL.md and INFORMATION_PIPELINE.md updated. Event Resolution removed from Pending Concepts as resolved.
- Relation's scope widened to include Event → Event connections.
- Independent Multi-Primary Corroboration added to Pending Concepts as a narrower, separate remaining gap.
- Of the five Resolution-type gaps named across this project (Entity Resolution, Event Resolution, Attribution Discovery, Confidence Computation Model, Citation Fidelity Computation Model), this is the first to reach Accepted status rather than staying Proposed or Pending.

---

# ADR-021

## Title

Relationships Must Not Be Inferred Without Evidence

## Status

Accepted

---

## Context

Statements frequently mention multiple entities together.

Their relationship is often implied rather than explicitly stated.

Incorrect relationship inference can produce false knowledge.

---

## Decision

Relationships between entities shall only be created when:

- explicitly stated in a Statement, or

- supported by independent Evidence.

Entity co-occurrence alone is insufficient.

---

## Consequences

Mentioning two entities in the same Statement does not establish a relationship.

Unknown relationships remain unknown.

Future Evidence may strengthen or create relationships.

---

# ADR-022

## Title

Claim Validation Depends on Claim Type

## Status

Accepted

---

## Context

Not all Claims can be evaluated using the same validation process.

A factual Claim can often be verified through supporting or contradicting evidence.

Predictions, warnings and recommendations require different validation approaches.

---

## Decision

Every Claim shall define its Validation Strategy.

Validation Strategy depends on Claim Classification.

Examples include:

- Evidence Comparison
- Future Outcome Tracking
- Regulatory Verification
- Scientific Verification

The Validation Strategy is independent from Confidence.

---

## Consequences

Evaluation becomes extensible.

New Claim types may introduce new Validation Strategies without changing the processing pipeline.
