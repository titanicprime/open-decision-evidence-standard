# Terminology

- **AIBOM**: An AI bill of materials describing what an AI system is, including components, dependencies, lineage, lifecycle context, and supply-chain properties.
- **decision evidence**: Information that helps explain and evaluate how a decision was made and whether it may be relied upon.
- **portable decision evidence record**: A machine-readable record that carries decision evidence coordinates across organizational, system, or jurisdictional boundaries.
- **related-work distinction**: A positioning note that neighboring governance, provenance, and system-description artifacts solve different problems from portable decision evidence records.
- **issuer**: The organization or system that creates and signs or otherwise publishes the record.
- **relying party**: A party that receives the record and determines whether and how to rely on it.
- **decision subject**: The person, entity, transaction, document, case, or process affected by the decision.
- **decision outcome**: The disposition, result, or action produced by the decision process.
- **human disposition**: The recorded human response to machine output or to the decision itself, such as acceptance, modification, rejection, or escalation.
- **machine role**: The role played by automation or AI in the decision path, such as retrieval, recommendation, assistance, execution, or generation.
- **model state**: Identifying and operational coordinates for the model and runtime context relevant to the decision.
- **evidence commitment**: A compact reference to supporting evidence, such as a hash, pointer, attestation, or other verification material, used without exposing all evidence by default.
- **policy basis**: The rules, controls, standards, contracts, or policies cited as the basis for the decision.
- **risk coordinates**: High-level descriptors that help downstream users understand risk tier, jurisdiction, and restricted or prohibited uses.
- **consumption condition**: A constraint on who may rely on the record, for what purpose, in what context, or until what time.
- **freshness**: The current validity status of the record for reliance purposes.
- **expiration**: A state in which the record should no longer be relied upon after a stated time limit.
- **supersession**: A state in which a newer record replaces an older record for the same decision or reliance purpose.
- **revocation**: A state in which the issuer or authorized authority withdraws the record from use.
- **verification**: The process of checking structure, issuer identity, integrity, status, and conformance conditions.
- **conformance profile**: A named set of additional requirements layered onto the base schema for a given use case or sector.
- **selective disclosure**: A pattern in which different relying parties receive different subsets or verification material derived from underlying evidence based on need and authorization.
- **fail closed**: A design posture in which unmet requirements result in rejection or revalidation rather than silent acceptance.

AIBOMs describe what the AI system is. ODES describes the decision evidence associated with a particular AI-influenced decision.

## Portable decision-evidence record

A structured record that carries decision evidence across organizational, system, or jurisdictional boundaries.

## Decision-evidence container

A plain-English description of the portable decision-evidence record: a container for governance coordinates, not conclusions.

## Governance coordinates

The structured facts a relying party may evaluate, including authority, machine role, human disposition, model state, policy basis, evidence commitments, freshness, revocation, and consumption conditions.

## Governed artifact

A decision represented with sufficient structured context that another party can evaluate it after it crosses a boundary.

## Record, not copy

The design principle that underlying confidential evidence need not move if the record can carry commitments, references, attestations, verification metadata, and disclosure coordinates.

## Coordinates, not conclusions

The design principle that the record gives relying parties structured information for evaluation, but does not force reliance or prove correctness.
