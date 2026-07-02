# Open Decision Evidence Standard

**Status:** Discussion Draft v0.1  
**Repository:** `open-decision-evidence-standard`  
**License:** Apache License 2.0  
**Maintainer:** Cognous, pending neutral standards governance  
**Purpose:** Open, vendor-neutral record format for portable decision evidence in AI-mediated and cross-boundary decisions  
**Note:** This is not a product announcement.

---

## Summary

Artificial intelligence is accelerating a problem that regulated markets have tolerated for decades:

> Decisions cross organizational boundaries, but the evidence behind those decisions usually does not.

A claim may be approved, a transaction cleared, a risk accepted, a vendor certified, a document verified, or an AI-assisted recommendation adopted. But the receiving party often cannot independently determine:

- who reviewed the matter;
- under what authority;
- against which rule, policy, model, contract, or evidence basis;
- with what degree of human judgment and machine assistance;
- under what model state or system configuration;
- and whether the basis for the decision remains current, stale, superseded, revoked, or expired.

This is not primarily a data-sharing problem.

The missing layer is **decision evidence**.

The **Open Decision Evidence Standard** proposes a portable, tamper-evident record format for carrying decision evidence across organizational, system, and jurisdictional boundaries without requiring counterparties to share the same platform, expose underlying confidential data, or join a proprietary trust network.

The goal is simple:

> When an AI-influenced decision crosses a boundary, the evidence required to rely on that decision should be able to cross with it.

---

## What This Is

The Open Decision Evidence Standard is a proposed open record format for cross-boundary decision evidence.

A portable decision evidence record is a structured artifact that can travel with, or alongside, a decision outcome. It allows a relying party to evaluate the basis for reliance without blindly trusting the issuer and without requiring the issuer to disclose all underlying data.

The record should answer:

> What was decided, by whom, under what authority, using what human and machine roles, against what evidence and rules, under what conditions, and with what current validity status?

The point is not to force all parties to accept the same conclusion.

The point is to allow each relying party to apply its own rules to a trustworthy record of what happened.

A good decision evidence record should carry:

> **coordinates, not conclusions.**

---

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

The standard should define the record format and verification semantics.

Commercial systems may produce, consume, route, verify, govern, audit, and operationalize those records.

The record format should remain open, vendor-neutral, and freely implementable.

---

## Why This Should Be Open

A cross-boundary decision evidence layer only works if parties on both sides of a boundary trust the format.

They will not rely on a format controlled by a competitor.

They will hesitate to adopt a format controlled by a single vendor.

They will resist infrastructure that requires entry into a proprietary network before a decision can be verified.

For that reason, the standard layer should be:

- openly specified;
- freely implementable;
- vendor-neutral;
- testable through public conformance profiles;
- compatible with selective disclosure;
- designed to preserve data locality;
- usable across regulated sectors;
- and compatible with commercial implementations.

The public good is the record format.

The market opportunity is the infrastructure that produces, verifies, governs, audits, and operationalizes those records.

---

## Background

This draft is aligned with independent research on **boundary blindness** under artificial intelligence: the observation that AI does not create the cross-boundary evidence gap, but removes the human slack that previously made the gap survivable.

Alexander D. Barrett’s July 2026 paper, *Boundary Blindness Under Artificial Intelligence*, argues that decision evidence often fails to travel across organizational, software, and regulatory boundaries, leaving relying parties with outcomes but not the basis for relying on them.

The Cognous discussion draft similarly frames the missing layer as portable decision evidence rather than raw data exchange. It describes this effort as an open, vendor-neutral record-format proposal, not a product announcement, and explicitly distinguishes the public record format from commercial implementations built around it. :contentReference[oaicite:0]{index=0}

---

## Core Design Principles

### 1. Record, not copy

The standard should not require movement of the underlying confidential data.

It should support hashes, references, attestations, commitments, and selectively disclosed fields.

### 2. Verifiable without trusting the issuer

A relying party should be able to check that a record was produced by an authorized source, has not been altered, and remains valid or invalid under defined freshness rules.

### 3. Portable across boundaries

The record should be consumable by a party that does not share the issuer’s internal systems.

### 4. Human and machine roles must be distinguishable

The record should distinguish between:

