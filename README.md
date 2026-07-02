# Open Decision Evidence Standard

- **Status:** Discussion Draft v0.2 narrative; schema reference `pder-v0.1`
- **Repository:** `open-decision-evidence-standard`
- **Public project page:** https://opendecisionevidence.org
- **Repository:** https://github.com/titanicprime/open-decision-evidence-standard
- **License:** Apache License 2.0
- **Initial editorial maintainer:** Cognous, pending neutral governance transition
- **Purpose:** Open, vendor-neutral record format for portable decision evidence in AI-mediated and cross-boundary decisions
- **Note:** This is not a product announcement

## Version note

The current machine-readable schema is `pder-v0.1`. The v0.2 narrative draft expands the explanatory specification text and informative related-work review but does not introduce a schema-breaking change.

A future schema-breaking update should be versioned separately.

## Summary

The Open Decision Evidence Standard is a discussion draft for a portable decision evidence record with integrity and verification metadata that can travel with, or alongside, a decision outcome.

The draft addresses a recurring cross-boundary problem: decisions move across organizations, systems, and jurisdictions, but the evidence needed to understand and rely on those decisions usually does not. The proposed record format is intended to make decision evidence more portable without requiring confidential source data to move, without requiring shared infrastructure, and without requiring counterparties to join a proprietary trust network.

A good decision evidence record should carry coordinates, not conclusions.

## What This Is

This repository contains a candidate standard for an open, vendor-neutral, freely implementable record format for portable decision evidence in AI-mediated and cross-boundary decisions.

A portable decision evidence record is meant to answer:

> What was decided, by whom, under what authority, using what human and machine roles, against what evidence and rules, under what conditions, and with what current validity status?

The repository includes a discussion-draft schema, field documentation, examples, conformance materials, and profiles for different implementation contexts.

## What This Is Not

This is not:

- a commercial product;
- a proprietary trust network;
- a data lake;
- a shared ledger by default;
- a universal workflow system;
- a model registry;
- a policy management platform;
- a replacement for ISO, NIST, SOC, audit, legal review, GRC, or sector-specific standards;
- a requirement that counterparties expose confidential data to one another;
- a certification that any decision is correct;
- or a claim that portable records eliminate misuse, fraud, regulatory risk, or governance failure.

## ODES as the missing interoperability primitive

ODES is not a replacement for ISO/NIST governance frameworks, AIBOMs, model passports, audit logs, provenance frameworks, or commercial execution platforms. It addresses a narrower object: the portable decision evidence record.

AIBOMs describe what the AI system is: its components, dependencies, lineage, lifecycle context, and supply-chain properties. ODES describes what the AI-influenced decision was: who or what participated, under what authority, with what human disposition, under what model state, against what evidence and policy basis, and under what consumption conditions.

The intended role of ODES is to help decision-level evidence travel across organizational, system, and jurisdictional boundaries without forcing counterparties into the same platform or requiring disclosure of underlying confidential data.

## Why This Should Be Open

A decision evidence format intended for cross-boundary use should not require trust in a single vendor or operator. Openness matters because relying parties need to inspect the format, implement it independently, test it publicly, and use it without joining a proprietary control plane.

An open candidate standard also helps preserve a clean distinction between the public record format and any commercial products that may later produce, verify, route, or govern records built on top of it.

## Background

Artificial intelligence makes an existing governance gap more acute. Decisions can now be created, recommended, routed, or executed at greater speed and scale, with changing model states and weaker human review artifacts than many legacy control environments assumed.

Internal governance remains necessary, but internal governance alone is not enough when a decision must be consumed by another organization, another system, or another jurisdiction. This draft focuses on portability of decision evidence rather than portability of raw underlying data.

## Core Design Principles

1. **Record, not copy**
2. **Supports verification without blind trust in the issuer**
3. **Portable across boundaries**
4. **Human and machine roles must be distinguishable**
5. **Model state matters**
6. **Authority must be time-bound**
7. **The record should fail closed**

## Minimum Expressible Field Categories

The table below describes conceptual field categories. The normative draft JSON field paths are defined in `schema/pder-v0.1.schema.json` and documented in `schema/pder-v0.1-fields.md`.

| Field category | Purpose |
| --- | --- |
| Decision identifier | Stable identifier for the decision being evidenced. |
| Decision type | High-level category of decision or disposition. |
| Decision timestamp | Time at which the decision was made. |
| Issuer identity | Organization and system identity for the record issuer. |
| Authority basis and validity | Source and validity window of decision authority. |
| Machine role | Whether and how AI or automation participated. |
| Model state | Model identity, version, and runtime coordinates relevant to review. |
| Human disposition | Human review status and disposition in relation to machine output. |
| Machine reliance level | Approximate degree of machine reliance in the human decision path. |
| Evidence commitment | Hash, reference, attestation, proof, or explicit absence of supporting evidence commitment. |
| Policy basis | Rules, controls, contracts, or standards used in the decision. |
| Risk coordinates | Risk tier, jurisdiction, and restricted or prohibited use flags. |
| Consumption conditions | Who may assess the record for a stated purpose, under stated conditions, and until when. |
| Freshness status | Current, stale, expired, superseded, revoked, pending revalidation, or unknown status. |
| Verification metadata | Signature, key reference, profile, and verifier information. |

In the v0.1 schema, the model-state, machine-reliance-level, evidence-commitment, and freshness-status concepts are represented within the `machine_role`, `human_disposition`, `evidence`, and `status` objects.

## Illustrative Example

