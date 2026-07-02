# Verifier Requirements

Schema validity means the record conforms to the base JSON structure. Profile conformance means the record satisfies a named conformance profile such as `pder_v0_1_minimal`. Verifier acceptance means the record is acceptable for a specific relying party, purpose, time, freshness state, and consumption condition.

A conceptual verifier for PDER v0.1 should:

1. parse the record;
2. validate the record against the schema;
3. verify `record_type` and `schema_version`;
4. check signature material or an explicit verification placeholder;
5. check expiration;
6. check freshness;
7. check the revocation flag;
8. check the permitted relying party;
9. check the permitted purpose;
10. check any required conformance profile; and
11. return pass/fail with reasons.

A record may be schema-valid and still fail verifier acceptance because it is expired, revoked, stale, outside the permitted purpose, outside the permitted relying party, or otherwise unsuitable for reliance.

Schema validation checks structure. It does not establish that the underlying decision is correct, lawful, complete, or suitable for reliance.

This repository does not provide production verifier code. The intent is to describe expected verifier behavior for an open record format.
