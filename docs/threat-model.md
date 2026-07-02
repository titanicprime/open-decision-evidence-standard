# Preliminary Threat Model

| Threat | Risk | Possible mitigation |
| --- | --- | --- |
| Issuer misrepresentation | A relying party may trust a record from the wrong organization or system. | Use strong issuer identifiers, key references, and independent verification checks. |
| Unauthorized issuer | An otherwise valid record may be created by an actor without authority to issue it. | Bind issuer identity to delegated authority and verify authorization context. |
| Stale authority | A person or system may appear authorized even though authority expired or changed. | Record authority validity windows and evaluate them at decision time and verification time. |
| Revoked record accepted as current | A revoked record may still circulate and be used. | Include revocation indicators and require verifiers to check freshness and revocation status. |
| Replay of old record | An old but once-valid record may be replayed in a different context. | Use expiry times, permitted purposes, relying-party constraints, and supersession markers. |
| Tampering | Record contents may be altered after issuance. | Use signatures, hashes, integrity checks, and fail-closed verification behavior. |
| Evidence hash mismatch | A commitment may not match the evidence later disclosed. | Define stable commitment semantics and verify commitments against disclosed evidence artifacts. |
| Leakage through metadata | Sensitive facts may leak from identifiers, policy names, or timestamps. | Minimize sensitive metadata, profile field use, and support privacy review of example patterns. |
| Over-disclosure | Issuers may disclose more evidence than necessary. | Encourage selective disclosure, purpose limitation, and profile-specific disclosure guidance. |
| Verifier endpoint spoofing | A relying party may contact a malicious endpoint that returns false verification results. | Authenticate verifier endpoints, prefer independent verification where possible, and avoid blind reliance on endpoint output. |
| Malicious relying-party use | A record may be used for an unauthorized purpose or by an unauthorized recipient. | Include permitted parties and purposes, and require verifiers to check them before reliance. |
| Conformance fraud | An issuer may claim profile conformance without meeting the profile. | Publish public conformance requirements and require explicit pass/fail reasons from verifiers. |
| Model-state ambiguity | Record consumers may misunderstand how a model influenced the decision. | Record machine role, model identifiers, runtime profile, and human disposition clearly. |
| Human-review mischaracterization | A nominal or constrained review may be presented as substantive oversight. | Distinguish review substantiveness from decision status and machine reliance level. |
| Cross-jurisdiction misuse | A record may be reused in a jurisdiction or context where it should not apply. | Record jurisdiction and restricted or prohibited use flags and require downstream policy checks. |
