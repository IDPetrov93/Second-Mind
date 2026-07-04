# CONCEPTS

This document defines the official vocabulary of KOS.

Every architectural decision must use these definitions.

If a concept is not defined here, it is not part of the architecture yet.

---

## Evidence

Evidence is the role that a Document, or a Claim structured from one, plays when it is used to evaluate one or more other Claims.

Evidence is contextual.

The same Document may support one Claim, dispute another, or be irrelevant to many others.

Evidence influences Confidence.

Evidence never establishes truth.

## Claim

A single, atomic, evaluable proposition, structured from one Statement (see ADR-004).

A claim must represent exactly one evaluable proposition. A statement that bundles multiple propositions is not one claim — it must be decomposed into separate claims (see ADR-005).

Examples:

- "Bitcoin reached a new all-time high."
- "The Federal Reserve increased interest rates."

Every claim must be traceable to its originating statement, document and source (see Provenance).

Every claim must carry both an Extraction Fidelity value and a Confidence value (see Extraction Fidelity).

A claim may be:

- supported
- disputed
- unknown

Claims may evolve as new evidence becomes available.

Claims are independently evaluable.

Claims are not knowledge.

Every Claim has a Claim Classification (e.g. factual, prediction, warning, recommendation), which determines its Validation Strategy — see Validation Strategy, ADR-022.

---

## Claim Classification

The category of proposition a Claim represents (e.g. factual, prediction, warning, recommendation).

Claim Classification determines which Validation Strategy applies to a Claim (see ADR-022).

How Claim Classification is actually assigned is not yet defined — see Pending Concepts.

---

## Validation Strategy

The method by which a Claim is evaluated, determined by its Claim Classification.

Examples:

- Evidence Comparison
- Future Outcome Tracking
- Regulatory Verification
- Scientific Verification

Validation Strategy is independent from Confidence: it determines *how* a Claim is checked, not *how reliable* it currently is (see ADR-022).

---

## Extraction Fidelity

An estimate of how faithfully an extracted Claim represents its originating Statement.

Extraction Fidelity measures extraction quality only.

It does not evaluate whether the Claim is true.

Extraction Fidelity covers more than wording drift: if a Claim assigns an action to the wrong Entity (e.g. crediting an approval to a named partner instead of the actual recipient named in the source), that is a fidelity failure, not a truth failure — the Statement was misread, not merely reworded. See ADR-019.

Extraction Fidelity and Confidence are independent concepts.

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

How two references are determined to be the same Entity (Entity Resolution) is not yet defined. This is an open architectural question, not an implementation detail — see Pending Concepts and PROJECT_STATE.md Open Questions.

---

## Relation

A meaningful connection between two or more entities, claims, or events.

Examples:

- NVIDIA → produces → AI chips
- ETF inflows → influence → Bitcoin price
- Event → follows → Event (connecting a sequence of related, discrete Events — see Event, ADR-020)

Relations create structure from information.

Every relation has a defined semantic type.

A Relation may only be created when it is explicitly stated in a Statement, or supported by independent Evidence. Co-occurrence of entities, claims, or events in the same Statement or the same time window is not, by itself, sufficient grounds to create a Relation between them (see ADR-021).

---

## Context

Relevant information surrounding a claim, entity or event.

Context answers questions such as:

- Why does this matter?
- What happened before?
- What is connected to it?

---

## Confidence

A measurable estimate of how reliable a claim or derived knowledge is, based on available evidence.

Confidence is assigned only to claims and to knowledge derived from them. A relation's reliability is derived from the confidence of the claims and entities it connects; relations do not carry independently assigned confidence (see ADR-006).

Confidence must not treat multiple Documents that trace to the same origin through Attribution as independent evidence. Five outlets echoing one report is one account, not five (see ADR-014). How this is computed is not yet defined (see Pending Concepts: Confidence Computation Model).

Confidence is never certainty.

Confidence may increase or decrease over time.

---

## Knowledge

Claims that have been evaluated, connected to context and assigned a measurable confidence.

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

Two claims describing similar content are not automatically the same Event. Topical similarity does not imply Event identity.

**Event Resolution:** two Claims are anchored to the same Event if and only if they trace, through Provenance and Attribution, to the same Primary Document (or, where no Document intervenes, the same direct Observation). If two Claims trace to different Primary Documents, they are different Events — even if they share Entities, wording, or theme, and even if one Primary Document explicitly follows another as part of the same unfolding situation. See ADR-020.

This resolves the punctual-vs-process ambiguity raised in ADR-018: what looks like one "evolving process" Event (e.g. a policy direction restated over months) is not a single fuzzy Event. It is a sequence of discrete, punctual Events — one per genuine Primary artifact (each filing, each official statement, each regulatory action) — connected to each other through Relations (e.g. Event → follows → Event) because they share Entities and a common thread, not because they are the same Event. Event itself stays punctual by definition; continuity is represented structurally, not by stretching what an Event is.

A Claim that does not describe something occurring at a specific point in time (a general statement, an opinion, an atemporal fact) does not require Event anchoring at all.

**Known remaining gap:** where two genuinely independent Primary Sources both directly document the same real-world occurrence with no Document-to-Document link between them (e.g. two agencies issuing separate statements about one incident, or independent eyewitnesses), Primary-Document anchoring will treat them as two different Events even though a human would consider them the same one. This is narrower than the original problem — it only applies when no document lineage connects the accounts — and is left as an explicit, smaller open item rather than solved here (see Pending Concepts: Independent Multi-Primary Corroboration).

