# RFC 0003: Verifier Behavior and Reliance Boundaries

## Status

Discussion Draft

This RFC is part of a discussion draft for an open, vendor-neutral candidate standard. It is not a product announcement, legal advice, compliance advice, certification, assurance, or warranty. It has not been recognized, approved, adopted, or endorsed by any regulator or standards body.

## Purpose

This RFC defines the conceptual behavior expected of an ODES verifier and clarifies the boundary between schema validity, profile conformance, verifier acceptance, and relying-party reliance.

ODES distinguishes four layers that should not be collapsed:

1. Schema validity: the record is structurally valid against the applicable ODES schema.
2. Profile conformance: the record satisfies the rules of its declared conformance profile.
3. Verifier acceptance: a verifier has evaluated the record and its declared verification material according to a stated verifier policy.
4. Relying-party reliance: the receiving party decides, under its own rules and context, whether to rely, request more evidence, reject, or escalate.

Verifier acceptance does not establish that the underlying decision was correct, lawful, complete, fair, unbiased, regulator-approved, or suitable for reliance in every context. A verifier evaluates the record, not the world.

## Scope

This RFC defines minimal interoperability semantics for public ODES verifiers. It describes what a verifier should check, how it should report outcomes, and how verifier results relate to relying-party decisions.

This RFC is limited to the portable decision-evidence record and its declared verification material. It does not require shared infrastructure, confidential evidence disclosure, or proprietary trust arrangements.

## Non-goals

This RFC does not:

- define production verifier architecture;
- define a registry, routing layer, or evidence-store design;
- define a policy engine or relying-party workflow;
- define authority scoring, admissibility scoring, or trust scoring;
- define a commercial verifier service;
- define a cryptographic selective-disclosure protocol; or
- require a verifier to prove that the represented decision process actually occurred as described.

## Verification layers

Schema validity checks whether a record conforms to the applicable ODES schema version.

Profile conformance checks whether the record satisfies the requirements of its declared profile.

Verifier acceptance checks whether the record and its declared verification material satisfy the verifier's stated policy for the relevant use mode.

Relying-party reliance is a separate decision. A relying party may accept a verifier output, request more evidence, reject the record, or escalate review.

## Required verifier checks

A conforming conceptual verifier should evaluate at least the following, subject to the applicable profile and verifier policy:

- schema validity;
- declared schema version;
- declared conformance profile;
- required field presence;
- signature or verification metadata presence, if required by profile;
- issuer identity or issuer key reference, if present or required;
- authority validity window, if present or required;
- evidence commitment presence, type, and reference integrity;
- status freshness;
- expiration;
- revocation;
- supersession;
- permitted relying party;
- permitted purpose;
- jurisdiction or use restrictions; and
- unsupported profile or unsupported verification material.

Where a required condition cannot be evaluated, the verifier should fail closed unless the applicable profile explicitly permits warning or partial acceptance.

## Optional verifier checks

A verifier may also evaluate additional checks when the profile or verifier policy calls for them, including:

- consistency between declared issuer identity and verification material;
- consistency between policy identifiers and declared decision context;
- internal consistency among timestamps, authority windows, and status fields;
- additional consumption-condition checks beyond party, purpose, and jurisdiction; and
- profile-specific evidence-commitment or attestation checks.

Optional checks should be reported as optional so they are not confused with universal ODES baseline semantics.

## Failure, warning, and revalidation semantics

A verifier should be able to return these conceptual outcomes:

- `pass`: required verifier checks passed under the stated verifier policy;
- `warn`: the record may be structurally usable but has unresolved limitations;
- `fail`: the record should not be accepted under the stated verifier policy; and
- `requires_revalidation`: freshness, revocation, supersession, or authority status requires current confirmation before acceptance.

A `warn` outcome may be appropriate where the record is schema-valid and partially interpretable but the verifier encounters limitations that the applicable profile explicitly allows to remain non-fatal.

A `fail` outcome is appropriate where required checks do not pass, where required verification material is missing or invalid, or where prohibited use conditions are triggered.

A `requires_revalidation` outcome is appropriate where current status cannot be established with enough confidence for acceptance, even though the record may otherwise be structurally valid.

## Freshness, expiration, revocation, and supersession

Expired records should fail unless the applicable profile permits historical review.

Revoked records should fail for prospective reliance.

Superseded records should point to replacement records where available.

Stale records should require revalidation or warning depending on profile.

Unknown freshness should not silently pass where freshness is required.

If freshness, revocation, supersession, or authority status depends on current confirmation that cannot be obtained, the verifier should return `requires_revalidation` or `fail` according to the applicable profile and verifier policy.

## Consumption-condition checks

A verifier should evaluate declared consumption conditions relevant to acceptance, including permitted relying party, permitted purpose, and jurisdiction or use restrictions.

A verifier may determine that a record is otherwise well-formed yet still not acceptable for the requested use because the relying party, purpose, or jurisdiction falls outside the record's declared bounds.

Consumption-condition checks inform verifier acceptance. They do not compel relying-party reliance, which remains a separate decision.

## Handling missing, unsupported, and unknown fields

If a required field is missing, the verifier should fail.

If a declared profile or verification material type is unsupported, the verifier should fail or return `warn` only where the applicable profile explicitly permits partial acceptance.

Unknown fields should not by themselves cause failure unless the profile prohibits them or they prevent correct interpretation of required semantics.

A verifier should distinguish between missing information, unknown information, and unsupported mechanisms in its output.

## Selective-disclosure commitments

Selective disclosure commitments may indicate that supporting evidence exists without disclosing the evidence itself. A verifier may check the presence, format, and declared commitment type, but full disclosure validation depends on the applicable profile and implementation. This RFC does not define a cryptographic disclosure protocol.

## Verifier output

Verifier output should identify:

- the verifier outcome;
- the checks performed;
- the verifier policy or policy identifier, if available;
- the reasons for any warning, failure, or revalidation requirement; and
- any unresolved limitations, including unsupported profile elements or unknown status conditions.

This RFC does not require a canonical wire format for verifier output.

## Relying-party reliance

A relying party decides whether to rely under its own rules, legal context, risk posture, and operational needs.

A verifier result may inform that decision, but it does not replace it. A relying party may reject a verifier-accepted record, require more evidence, or escalate review.

Verifier acceptance does not establish that the underlying decision was correct, lawful, complete, fair, unbiased, regulator-approved, or suitable for reliance in every context. A verifier evaluates the record, not the world.

## Examples

1. **Schema-valid but expired record.** A record validates against the schema and satisfies its declared profile, but `expires_at` has passed. The verifier should return `fail` for prospective reliance unless the profile permits historical review mode.
2. **Schema-valid and profile-conforming record with unsupported verifier material.** A record is structurally valid and meets profile field requirements, but the verifier does not support the declared signature or verification material type. The verifier should return `fail` or `warn` only if the profile explicitly permits partial acceptance.
3. **Verifier-accepted record that relying party still rejects.** A verifier returns `pass`, but the relying party determines that the requested use does not match the record's permitted purpose. The relying party rejects or escalates despite verifier acceptance.

## Open questions

- Which checks belong in minimal profile vs higher-assurance profiles?
- Should verifier output have a canonical JSON form?
- How should verifier policies be identified?
- Should revocation checks be profile-specific?
- How should historical audit review differ from prospective reliance?
