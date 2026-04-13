# Unified Prompt Intelligence Framework (UPIF)

**UPIF defines a missing layer in the generative AI stack:  
governance of prompts *before* model execution.**

Where existing systems optimize outputs, UPIF governs intent.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15242693.svg)](https://doi.org/10.5281/zenodo.15242693)
[![License](https://img.shields.io/github/license/XwhyZ-WHYLD/upif-specs)](./LICENSE)
[![Version](https://img.shields.io/badge/version-1.0-blue)](https://github.com/XwhyZ-WHYLD/upif-specs/releases/tag/v1.0)

---

## What UPIF Is

UPIF is a **protocol-level specification** for treating prompts as
first-class, auditable, and governed digital artifacts.

It formalizes how prompts are:

- Authored collaboratively
- Attributed to contributors
- Evaluated for policy and compliance
- Governed for tone and context
- Refined prior to AI execution

UPIF operates **before inference**, independent of any specific model,
vendor, or runtime.

---

## What UPIF Is Not

UPIF is **not**:

- A prompt library
- A model wrapper
- A post-output moderation tool
- A proprietary platform

UPIF does **not** generate content.  
It governs the *inputs* that generate content.

---

## Why Prompt Governance Now

As generative AI adoption accelerates, prompts have become:

- A source of intellectual property
- A compliance and regulatory liability
- A vector for brand, safety, and attribution risk
- A blocker to enterprise and institutional adoption

Yet most AI systems still treat prompts as ephemeral strings.

UPIF addresses this gap by introducing **governance-before-generation**:
a structured, auditable lifecycle for prompts prior to model execution.

---

## Core Architecture

UPIF defines a **seven-layer orchestration model**, each layer modular and
independently adoptable:

1. **L1 — Co-Prompting Interface**  
   Multi-user collaborative prompt authoring with version control and role-based access.

2. **L2 — Cross-Modal Router**  
   Routes prompts across modalities: text, image, audio, video, and code.

3. **L3 — Personalization Engine**  
   Context-aware adaptation using policy-aligned, non-sensitive signals.

4. **L4 — Attribution Ledger**  
   Records authorship, revision history, timestamps, and SHA-256 content hashes for every governed prompt.

5. **L5 — Compliance Firewall**  
   Evaluates prompts against legal, ethical, and organizational policies before execution. Supports GDPR, COPPA, and HIPAA signal flags.

6. **L6 — Tone / Brand Governor**  
   Enforces stylistic, academic, or brand-aligned communication consistency within the prompt structure.

7. **L7 — Feedback Loop**  
   Captures feedback from users, evaluators, and system metrics to refine prompt structures over time.

All seven layers are modular, conditionally triggerable, and independently adoptable.

---

## Repository Structure

```
upif-specs/
├── IP/                  — IP declarations and priority documentation
├── diagrams/            — Architecture and flow diagrams
├── docs/                — Extended documentation
├── schemas/             — UPIF JSON metadata schema
├── ARCHITECTURE.md      — Detailed layer architecture
├── CITATION.cff         — Citation metadata
├── CONFORMANCE.md       — Conformance tiers and layer requirements
├── LICENSE              — License terms
├── ROADMAP.md           — Development roadmap
└── SPEC.md              — Full protocol specification
```

---

## Conformance

UPIF supports three conformance tiers — Minimal, Partial, and Full — allowing implementations to adopt individual layers without requiring full-stack implementation.

See [CONFORMANCE.md](./CONFORMANCE.md) for layer-by-layer requirements, metadata schema, and instructions for claiming conformance.

**Example conformance statement:**
> This implementation is Partial UPIF Conformant (v1.0), implementing layers L1, L4, and L5 in accordance with the UPIF Conformance Specification v1.0 (https://doi.org/10.5281/zenodo.15242693).

---

## Prompt Metadata Schema

Every UPIF-governed prompt carries a structured metadata object. Minimum required fields:

```json
{
  "prompt_id": "upif-xyz123",
  "author_uid": "user-001",
  "timestamp": "2025-04-18T00:00:00Z",
  "modality": "text",
  "tone_profile": "formal",
  "compliance_flags": {
    "gdpr_safe": true,
    "coppa_compliant": true
  },
  "revision_history": [
    {
      "rev": 1,
      "contributor_uid": "user-001",
      "timestamp": "2025-04-18T00:00:00Z",
      "content_hash": "sha256:..."
    }
  ]
}
```

Full schema: [`schemas/`](./schemas/)

---

## Strategic Significance

- **New layer of the AI stack** — UPIF operates between the user/application layer and the model API, enabling governance-before-generation.
- **PromptOps as a discipline** — UPIF introduces PromptOps: the orchestration of prompt authorship, governance, and safety as infrastructure.
- **Open protocol potential** — UPIF is designed to evolve as an open standard, enabling community-led governance packs, safety filters, and attribution protocols.
- **Model-agnostic** — UPIF is independent of any specific model, vendor, or runtime.

---

## Citation

If you use UPIF in your research or implementation, please cite:

```bibtex
@misc{thomas2025upif,
  author    = {Thomas, Roshan George},
  title     = {Unified Prompt Intelligence Framework (UPIF)},
  year      = {2025},
  doi       = {10.5281/zenodo.15242693},
  url       = {https://doi.org/10.5281/zenodo.15242693},
  publisher = {Zenodo}
}
```

Or see [CITATION.cff](./CITATION.cff) for other formats.

---

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for how to participate in the development of this specification.

---

## License

This specification is released under the terms in [LICENSE](./LICENSE).  
All uploaded content remains the property of the original author. See [IP/](./IP/) for IP declarations.

---

*Developed by [Roshan George Thomas](https://orcid.org/your-orcid-here) / XWHYZ  
Canonical record: [10.5281/zenodo.15242693](https://doi.org/10.5281/zenodo.15242693)*
