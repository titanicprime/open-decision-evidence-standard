# Verifier Requirements

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

This repository does not provide production verifier code. The intent is to describe expected verifier behavior for an open record format.
