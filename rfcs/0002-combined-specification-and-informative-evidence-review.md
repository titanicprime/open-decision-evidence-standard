# RFC 0002: Combined Specification and Informative Evidence Review

- **RFC number:** 0002
- **Title:** Combined Specification and Informative Evidence Review
- **Status:** Draft
- **Proposed by:** Cognous
- **Date:** July 2026
- **Narrative version:** v0.2
- **Schema reference:** `pder-v0.1`
- **License:** Apache License 2.0

## Draft status note

This RFC is part of a discussion draft for an open, vendor-neutral candidate standard. It is not a product announcement, legal advice, compliance advice, certification, assurance, or warranty. It has not been recognized, approved, adopted, or endorsed by any regulator or standards body.

## Purpose

The v0.2 narrative draft separates:

- Part I: proposed specification / standards-facing layer; and
- Part II: informative evidence and related work.

Part II is informative only and defines no requirements.

## Version note

The current machine-readable schema remains `pder-v0.1`. The v0.2 narrative expands explanatory specification text and related-work analysis but does not introduce a schema-breaking update.

## Boundary Blindness attribution

Alexander D. Barrett’s July 2026 paper, Boundary Blindness Under Artificial Intelligence, is foundational related work for this draft. It independently articulates the cross-boundary decision-evidence gap and frames AI as an amplifier of a pre-existing structural failure rather than as the original cause. ODES should be read as one candidate standards-layer response to that diagnosis. No endorsement, affiliation, or relationship is implied.

## Related-work positioning

AIBOMs describe what the AI system is: its components, dependencies, lineage, lifecycle context, and supply-chain properties. ODES describes what the AI-influenced decision was: who or what participated, under what authority, with what human disposition, under what model state, against what evidence and policy basis, and under what consumption conditions.

- ISO/NIST/GRC govern internal AI management systems.
- Provenance and audit systems record traces and integrity signals.
- Commercial platforms produce, verify, govern, audit, and operationalize records.
- ODES supplies the portable decision evidence record that can cross boundaries.

## Non-goals

- not a product;
- not a compliance guarantee;
- not a replacement for ISO/NIST/GRC;
- not a replacement for AIBOMs/model passports;
- not production infrastructure;
- not proof of correctness;
- not proof that represented internal review actually occurred as described;
- not regulatory recognition.

## Next steps

- public comment;
- alignment review with AIBOM/model passport/provenance work;
- PROV-O mapping;
- cryptographic profile candidates;
- conformance test vectors; and
- cross-boundary pilot design.
