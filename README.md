# Reproof: The Umpire Assay Protocol

> **Ownership and Attribution Notice**
>
> Reproof and the Umpire Assay Protocol (PP-SPEC-081) are authored by **Craig Thomas Ellrod** and published as part of **Proof Protocol**. Copyright (c) 2026 Craig Thomas Ellrod.
>
> Any use, implementation, derivative, citation, or incorporation of this work, in whole or in part, MUST attribute **Craig Thomas Ellrod and Proof Protocol**. See [NOTICE.md](NOTICE.md).
>
> Licensed under the Proof Protocol License 1.1 (see LICENSE.md); text CC BY 4.0 under Part A, which grants no patent rights. Original inventor: Craig Thomas Ellrod (ORCID 0009-0004-1058-7666).
>
> **Patents.** Patent terms are in [PATENT-SCHEDULE.md](PATENT-SCHEDULE.md). Claims not listed there are reserved by Craig Thomas Ellrod. Licensing: 1proofprotocol@gmail.com.

---

**One assay is a claim. Two independent assays are a fact.**

Anyone can verify a Proof Protocol record: recompute the root, check the signatures, confirm the receipt. That proves the record is intact. It does not prove anyone else would get the same result. Reproof does.

## How it works

```
 Head Assay (the original proof, already registered)
        |
        |  Reproof Manifest: Split, Splitting Limit, Party Set,
        |  umpire rule, publication commitment. Anchored BEFORE the check.
        v
 Check Assay: new Issuer, new Witness, new everything,
 same control (same Fingerprint), fresh canaries, unannounced
        |
        v
 Comparator: Cell by Cell, mechanical, limits fixed in advance
        |
   +----+-----------------+------------------+
   |                      |                  |
 Agree               Diverge             Insufficient
 -> Reproven         -> Umpire Assay      -> no claim either way
                        drawn by beacon,
                        independent of both
                        -> head_upheld / check_upheld /
                           both_within_umpire / disputed
```

1. **Declare first.** What is being reproven, by whom, and how close counts as agreement are anchored before the Check Assay commits.
2. **Hold the control constant.** Same DUT Fingerprint, captured independently. Same environment (Instance Reproof) or same Comparability Class (Class Reproof).
3. **Never reuse the test.** Fresh canaries, nonces, and effect tokens. Reusing them is replay, not reproduction.
4. **Compare mechanically.** Per technique class and target level. Agree, Diverge, or Insufficient. Never fudged.
5. **Settle by umpire.** Divergence goes to a third assay drawn by public beacon from a declared pool. Its ruling stands.
6. **Publish everything.** Agreeing, diverging, insufficient, abandoned, lapsed. A status shown without its history is non-conforming.

## Why it is different

- **Record verification is not reproof.** A perfectly sealed record can be perfectly wrong.
- **Independence across every seam.** No party, or affiliate, from the original occupies any seam of the check.
- **Repeat runs do not count.** The same parties getting the same answer is consistency, not independence.
- **Limits before results.** Nobody picks the Splitting Limit after seeing the numbers.
- **No shopping.** Every committed check is published. One umpire per divergence, drawn not chosen.
- **The original is never touched.** Reproof Status is computed from the Registry by anyone, the same way by a person and a machine.
- **Proof expires.** Change the control and the reproof ends with it.

## Repository

| Path | Contents |
|---|---|
| [SPEC.md](SPEC.md) | The normative specification, PP-SPEC-081 |
| [docs/overview.md](docs/overview.md) | Plain-English walkthrough |
| [docs/glossary.md](docs/glossary.md) | Terms |
| [docs/conformance.md](docs/conformance.md) | Conformance checklist |
| [docs/faq.md](docs/faq.md) | Common questions |
| [schemas/reproof.schema.json](schemas/reproof.schema.json) | Reproof Manifest, Comparison, Umpire Draw, Umpire Record schemas |
| [schemas/ai-disclosure.schema.json](schemas/ai-disclosure.schema.json) | Authorship Disclosure schema (077 21.15) |
| [CHANGELOG.md](CHANGELOG.md) | Version history |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to engage |
| [NOTICE.md](NOTICE.md) | Attribution requirements |
| [AI_DISCLOSURE.md](AI_DISCLOSURE.md) | What was human-authored and what was AI-drafted |
| [FUNDING.md](FUNDING.md) | Funding disclosure |
| [REVIEWERS.md](REVIEWERS.md) | Review disclosure |
| [ACKNOWLEDGEMENTS.md](ACKNOWLEDGEMENTS.md) | Credits |
| [ETHICS.md](ETHICS.md) | Proof Economy Code of Ethics |
| [CITATION.cff](CITATION.cff) | Citation metadata |
| [SECURITY.md](SECURITY.md) | Reporting protocol flaws |
| [PATENT-SCHEDULE.md](PATENT-SCHEDULE.md) | Patent terms |
| [LICENSE.md](LICENSE.md) | License terms |
| [LICENSE-CC-BY-4.0.md](LICENSE-CC-BY-4.0.md) | CC BY 4.0, specification text |

## Status

Draft, version 0.1.0, 2026-10-23. Maintained by Craig Thomas Ellrod as part of Proof Protocol.

Builds on PP-SPEC-077 (Dead Canary), PP-SPEC-078 (Jailed Canary), PP-SPEC-079 (Coal Mine), and PP-SPEC-080 (Pithead). Records are registered to a [PP-SPEC-004](https://github.com/proofprotocol/registry-api-spec) registry; the public instance is [proofregister.com](https://proofregister.com).

Archived on Zenodo: v0.1.0, DOI [10.5281/zenodo.23607722](https://doi.org/10.5281/zenodo.23607722). All versions: [10.5281/zenodo.23607721](https://doi.org/10.5281/zenodo.23607721).

Related: Proof Economy Prior Art Declaration, DOI [10.5281/zenodo.21379780](https://doi.org/10.5281/zenodo.21379780), Category 4a, Reproducibility requirement. PP-SPEC-077, ProofSwarm: The Dead Canary Protocol, DOI [10.5281/zenodo.23285060](https://doi.org/10.5281/zenodo.23285060).

## Cite

```
Ellrod, C. (2026). Reproof: The Umpire Assay Protocol (PP-SPEC-081), v0.1.0.
Craig Thomas Ellrod, Proof Protocol. https://doi.org/10.5281/zenodo.23607722
```
