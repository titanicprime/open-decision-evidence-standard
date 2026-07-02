# Selective Disclosure

The standard should not require all supporting evidence to be exposed in every exchange. A portable decision evidence record should enable verification and controlled reliance without assuming that raw evidence moves with the record.

Different relying parties may receive different views. One party may receive only a commitment and basic policy references, while another may receive references, attestations, or more detailed disclosed materials under a narrower purpose and authority basis.

Evidence commitments may take the form of hashes, references, attestations, or proofs. The record should identify what is disclosed, what is committed, and what remains with the issuer.

The draft therefore favors a structure in which the record can point to evidence and describe disclosure availability without assuming a single privacy model or a single technical proof mechanism.

## Open questions

- Which privacy-preserving proof mechanisms are mature enough for profile-level adoption?
- How should selective disclosure interact with jurisdiction-specific data minimization requirements?
- When should verifier access to supporting evidence be direct, delegated, or prohibited?
- How should revocation, supersession, or freshness changes affect previously disclosed views?
