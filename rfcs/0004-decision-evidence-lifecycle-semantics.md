# RFC 0004: Decision-Evidence Lifecycle Semantics

## Status

Discussion Draft

This RFC is part of a discussion draft for an open, vendor-neutral candidate standard. It is not a product announcement, legal advice, compliance advice, certification, assurance, or warranty. It has not been recognized, approved, adopted, or endorsed by any regulator or standards body.

## Purpose

This RFC defines conceptual lifecycle states and transitions for ODES records so issuers, verifiers, and relying parties can interpret status, freshness, expiration, supersession, revocation, and revalidation consistently.

An ODES record should not be treated as permanently valid merely because it was once issued. Decision evidence has a lifecycle.

## Scope

This RFC defines public, minimal interoperability semantics for interpreting lifecycle state in portable decision-evidence records.

The states in this RFC are conceptual semantics. They may map to existing status fields or future profiles. This RFC does not require schema changes.

## Non-goals

This RFC does not:

- define a lifecycle management platform;
- define a registry, endpoint, or evidence-store architecture;
- define policy-engine design or operational workflow orchestration;
- define commercial revalidation services;
- require disclosure of raw confidential evidence; or
- require a single status mechanism for every profile or sector.

## Lifecycle states

This RFC defines these conceptual lifecycle states:

- `current`;
- `stale`;
- `expired`;
- `superseded`;
- `revoked`;
- `pending_revalidation`;
- `revalidated`; and
- `unknown`.

`current` means the record is within its declared reliance window and no known status defect has been established under the applicable profile or verifier policy.

`stale` means the record may still be interpretable, but its freshness expectations are no longer satisfied without further confirmation.

`expired` means a declared time limit for reliance has been reached.

`superseded` means a newer record replaces or updates the prior record for the relevant decision or reliance purpose.

`revoked` means the record should no longer be accepted for the relevant reliance purpose.

`pending_revalidation` means current status cannot yet be established and revalidation has been requested or is otherwise required.

`revalidated` means a later status check has confirmed a new current status under the applicable profile or verifier policy.

`unknown` means current lifecycle state cannot be established from available information.

## Transition triggers

Possible lifecycle transition triggers include:

- expiration time reached;
- issuer revokes record;
- issuer supersedes record;
- underlying evidence changes;
- policy basis changes;
- authority window expires or changes;
- model version or runtime-relevant model state changes;
- relying-party purpose falls outside consumption conditions;
- verification material becomes unsupported or invalid;
- revalidation request is made; and
- revalidation succeeds or fails.

Profiles may define which triggers matter for a given assurance level, but this RFC treats them as conceptual triggers rather than mandatory platform events.

## Issuer responsibilities

Issuers should represent expiration, revocation, supersession, and revalidation status where applicable.

Issuers should avoid implying perpetual validity.

Issuers should preserve or publish enough status information for relying parties to distinguish current, stale, expired, superseded, and revoked records.

Issuers should provide replacement identifiers where records are superseded, when available.

Issuers should not require disclosure of raw confidential evidence unless a profile or bilateral arrangement requires it.

## Verifier responsibilities

Verifiers should evaluate lifecycle state according to the applicable profile and verifier policy.

Verifiers should not silently pass records with required but unknown freshness.

Verifiers should fail revoked records for prospective reliance.

Verifiers should fail expired records unless historical-review mode or profile rules permit otherwise.

Verifiers should identify superseded records and surface replacement references where available.

Verifiers may return `requires_revalidation` where current status cannot be established.

## Relying-party interpretation

Relying parties decide whether to rely under their own rules.

Lifecycle state informs reliance but does not force reliance.

A current record can still be rejected.

An expired or superseded record may still be relevant for historical audit.

A revoked record should not support prospective reliance unless a specific profile or legal context says otherwise.

## Supersession chains

Supersession means a newer record replaces or updates a prior record.

Supersession should preserve traceability to the prior record.

Replacement chains should avoid ambiguity where possible.

Supersession is not the same as revocation.

Where multiple replacement records exist, profiles or issuers should make the intended replacement path clear enough to avoid conflicting interpretations.

## Revocation semantics

Revocation means the issuer or authorized status source indicates the record should no longer be accepted for the relevant reliance purpose.

Revocation may result from error, changed evidence, authority defect, policy change, security compromise, or other status-invalidating event.

Revocation does not necessarily erase historical relevance.

## Revalidation semantics

Revalidation is a process by which status, freshness, authority, evidence commitment, or verification material is checked again.

Revalidation may return current, stale, expired, superseded, revoked, or unknown.

This RFC does not define a registry, endpoint, or commercial revalidation service.

## Historical review versus prospective reliance

Historical review asks what record existed, what status information was available, and what replacement or revocation events later occurred.

Prospective reliance asks whether the record should be accepted now for an active purpose.

These modes should not be collapsed. A record that is no longer acceptable for prospective reliance may still be relevant for audit, dispute review, or later analysis.

## Examples

1. **Record expires after permitted reliance window.** A record remains structurally valid, but its declared reliance period ends. The lifecycle state becomes `expired` for prospective reliance.
2. **Record superseded after policy update.** An issuer publishes a replacement record reflecting a new policy basis and marks the prior record as superseded with a replacement reference.
3. **Record revoked after evidence defect discovered.** A later review finds that a supporting evidence commitment was defective, and the issuer revokes the prior record for prospective reliance.
4. **Record pending revalidation because issuer key status cannot be confirmed.** A verifier cannot confirm whether the issuer key remains acceptable under the declared profile, so the record enters `pending_revalidation` or returns `requires_revalidation` until status can be checked again.

## Open questions

- Should lifecycle state transitions be normatively represented in future schema versions?
- Should profiles define required status-check mechanisms?
- How should offline verification handle freshness?
- Should supersession chains require canonical replacement references?
- How should audit-only review differ from reliance review?