---

## Document

A container that carries one or more pieces of recorded content, acquired from a Source before it has been evaluated or structured by KOS.

Examples:

- Article
- PDF
- Video
- Podcast
- Tweet
- RSS item
- API response
- Database record

Documents are transport media. Documents are not knowledge. A Document may be true, false or incomplete — Documents are not evaluated, only the Claims structured from them are.

---

## Source

The origin of a Document.

A Source may be Primary (a first-hand account: a company statement, a filing, a direct observation) or Secondary (an account derived from another Source, e.g. an outlet reporting on another outlet's reporting).

A Source may be anonymous. Anonymity is a property of a Source, not a reason to exclude it — its effect is accounted for through Confidence, not through Source identity.

A source is not automatically trustworthy.

One Source may produce many Documents.

Which sources KOS tracks, and how much any given Source is trusted, is niche-specific configuration supplied by the deployment — not part of core architecture. Core defines the structure (Source, Attribution below); concrete source catalogs and trust rankings are supplied externally, per client, per domain (see Pending Concepts: Source Trust Configuration).

Examples:

- Reuters
- SEC
- Binance Blog
- GitHub
- Government website

---

## Attribution

A link from one Document to the Source or Document it was derived from.

A Document may have zero, one, or more Attributions.

Attribution makes visible whether a Document is a Primary account or a Secondary account — one derived from another Document already known to KOS (e.g. an outlet's article about another outlet's article, or about a primary filing), rather than a direct account from a Source.

Attribution is structural only. It records that a citation or derivation exists. It does not evaluate whether that citation is trustworthy — trust is a function of Confidence, computed later, not of Attribution itself.

Multiple Documents that trace back to the same origin through Attribution are not independent corroboration of each other. They are echoes of one account, and Claims structured from them must be treated as such (see ADR-014).

How KOS determines that a Document cites or derives from another Document — as opposed to being told so explicitly by the Document itself — is not yet defined (Attribution Discovery, see Pending Concepts, ADR-017).

---

## Citation Fidelity

An estimate of how accurately a Document represents the Document or Source it is Attributed to.

Citation Fidelity is distinct from Extraction Fidelity. Extraction Fidelity measures whether a Claim faithfully represents the Statement it came from, inside one Document. Citation Fidelity measures whether a Document faithfully represents another Document or Source it claims to cite, across an Attribution link.

A Document may cite an unreliable Source accurately (high Citation Fidelity, low Source trust) or cite a reliable Source inaccurately — through spin, selective quotation, or distortion (low Citation Fidelity, high Source trust). These are independent and must not be collapsed into one number.

Citation Fidelity exists because Attribution only records that a citation exists; it says nothing about whether the citation is a fair representation of what was cited. See ADR-016.

---

## Observation

The act of detecting information from the external world.

Observation always precedes information processing.

Observation itself does not validate information.

---

## Fact

A claim that corresponds to reality.

Facts exist independently of KOS.

KOS never stores facts directly.

KOS stores knowledge with varying confidence about facts.

## Statement

The smallest immutable linguistic unit extracted from a document.

A statement preserves the original wording.

Statements may contain zero, one or multiple claims.

Statements are never modified.

Statement atomicity is linguistic, not propositional: a Statement cannot be split without altering the original wording, but it may still bundle more than one evaluable proposition. This is why Statement does not qualify as the smallest meaningful processing unit — see ADR-005.

Examples:

"We generated $1.4 billion from crypto."

"There is nothing illegal."

---

## Provenance

The complete traceability chain of a claim.

Every claim must preserve references to:

- originating statement
- originating document
- originating source
- any Attribution chain the originating document carries, where that document is itself derived from another document or source (see Attribution, ADR-014)

No claim inside KOS may lose provenance.

---

##Pattern

A recurring or emerging behavior identified through the synthesis of multiple validated Knowledge Objects over time.

Patterns describe how a Topic evolves.

Patterns are evidence-based.

Patterns are not predictions.

---

# Pending Concepts

The following concepts are intentionally left undefined.

They will only be introduced when required by the architecture.

- Memory
- Reasoning
- Timeline
- Workflow
- Task
- Collection
- Knowledge Graph
- Knowledge Quality Model
- Provenance Model
- Component Boundaries
- Internal Interface
- Entity Resolution
- Independent Multi-Primary Corroboration (when two independent Primary Sources document the same real-world occurrence with no Document-to-Document link between them, Event Resolution's Primary-Document anchoring cannot yet tell they're the same Event — narrower than the original Event Resolution problem, see ADR-020)
- Attribution Discovery (how KOS determines that a Document cites or derives from another Document is not yet defined — see ADR-017)
- Confidence Computation Model (how a Confidence value is actually derived/aggregated is not yet defined anywhere; it must account for Attribution-linked echoes, see ADR-014)
- Citation Fidelity Computation Model (how Citation Fidelity is actually measured is not yet defined — see ADR-016)
- Source Trust Configuration (how much a given Source is trusted is niche-specific and client-supplied — deliberately not defined here; core only defines the Source/Attribution structure, not a fixed trust ranking or fixed source catalog)
- Claim Classification Assignment (how a Claim is actually assigned its Claim Classification — e.g. factual vs. prediction vs. warning vs. recommendation — is not yet defined; ADR-022 requires the classification to exist and drive Validation Strategy, but not how it is produced)

A concept may only be modified through an accepted Architecture Decision Record (ADR).
