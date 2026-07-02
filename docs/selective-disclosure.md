# Selective Disclosure

Draft status note: This document is part of a discussion draft for an open, vendor-neutral candidate standard. It is not a product announcement, legal advice, compliance advice, certification, assurance, or warranty.

The standard should not require all supporting evidence to be exposed in every exchange. A portable decision evidence record should enable verification and controlled reliance without assuming that raw evidence moves with the record.

Different relying parties may receive different views. One party may receive only a commitment and basic policy references, while another may receive references, attestations, or more detailed disclosed materials under a narrower purpose and authority basis.

Evidence commitments may take the form of hashes, references, attestations, or proofs. The record should identify what is disclosed, what is committed, and what remains with the issuer.

The draft therefore favors a structure in which the record can point to evidence and describe disclosure availability without assuming a single privacy model or a single technical proof mechanism. v0.1 does not claim to solve selective disclosure fully. It only identifies draft metadata and design questions that later profiles or extensions may refine.

## Open Questions

- What privacy-preserving proof mechanisms, if any, should be referenced or profiled by the standard?
- How should the standard distinguish between disclosed evidence, committed evidence, and externally held evidence?
- How should jurisdiction-specific privacy, banking, insurance, health, employment, and security rules affect selective disclosure?
- How should relying parties verify that undisclosed evidence exists without gaining unauthorized access to it?
- What metadata creates unacceptable inference risk even when underlying evidence is not disclosed?
