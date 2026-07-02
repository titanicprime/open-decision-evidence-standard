# PDER v0.1 Minimal Conformance Profile

A record satisfies the `pder_v0_1_minimal` profile only if it is schema-valid and also meets this profile's additional expectations. A record may be schema-valid and still fail profile conformance or verifier acceptance.

A conforming minimal record must:

- identify the decision;
- identify the issuer;
- state the decision type and timestamp;
- include authority information;
- distinguish human and machine roles;
- include evidence commitment or explicitly state none;
- include consumption conditions;
- include freshness status;
- include verification method or explicitly state none;
- be machine-readable JSON; and
- validate against `schema/pder-v0.1.schema.json`.

Schema validity means the record conforms to the base JSON structure. Profile conformance means the record satisfies the named `pder_v0_1_minimal` requirements layered onto that structure. Verifier acceptance means a relying party determines the record is acceptable for a specific purpose, party, time, freshness state, and consumption condition.

A record may be schema-valid and still fail verifier acceptance because it is expired, revoked, stale, outside the permitted purpose, outside the permitted relying party, or otherwise unsuitable for reliance.

The minimal profile is intended to define the smallest discussion-draft record that is still portable and reviewable across boundaries.