- human judgment;
- machine recommendation;
- machine execution;
- human override;
- nominal approval;
- constrained review;
- escalation;
- and non-review.

### 5. Model state matters

For AI-mediated decisions, the record should preserve enough information about the model, configuration, tools, runtime context, and authority state to make later review meaningful.

### 6. Authority must be time-bound

The record should capture whether the relevant human, system, agent, or organization had authority at the moment of decision, and whether that authority later expired, changed, or was revoked.

### 7. The record should fail closed

If required conditions are not met — wrong party, wrong purpose, expired record, revoked authority, unsupported verifier, prohibited jurisdiction, or unmet consumption condition — the record should not silently pass.

---

## Minimum Expressible Fields

A minimal portable decision evidence record should include fields in the following categories.

| Field | Purpose |
|---|---|
| `decision_id` | Identifies the decision being evidenced. |
| `decision_type` | Describes the class of decision: approval, denial, clearance, recommendation, override, escalation, etc. |
| `decision_timestamp` | Records when the decision occurred. |
| `issuer` | Identifies the organization, system, or agent that produced the record. |
| `authority` | Describes who or what had authority to decide, review, approve, execute, or override. |
| `machine_role` | Describes whether AI retrieved, recommended, assisted, executed, escalated, or generated the decision. |
| `model_state` | Captures model identity, version, configuration, tool access, and relevant runtime conditions. |
| `human_disposition` | Captures whether the human accepted, modified, rejected, escalated, overrode, or did not review the machine output. |
| `reliance_level` | Indicates the approximate degree to which the human relied on machine output. |
| `evidence_commitment` | Provides a hash, reference, or commitment to supporting evidence without exposing underlying data by default. |
| `policy_basis` | Identifies the rule, standard, policy, contract, regulation, or control framework applied. |
| `risk_coordinates` | Captures risk tier, jurisdictional class, prohibited-use flag, or other relevant coordinates. |
| `consumption_conditions` | Defines who may rely on the record, for what purpose, in what context, and until when. |
| `freshness_status` | Indicates whether the record is current, stale, expired, superseded, revoked, or pending revalidation. |
| `verification` | Provides the cryptographic seal, signature, key reference, conformance profile, or verifier endpoint. |

---

## Illustrative Example

This example is non-normative. It exists only to make the proposed vocabulary concrete.

```json
{
  "record_type": "portable_decision_evidence_record",
  "schema_version": "0.1",
  "decision_id": "example-decision-123",
  "decision_type": "ai_assisted_review",
  "decision_timestamp": "2026-07-01T14:30:00Z",
  "issuer": {
    "organization_id": "issuer-example",
    "system_id": "claims-review-system"
  },
  "authority": {
    "human_reviewer_role": "senior_claims_reviewer",
    "authority_basis": "internal_policy_reference",
    "authority_valid_at_decision": true
  },
  "machine_role": {
    "ai_used": true,
    "role": "recommendation",
    "model_id": "model-example",
    "model_version": "v1.2.3",
    "tool_access_profile": "restricted",
    "runtime_profile": "standard_review"
  },
  "human_disposition": {
    "status": "modified",
    "review_substantiveness": "substantive",
    "machine_reliance_level": "medium"
  },
  "evidence": {
    "evidence_commitment_type": "hash",
    "evidence_hash": "example_hash_value",
    "evidence_location": "held_by_issuer",
    "selective_disclosure_available": true
  },
  "policy_basis": [
    {
      "policy_id": "policy-example",
      "policy_version": "2026.06"
    }
  ],
  "risk_coordinates": {
    "risk_tier": "high",
    "jurisdiction": "example_jurisdiction",
    "restricted_use_flag": false
  },
  "consumption_conditions": {
    "permitted_relying_parties": ["authorized_counterparty"],
    "permitted_purposes": ["audit", "reliance_review", "regulatory_response"],
    "expires_at": "2026-08-01T00:00:00Z"
  },
  "status": {
    "freshness": "current",
    "superseded": false,
    "revoked": false
  },
  "verification": {
    "signature_type": "example_signature_method",
    "issuer_key_reference": "example_key_reference",
    "conformance_profile": "pder_v0_1_minimal"
  }
}
