# UPIF Conformance Specification

**Version:** 1.0  
**Date:** April 18, 2025  
**Author:** Roshan George Thomas, XWHYZ  
**DOI:** [10.5281/zenodo.15242693](https://doi.org/10.5281/zenodo.15242693)  
**Status:** Active

---

## Overview

This document defines conformance requirements for implementations of the Unified Prompt Intelligence Framework (UPIF). It specifies what it means for a system, platform, or tool to claim UPIF compliance across three conformance tiers.

UPIF is a modular, seven-layer protocol. Conformance is layer-scoped — implementations may adopt individual layers independently without implementing the full stack, provided they meet the requirements defined for each adopted layer.

---

## Conformance Tiers

### Tier 1 — Minimal Conformance

A system achieves Minimal Conformance by implementing **at least one** of the seven UPIF layers in full accordance with the layer requirements defined in this document.

Minimal Conformance is appropriate for:
- Single-purpose tools (e.g. a compliance firewall plugin)
- Experimental or proof-of-concept implementations
- SDK modules targeting a single layer

A Minimal Conformant implementation **must**:
- Implement all MUST-level requirements for the adopted layer(s)
- Correctly handle prompt metadata according to the UPIF JSON schema (Appendix A of the whitepaper)
- Not claim full or partial UPIF conformance for unadopted layers

### Tier 2 — Partial Conformance

A system achieves Partial Conformance by implementing **three or more** UPIF layers, including L4 (Attribution Ledger) as a mandatory component.

L4 is mandatory at this tier because authorship tracking is the minimum auditable signal required to distinguish UPIF-governed prompts from ungoverned ones.

A Partial Conformant implementation **must**:
- Meet all MUST-level requirements for each adopted layer
- Implement L4 in full
- Produce UPIF-compliant prompt metadata objects for all governed prompts
- Expose a mechanism for downstream systems to verify prompt provenance

### Tier 3 — Full Conformance

A system achieves Full Conformance by implementing all seven UPIF layers in accordance with this specification.

Full Conformance is the target for:
- Enterprise AI governance platforms
- Multi-modal content generation pipelines
- Regulated-industry AI deployments (healthcare, legal, government)
- Platforms seeking UPIF certification or licensing

A Full Conformant implementation **must**:
- Meet all MUST-level and SHOULD-level requirements for all seven layers
- Produce, store, and expose complete prompt metadata objects
- Support revision history and contributor attribution across the full prompt lifecycle
- Pass all test cases defined in the UPIF conformance test suite (forthcoming in v1.1)

---

## Layer-by-Layer Requirements

### L1 — Co-Prompting Interface

**Purpose:** Enable multi-user, real-time collaborative prompt authoring with version control and role-based access.

| Requirement | Level | Description |
|---|---|---|
| Multi-user sessions | MUST | Support two or more simultaneous contributors to a single prompt |
| Role differentiation | MUST | Distinguish at minimum between author and reviewer roles |
| Version control | MUST | Maintain a revision history with contributor UID and timestamp per revision |
| Conflict resolution | SHOULD | Provide a defined strategy for concurrent edits |
| Access control | SHOULD | Support permission scoping per contributor role |
| Real-time sync | MAY | Provide live synchronization of prompt state across contributors |

---

### L2 — Cross-Modal Router

**Purpose:** Route prompts across modalities — text, image, audio, video, and code — with appropriate transformation metadata.

| Requirement | Level | Description |
|---|---|---|
| Modality declaration | MUST | Every routed prompt must declare its source and target modality |
| Routing metadata | MUST | Attach routing decision and target modality to prompt metadata object |
| Text support | MUST | Support text-to-text routing at minimum |
| Multi-modal support | SHOULD | Support at least two of: image, audio, video, code |
| Fallback handling | MUST | Define behavior when target modality is unavailable |
| Transformation log | SHOULD | Record modality transitions in the prompt revision history |

---

### L3 — Personalization Engine

**Purpose:** Adapt prompt structure and content dynamically based on user context, profile, and interaction history.

| Requirement | Level | Description |
|---|---|---|
| Context signals | MUST | Accept at minimum user role and session context as personalization inputs |
| Policy alignment | MUST | Personalization must not override compliance or safety constraints from L5 |
| Signal transparency | MUST | Declare which signals influenced prompt adaptation in metadata |
| Sensitive data exclusion | MUST | Must not use PII, biometric, or health data as personalization signals without explicit consent |
| Reinforcement input | SHOULD | Support feedback signals from L7 to improve personalization over time |
| Profile portability | MAY | Support import/export of user profiles in a standard format |

---

### L4 — Attribution Ledger

**Purpose:** Track authorship, versioning, and revision history for every governed prompt using unique identifiers and hash functions.

> **Note:** L4 is mandatory for Tier 2 and Tier 3 conformance.

| Requirement | Level | Description |
|---|---|---|
| Unique prompt ID | MUST | Assign a globally unique identifier (UID) to every prompt |
| SHA-256 hash | MUST | Generate and store a SHA-256 hash of prompt content at each revision |
| Contributor attribution | MUST | Record the UID of every contributor per revision |
| Timestamp | MUST | Record an ISO 8601 timestamp for each revision |
| Revision chain | MUST | Maintain an ordered, append-only revision history |
| Immutability | MUST | Revision records must not be modifiable after creation |
| Blockchain anchoring | MAY | Optionally anchor hashes to a distributed ledger for legal-grade timestamping |

**Minimum metadata object per revision:**
```json
{
  "prompt_id": "upif-{uid}",
  "revision": 1,
  "contributor_uid": "user-{uid}",
  "timestamp": "2025-04-18T00:00:00Z",
  "content_hash": "sha256:{hash}",
  "modality": "text",
  "parent_revision": null
}
```

---

### L5 — Compliance Firewall

**Purpose:** Screen and evaluate prompts against ethical, legal, and organizational policies before execution.

| Requirement | Level | Description |
|---|---|---|
| Pre-inference evaluation | MUST | All policy checks must occur before the prompt reaches a model API |
| Policy rule format | MUST | Rules must be declarative and inspectable (not opaque ML classifiers alone) |
| Block/allow decision | MUST | Every prompt must receive an explicit pass or block decision |
| Block reason logging | MUST | Blocked prompts must record the triggering rule and reason |
| GDPR flag support | SHOULD | Support evaluation against GDPR-relevant content signals |
| COPPA flag support | SHOULD | Support evaluation against age-appropriate content signals |
| HIPAA flag support | SHOULD | Support evaluation against health information signals |
| Custom rule packs | SHOULD | Allow organizations to define and load custom policy rule sets |
| Override mechanism | MAY | Allow authorized roles to override a block with logged justification |

---

### L6 — Tone / Brand Governor

**Purpose:** Enforce stylistic, tonal, and brand-aligned communication consistency within the prompt structure.

| Requirement | Level | Description |
|---|---|---|
| Tone profile definition | MUST | Support at least one named tone profile (e.g. formal, friendly, academic) |
| Pre-inference enforcement | MUST | Tone evaluation must occur before prompt execution, not post-output |
| Profile attribution | MUST | Record which tone profile was applied in prompt metadata |
| Conflict handling | MUST | Define behavior when prompt content conflicts with active tone profile |
| Multi-profile support | SHOULD | Support multiple simultaneous tone profiles with priority ordering |
| Brand vocabulary | SHOULD | Support allowlists and blocklists of brand-specific terminology |
| Profile inheritance | MAY | Allow tone profiles to inherit from parent profiles |

---

### L7 — Feedback Loop

**Purpose:** Capture and integrate feedback from users, evaluators, and system metrics to refine prompt structures over time.

| Requirement | Level | Description |
|---|---|---|
| Feedback capture | MUST | Accept explicit feedback signals (e.g. accept, reject, revise) per prompt |
| Feedback attribution | MUST | Attribute each feedback signal to a contributor UID and timestamp |
| Feedback linkage | MUST | Link feedback records to the specific prompt UID and revision |
| Loop closure | SHOULD | Feed aggregated feedback signals back to L3 (Personalization Engine) |
| Metric tracking | SHOULD | Track quantitative metrics (e.g. acceptance rate, revision count) per prompt type |
| Audit trail | MUST | Feedback records must be append-only and non-modifiable |
| Aggregation API | MAY | Expose an API for downstream analytics over feedback data |

---

## Metadata Schema

All UPIF-conformant implementations must produce prompt metadata objects compatible with the following base schema. Additional fields may be added; defined fields must not be renamed or removed.

```json
{
  "prompt_id": "string — globally unique identifier",
  "author_uid": "string — original author identifier",
  "timestamp": "string — ISO 8601 creation timestamp",
  "modality": "string — one of: text, image, audio, video, code",
  "intent_tags": ["array of strings — optional semantic tags"],
  "tone_profile": "string — active tone profile name",
  "compliance_flags": {
    "gdpr_safe": "boolean",
    "coppa_compliant": "boolean",
    "hipaa_safe": "boolean"
  },
  "revision_history": [
    {
      "rev": "integer — revision number",
      "contributor_uid": "string",
      "timestamp": "string — ISO 8601",
      "content_hash": "string — SHA-256 hash of prompt content at this revision"
    }
  ],
  "routing": {
    "source_modality": "string",
    "target_modality": "string",
    "router_decision": "string — pass or block"
  },
  "compliance_result": {
    "decision": "string — pass or block",
    "triggered_rule": "string or null",
    "evaluated_at": "string — ISO 8601"
  }
}
```

---

## Claiming Conformance

Implementations claiming UPIF conformance must:

1. Specify the conformance tier (Minimal, Partial, or Full)
2. List the specific layers implemented
3. Reference this document and version: `UPIF Conformance Specification v1.0`
4. Link to the canonical specification: `https://doi.org/10.5281/zenodo.15242693`

**Example conformance statement:**

> This implementation is Partial UPIF Conformant (v1.0), implementing layers L1, L4, and L5 in accordance with the UPIF Conformance Specification v1.0 (https://doi.org/10.5281/zenodo.15242693).

---

## Terminology

| Term | Definition |
|---|---|
| MUST | Absolute requirement. Non-conformance disqualifies the conformance claim for that layer. |
| SHOULD | Strongly recommended. Non-conformance must be documented with justification. |
| MAY | Optional. Implementations may include or omit at their discretion. |
| Prompt | A structured input artifact governed by the UPIF lifecycle. |
| UID | Unique identifier — any format that guarantees global uniqueness (UUID v4 recommended). |
| Governed prompt | A prompt that has passed through at least one UPIF layer and carries UPIF metadata. |

---

## Versioning

This conformance specification follows semantic versioning. Breaking changes to MUST-level requirements increment the major version. Additive changes increment the minor version.

| Version | Date | Notes |
|---|---|---|
| 1.0 | April 18, 2025 | Initial release |

---

## License

This specification is released under the same license as the UPIF repository. See [LICENSE](./LICENSE) for details.

---

*UPIF is developed and maintained by Roshan George Thomas / XWHYZ. For questions or conformance inquiries, open an issue at https://github.com/XwhyZ-WHYLD/upif-specs*
