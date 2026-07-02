# PDER v0.1 Field Reference

| Field path | Type | Required? | Purpose | Notes |
| --- | --- | --- | --- | --- |
| `record_type` | string | Yes | Identifies the record type. | Must equal `portable_decision_evidence_record`. |
| `schema_version` | string | Yes | Identifies the schema version. | v0.1 allows `0.1`. |
| `decision_id` | string | Yes | Identifies the decision. | Issuer-assigned identifier. |
| `decision_type` | string | Yes | Names the decision category. | Free-form in v0.1. |
| `decision_timestamp` | string (`date-time`) | Yes | States when the decision occurred. | RFC 3339 date-time. |
| `issuer` | object | Yes | Groups issuer identity fields. | Core top-level object. |
| `issuer.organization_id` | string | No | Identifies the issuing organization. | Recommended for cross-boundary use. |
| `issuer.system_id` | string | No | Identifies the issuing system or service. | May represent an agentic system boundary. |
| `authority` | object | Yes | Groups authority coordinates. | Core top-level object. |
| `authority.human_reviewer_role` | string | No | Names the human reviewer or approver role. | Role, not personal identity. |
| `authority.authority_basis` | string | No | Describes the basis of authority. | Policy, delegation, contract, mandate, or similar. |
| `authority.authority_valid_at_decision` | boolean | No | Indicates whether authority was valid at decision time. | Useful for fail-closed verification. |
| `authority.authority_valid_from` | string (`date-time`) | No | Start of authority validity window. | Optional in v0.1. |
| `authority.authority_valid_until` | string (`date-time`) | No | End of authority validity window. | Optional in v0.1. |
| `machine_role` | object | Yes | Groups machine involvement fields. | Also carries model-state coordinates. |
| `machine_role.ai_used` | boolean | No | Indicates whether AI or automation was used. | `false` is valid for non-AI decisions. |
| `machine_role.role` | enum string | No | Describes the machine role. | One of `none`, `retrieval`, `recommendation`, `assistance`, `execution`, `escalation`, `generation`, `unknown`. |
| `machine_role.model_id` | string | No | Identifies the model or automated component. | Optional when `ai_used` is false. |
| `machine_role.model_version` | string | No | Identifies the model or component version. | Part of model-state coordinates. |
| `machine_role.tool_access_profile` | string | No | Describes tool or data access boundaries. | Useful for agentic or integrated systems. |
| `machine_role.runtime_profile` | string | No | Describes runtime context. | Useful for reproducibility and review. |
| `human_disposition` | object | Yes | Groups human review coordinates. | Core top-level object. |
| `human_disposition.status` | enum string | No | States the human disposition. | Values include `accepted`, `modified`, `rejected`, `overridden`, `escalated`, `not_reviewed`, `reviewed_under_constraint`, `unknown`. |
| `human_disposition.review_substantiveness` | enum string | No | Describes depth of human review. | Distinguishes substantive from nominal or constrained review. |
| `human_disposition.machine_reliance_level` | enum string | No | Indicates degree of machine reliance. | Corresponds to the reliance-level concept. |
| `evidence` | object | Yes | Groups evidence commitment fields. | Core top-level object. |
| `evidence.evidence_commitment_type` | enum string | No | States how evidence is referenced or committed. | One of `hash`, `reference`, `attestation`, `proof`, `none`, `unknown`. |
| `evidence.evidence_hash` | string | No | Stores a digest or similar commitment. | Only meaningful when commitment type supports it. |
| `evidence.evidence_location` | string | No | Describes where evidence is held or referenced. | May be descriptive rather than directly resolvable. |
| `evidence.selective_disclosure_available` | boolean | No | Indicates whether selective disclosure is supported. | Does not specify the mechanism. |
| `policy_basis` | array of objects | Yes | Lists policy or rule references. | Empty array is schema-valid but often not useful. |
| `policy_basis[].policy_id` | string | No | Identifies the policy, rule, or standard. | Recommended for profile-level use. |
| `policy_basis[].policy_version` | string | No | Identifies the cited version. | Optional in v0.1. |
| `policy_basis[].policy_type` | string | No | Identifies the kind of policy reference. | Examples: internal policy, contract, regulation. |
| `risk_coordinates` | object | Yes | Groups risk and jurisdiction coordinates. | Core top-level object. |
| `risk_coordinates.risk_tier` | enum string | No | States the risk tier. | One of `low`, `medium`, `high`, `critical`, `unknown`. |
| `risk_coordinates.jurisdiction` | string | No | Names the jurisdiction or context class. | Free-form in v0.1. |
| `risk_coordinates.restricted_use_flag` | boolean | No | Indicates additional restrictions on use. | Should be checked by verifiers. |
| `risk_coordinates.prohibited_use_flag` | boolean | No | Indicates the record should not be relied upon in some contexts. | Supports fail-closed behavior. |
| `consumption_conditions` | object | Yes | Groups reliance conditions. | Core top-level object. |
| `consumption_conditions.permitted_relying_parties` | array of strings | No | Lists authorized relying parties or classes. | Interpretation may be profile-specific. |
| `consumption_conditions.permitted_purposes` | array of strings | No | Lists authorized reliance purposes. | Supports purpose limitation. |
| `consumption_conditions.expires_at` | string (`date-time`) | No | States when the record expires for reliance. | Distinct from authority validity. |
| `status` | object | Yes | Groups current validity status. | Core top-level object. |
| `status.freshness` | enum string | No | States current freshness. | One of `current`, `stale`, `expired`, `superseded`, `revoked`, `pending_revalidation`, `unknown`. |
| `status.superseded` | boolean | No | Indicates whether a newer record replaces this one. | Should align with `superseded_by` where present. |
| `status.revoked` | boolean | No | Indicates whether the record has been revoked. | Should align with `revoked_at` where present. |
| `status.superseded_by` | string | No | Identifies the superseding record. | Optional linkage field. |
| `status.revoked_at` | string (`date-time`) | No | States when revocation occurred. | Optional in v0.1. |
| `verification` | object | Yes | Groups verification metadata. | Core top-level object. |
| `verification.signature_type` | string | No | Names the signature or verification method. | May be `none` in minimal cases. |
| `verification.issuer_key_reference` | string | No | Points to the issuer key or key reference. | Optional placeholder in minimal records. |
| `verification.conformance_profile` | string | No | Names the conformance profile claimed. | Example: `pder_v0_1_minimal`. |
| `verification.verifier_endpoint` | string (`uri`) | No | Provides an endpoint for verifier interaction. | Optional and not required for independent verification. |
