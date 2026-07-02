# Design Principles

## 1. Record, not copy

**Rationale:** Cross-boundary evidence sharing should not require underlying confidential data to move by default.

**Implications:** The format should support commitments, references, attestations, and selective disclosure patterns rather than assuming a full evidence payload is exported.

## 2. Supports verification without blind trust in the issuer

**Rationale:** A relying party needs more than an issuer's assertion that a decision was valid.

**Implications:** The record should support integrity checks, issuer identification, key references, freshness checks, and revocation or supersession indicators that can be evaluated independently.

## 3. Portable across organizational boundaries

**Rationale:** The format should remain useful when the relying party does not share systems, workflows, or operating assumptions with the issuer.

**Implications:** The record should use a stable, machine-readable structure and avoid coupling to a single product, ledger, or trust network.

## 4. Human and machine roles must be distinguishable

**Rationale:** Reviewers need to know whether a human exercised judgment, merely acknowledged machine output, or did not review the matter at all.

**Implications:** The format should distinguish machine role, human disposition, and machine reliance level so downstream users can apply their own governance thresholds.

## 5. Model state matters

**Rationale:** AI-mediated decisions can depend materially on the model version, configuration, runtime context, and tool access in effect at decision time.

**Implications:** The record should preserve enough model-state coordinates to make later review meaningful without requiring the full underlying system state to be exported.

## 6. Authority must be time-bound

**Rationale:** A decision can become harder to rely on if the authority of a person, system, or delegated agent was invalid, expired, or later revoked.

**Implications:** The record should capture authority basis and validity windows, and verifiers should be able to consider time-bound authority when determining whether reliance is appropriate.

## 7. Fail closed

**Rationale:** Missing or contradictory conditions should not silently result in a positive reliance outcome.

**Implications:** If verification fails, the relying party is unauthorized, the purpose is not permitted, the record is expired, or freshness cannot be established, the default outcome should be rejection or explicit revalidation rather than implicit acceptance.
