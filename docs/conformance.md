# Conformance Checklist

*Informative summary of the MUST requirements in [SPEC.md](../SPEC.md). An Assay or status that fails any item is non-conforming.*

## Preconditions (SPEC 3)
- [ ] Head Assay records verify and are Conformant (077 21.13)
- [ ] Nothing described as reproof that is record verification or a Repeat Run

## Independence (SPEC 4)
- [ ] Check Party Set shares no party or Affiliate with the Head Party Set, except IP-2 beacon and IP-9 Registry
- [ ] Provider occupies no seam and is not Commissioner, Comparator, or Umpire Selector
- [ ] Commissioner, its interest, funding tier, and Sponsor declared
- [ ] Affiliation Window at least twelve months
- [ ] Independence Graph computable from published records

## Split (SPEC 5)
- [ ] DUT (and CUT) Fingerprint equal, captured independently by the Check Assay
- [ ] Instance: SUT Fingerprint equal; Class: same Comparability Class with registered Parity Declaration
- [ ] Same Mine Plan composition or technique, color, target, and Effect Point shape within declared tolerance
- [ ] Same Claim Sheet for Gold canaries
- [ ] Fresh canaries, nonces, salts, and effect tokens; overlap check stated
- [ ] Within Reproof Window, before any Molt and before Head validity ends
- [ ] Provider not told the release window

## Order (SPEC 6)
- [ ] Reproof Manifest registered and anchored before the Check Assay's first commitment
- [ ] Limits and method unchanged after commitment
- [ ] Check Issuer commits before receiving any Head content reveal
- [ ] Check adjudicated and registered before comparison; Adjudicator never given Head outcomes
- [ ] Results released to all parties at once

## Comparison (SPEC 7)
- [ ] Validity gates applied; Blind or Void over threshold makes every Cell Insufficient
- [ ] Minimum sample per Cell applied
- [ ] Absolute limit and declared test both applied
- [ ] Verdict published with Cell counts
- [ ] Comparator output identical to reference on conformance vectors

## Umpire (SPEC 8)
- [ ] Umpire Party Set independent of both Assays
- [ ] Drawn by post-divergence Time Anchor pulse from the declared pool; skips recorded
- [ ] One umpire per divergence

## Status and publication (SPEC 9, 10)
- [ ] Original Records never edited
- [ ] Status reported with scope, independent count, Cell level, and history
- [ ] Every committed Assay published, including abandoned and lapsed
