# Contributing to UPIF

Thank you for your interest in contributing to the Unified Prompt Intelligence Framework (UPIF). UPIF is a specification-first protocol — contributions are primarily to the specification itself, the conformance requirements, the schema, and the supporting documentation.

This document explains how to participate effectively.

---

## What You Can Contribute

### Specification improvements
Corrections, clarifications, or extensions to [SPEC.md](./SPEC.md), [ARCHITECTURE.md](./ARCHITECTURE.md), or [CONFORMANCE.md](./CONFORMANCE.md). This includes:
- Ambiguities in MUST/SHOULD/MAY requirements
- Missing edge cases in layer definitions
- Conflicts between layer specifications
- Typos and formatting issues

### Schema contributions
Extensions or corrections to the UPIF prompt metadata schema in [`schemas/`](./schemas/). All schema changes must remain backward-compatible within a major version.

### Governance packs
Domain-specific policy rule sets for L5 (Compliance Firewall) — for example, a GDPR governance pack, a COPPA governance pack, or an enterprise brand governance pack. These live in `docs/governance-packs/`.

### Diagrams and documentation
Improvements to architecture diagrams, flow diagrams, or supporting documentation in `docs/` and `diagrams/`.

### Conformance test cases
Test cases and test vectors for verifying layer conformance. These will form the basis of the forthcoming UPIF conformance test suite (targeted for v1.1).

### Reference implementations
Links to or contributions of reference implementations in any language. Reference implementations should be clearly scoped to specific layers and conformance tiers.

---

## What This Repo Is Not

This is a **specification repository**, not an application codebase. Please do not open pull requests for:
- Full application builds
- Model wrappers or inference tools
- Prompt libraries or template collections
- Marketing or promotional content

---

## How to Contribute

### 1. Open an issue first

Before writing anything, open a GitHub Issue describing:
- Which layer or document the contribution affects
- The problem or gap you have identified
- Your proposed approach

This prevents duplicate effort and allows the maintainer to signal whether the direction aligns with the protocol's design intent before you invest time in a draft.

### 2. Fork and branch

```bash
git clone https://github.com/XwhyZ-WHYLD/upif-specs.git
cd upif-specs
git checkout -b your-branch-name
```

Branch naming convention:
- `spec/layer-name-description` for specification changes
- `schema/description` for schema changes
- `docs/description` for documentation changes
- `conformance/description` for conformance requirement changes

### 3. Make your changes

Follow the style conventions below. Keep changes focused — one issue per pull request.

### 4. Open a pull request

In your pull request description, include:
- The issue number it addresses
- A summary of what changed and why
- Which conformance tier or layer is affected
- Whether any existing conformance claims would be affected by the change

---

## Style Conventions

### Specification language
- Use **MUST**, **SHOULD**, and **MAY** in accordance with [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) semantics — the same conventions used in [CONFORMANCE.md](./CONFORMANCE.md)
- MUST-level changes require strong justification and will be reviewed carefully — they affect all conformance claims
- Write in plain English. Avoid jargon where a plain term is equally precise

### Markdown
- Use ATX headings (`#`, `##`, `###`)
- Use fenced code blocks with language identifiers (` ```json `, ` ```bash `)
- Use reference-style links for repeated URLs
- Keep lines under 120 characters where practical

### Schema
- All schema changes must be validated against the existing schema examples in Appendix A of the whitepaper
- New fields must include: field name, type, required/optional status, and a one-line description
- Removing or renaming existing fields is a breaking change and requires a major version bump

### Versioning
UPIF follows semantic versioning:
- **Major version** — breaking changes to MUST-level requirements or schema field names/types
- **Minor version** — additive changes: new SHOULD/MAY requirements, new optional schema fields, new governance packs
- **Patch version** — corrections, clarifications, typos with no semantic effect

---

## Governance

UPIF is currently maintained by Roshan George Thomas (XWHYZ). All contributions are reviewed by the maintainer. The project intends to establish a formal governance structure as the contributor community grows.

Contribution decisions are guided by the following principles:
- **Protocol integrity** — changes must preserve the coherence of the seven-layer model
- **Backward compatibility** — within a major version, existing conformance claims must remain valid
- **Openness** — the protocol is designed to evolve as an open standard; contributions that advance that goal are prioritised
- **Attribution** — all contributors are credited in the repository commit history and, where significant, in the CITATION.cff

---

## Citing UPIF in Your Work

If your contribution references or builds on UPIF, please use the canonical citation:

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

---

## Code of Conduct

All contributors are expected to engage with each other respectfully and in good faith. Harassment, dismissiveness, or bad-faith engagement will result in removal from the project.

---

## Questions

Open a [GitHub Discussion](https://github.com/XwhyZ-WHYLD/upif-specs/discussions) for questions that don't fit neatly into an issue. For direct correspondence, contact via the ORCID profile linked in [README.md](./README.md).
