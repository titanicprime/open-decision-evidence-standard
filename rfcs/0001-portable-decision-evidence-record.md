# RFC 0001: Portable Decision Evidence Record

- **RFC number:** 0001
- **Title:** Portable Decision Evidence Record
- **Status:** Draft
- **Proposed by:** Cognous
- **Date:** July 2026

Draft status note: This document is part of a discussion draft for an open, vendor-neutral candidate standard. It is not a product announcement, legal advice, compliance advice, certification, assurance, or warranty.

## Abstract

This RFC proposes a portable decision evidence record for AI-mediated and cross-boundary decisions. The goal is to define an open, vendor-neutral, freely implementable format for carrying decision evidence coordinates without requiring confidential underlying data, shared infrastructure, or proprietary trust networks.

## Problem

Decision outcomes often cross boundaries without the supporting evidence needed for later reliance, review, or challenge. AI increases the speed, scale, and opacity of this problem, especially where model state, delegated automation, and uneven human review complicate downstream interpretation.

## Goals

- define a compact portable decision evidence record;
- distinguish human and machine roles;
- preserve authority, evidence, policy, and freshness coordinates;
- support selective disclosure and confidentiality; and
- enable open conformance work across independent implementations.

## Non-goals

- creating a shared ledger by default;
- standardizing a universal workflow engine;
- replacing legal, audit, regulatory, or sector-specific standards;
- requiring raw evidence disclosure; or
- defining proprietary product architecture.

## Minimal record structure

The proposed minimal record structure includes record identity, decision identity, issuer, authority, machine role, human disposition, evidence commitment, policy basis, risk coordinates, consumption conditions, current status, and verification metadata.

Schema validation in this draft checks structure only. It does not establish that the underlying decision is correct, lawful, complete, or suitable for reliance.

## Open questions

- Which verification profiles should be standardized first?
- How much issuer and system identity should be mandatory in regulated contexts?
- Which selective-disclosure mechanisms are practical across jurisdictions?
- How should revocation and supersession be represented across offline and online verification models?

## Security considerations

Security concerns include issuer impersonation, stale authority, replay, tampering, signature confusion, endpoint spoofing, and false conformance claims. The draft favors fail-closed verification and explicit freshness indicators.

## Privacy considerations

The record should carry coordinates, not conclusions, and should not require full evidence disclosure by default. Selective disclosure and data minimization should remain central design goals.

## Conformance considerations

Conformance should be profile-based. The base schema should remain modest, while profiles may raise requirements for sectors, deployment models, or assurance levels. A schema-valid record may still fail profile conformance, verifier acceptance, or a relying party's decision to rely.

## Next steps

Next steps include public comment, independent implementation feedback, review of related standards, refinement of terminology and threat assumptions, and iteration toward clearer governance and conformance expectations.