```json
{
  "record_type": "portable_decision_evidence_record",
  "schema_version": "0.1",
  "decision_id": "air-2026-07-001",
  "decision_type": "ai_assisted_review",
  "decision_timestamp": "2026-07-01T14:30:00Z",
  "issuer": {
    "organization_id": "issuer.example.org",
    "system_id": "review-orchestrator"
  },
  "authority": {
    "human_reviewer_role": "senior_case_reviewer",
    "authority_basis": "internal-review-policy-v3",
    "authority_valid_at_decision": true
  },
  "machine_role": {
    "ai_used": true,
    "role": "recommendation",
    "model_id": "triage-model",
    "model_version": "2026.06"
  },
  "human_disposition": {
    "status": "modified",
    "review_substantiveness": "substantive",
    "machine_reliance_level": "medium"
  },
  "evidence": {
    "evidence_commitment_type": "hash",
    "evidence_hash": "sha256:...",
    "selective_disclosure_available": true
  },
  "policy_basis": [
    {
      "policy_id": "review-policy",
      "policy_version": "3.2",
      "policy_type": "internal_policy"
    }
  ],
  "risk_coordinates": {
    "risk_tier": "medium",
    "jurisdiction": "multi-jurisdiction"
  },
  "consumption_conditions": {
    "permitted_relying_parties": ["counterparty-a"],
    "permitted_purposes": ["audit"],
    "expires_at": "2026-09-30T00:00:00Z"
  },
  "status": {
    "freshness": "current",
    "superseded": false,
    "revoked": false
  },
  "verification": {
    "signature_type": "jws-detached",
    "issuer_key_reference": "did:web:issuer.example.org#keys-1",
    "conformance_profile": "pder_v0_1_minimal"
  }
}
```

Schema validation checks structure. It does not establish that the underlying decision is correct, lawful, complete, or suitable for reliance. A record may be schema-valid and still fail profile conformance, verifier acceptance, or a relying party's decision to rely.

## Candidate Use Cases

- AI-assisted underwriting
- Claims handling
- Trade finance
- Customs and logistics
- AML and sanctions
- Vendor AI governance
- Agentic AI operations
- Regulatory response

## Proposed v0.1 Scope

The v0.1 discussion draft is intentionally limited. It proposes:

- a baseline JSON record structure;
- a shared vocabulary for portable decision evidence;
- a minimal conformance profile;
- verifier requirements at the conceptual level;
- and illustrative profiles for different implementation settings.

It does not attempt to settle cryptographic profiles, sector-specific mandates, trust frameworks, or governance arrangements for a mature standards body.

## Repository Structure

```text
/
├── README.md
├── LICENSE
├── NOTICE
├── GOVERNANCE.md
├── CONTRIBUTING.md
├── SECURITY.md
├── CODE_OF_CONDUCT.md
├── docs/
├── schema/
├── examples/
├── conformance/
├── profiles/
└── rfcs/
```

See the repository directories for the current discussion-draft schema, examples, profiles, and conformance materials.

## Governance Proposal

The repository is currently under initial editorial maintenance by Cognous as a public discussion draft, with the stated goal of transitioning to neutral standards governance if the effort gains external participation and sufficient implementation interest.

See [`GOVERNANCE.md`](GOVERNANCE.md) for the current draft governance approach.

## What Would Strengthen the Draft

The draft would be strengthened by evidence that independent parties can implement it, exchange records across boundaries, validate records consistently, and use it without disclosing unnecessary confidential data.

Signs of validation would include public review, independent prototypes, comments from regulated sectors, cross-organizational testing, and convergence on useful conformance profiles.

## What Would Weaken or Falsify the Standard

The proposal would be weakened if the record cannot be interpreted consistently, requires excessive disclosure to be useful, cannot support meaningful verification without hidden infrastructure, or collapses into product-specific assumptions.

It would also be weakened if the same use cases can be met more simply by existing open formats without loss of meaning or interoperability.

## Relationship to Commercial Implementations

Commercial implementations may be developed separately. Those implementations may offer control planes, governance workflows, key management, verification services, audit interfaces, or operational tooling.

That commercial layer is outside the scope of this repository. The intent here is to keep the record format open and interoperable so that no commercial implementation becomes the format itself.

## License

Unless otherwise noted, this repository is licensed under the Apache License 2.0. The intent is to develop an open, vendor-neutral, freely implementable record format for portable decision evidence. Commercial implementations may be developed separately, provided the record format remains open and interoperable.

## Contribution Policy

Contributions are welcome through issues and pull requests. Contributors should focus on technical clarity, portability, verifiability, privacy, and realistic cross-boundary use.

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for contribution expectations.

## Call for Comment

Comments are especially welcome on record scope, field selection, conformance requirements, verifier behavior, privacy-preserving disclosure patterns, sector-specific examples, and alignment with existing open standards.

## Disclaimer

This repository is a discussion draft for an open, vendor-neutral candidate decision evidence standard. It is not a product announcement, legal advice, compliance advice, certification, assurance, warranty, or representation that any record produced under the draft prevents misuse, fraud, error, regulatory failure, or harm.

A schema-valid or profile-conforming record does not establish that the underlying decision is correct, lawful, complete, or suitable for reliance.

This draft has not been recognized, approved, adopted, or endorsed by any regulator or standards body.

No endorsement, affiliation, or relationship with any external researcher, standards body, regulator, or institution is implied unless expressly stated.

## Suggested Citation

*Open Decision Evidence Standard: Discussion Draft v0.2 narrative; schema reference `pder-v0.1`*. Cognous, July 2026. Repository: `open-decision-evidence-standard`. Apache License 2.0.
