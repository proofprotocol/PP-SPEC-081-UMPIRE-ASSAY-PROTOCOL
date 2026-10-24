# Reproof: The Umpire Assay Protocol (UAP)

*A Proof Protocol specification*

> **Ownership and Attribution Notice**
>
> This specification is authored by **Craig Thomas Ellrod** and is published as part of **Proof Protocol**. Copyright (c) 2026 Craig Thomas Ellrod.
>
> Any use, implementation, derivative, citation, or incorporation of this specification, in whole or in part, MUST attribute **Craig Thomas Ellrod and Proof Protocol**. This requirement applies to standards bodies, working groups, consortia, and commercial implementations.
>
> This specification is licensed under the Proof Protocol License 1.1 (see LICENSE.md); text CC BY 4.0 under Part A, which grants no patent rights. Original inventor: Craig Thomas Ellrod (ORCID 0009-0004-1058-7666).
>
> **Patents.** Patent terms are in [PATENT-SCHEDULE.md](PATENT-SCHEDULE.md). Claims not listed there are reserved by Craig Thomas Ellrod. Licensing: 1proofprotocol@gmail.com.
>
> This specification is related to the Proof Economy Prior Art Declaration, DOI [10.5281/zenodo.21379780](https://doi.org/10.5281/zenodo.21379780), Category 4a, Reproducibility requirement.

| Field | Value |
|---|---|
| Spec ID | PP-SPEC-081 |
| Version | 0.1.0 (Draft) |
| Date | 2026-10-23 |
| Status | Draft for public record |
| Maintainer | Craig Thomas Ellrod (Proof Protocol) |
| Builds on | PP-SPEC-077 v0.8.2 (Dead Canary), PP-SPEC-078 v0.2.4 (Jailed Canary), PP-SPEC-079 v0.1.4 (Coal Mine), PP-SPEC-080 v0.1.2 (Pithead Safety and Acceptance), PP-SPEC-004 (ProofRegister API) |

---

## Abstract

A proof under PP-SPEC-077 is the record of one run: one Issuer, one Proof Witness, one Proof Swarm, one day. Anyone can verify that record: recompute its commitment root, check its signatures, confirm its Registry Receipt. Verifying a record proves the record is intact. It does not prove the outcome would happen again, and it does not prove that the parties who produced it got it right.

The Umpire Assay Protocol (UAP) defines **Reproof**: the independent re-execution of a proof, by parties who had no part in the original, against the same deployed control, with fresh canaries, under limits of agreement declared before the second run begins. A **Check Assay** that agrees with the original makes the original **Reproven**. A Check Assay that does not agree produces a **Divergence Finding**, which a third, independently drawn **Umpire Assay** settles. Every assay is committed in advance, published whatever its result, and registered as its own record. No original record is ever edited; reproof status is computed from the Registry by anyone, the same way by a person and by a machine.

The name comes from mining. When a buyer's laboratory and a seller's laboratory assay the same ore and disagree beyond the agreed splitting limit, a third laboratory, the umpire, assays its own split of the sample, and its result decides. Mining learned long ago that one assay is a claim and two independent assays are a fact. This specification applies that rule to security controls.

## Introduction: Why This Specification Exists

### The problem this family of specifications solves

Nobody can price security risk, because nobody can measure security efficacy. Every control, whether bought, built, or adopted, is described by the party that made it: a datasheet, a demo, a Provider-funded report, a design document, a dashboard of alerts. Implementors choose controls on those descriptions. Insurers underwrite on questionnaires that ask whether controls exist, not whether they work. Regulators supervise against attestations. Each of them is relying on the word of someone with a stake in the answer, and none of them has proof of what a control actually does when an attack arrives.

Agentic AI makes the gap wider and more expensive. An agent acts inside the system with legitimate credentials, decides its next step from text it has just read, and can be persuaded to do what its owner never authorized. The losses it can cause are new, and the controls sold to contain it have no track record. When risk cannot be measured, it is excluded, restricted, or priced as if every control were equally good, which punishes the controls that work and rewards the ones that only claim to.

The Proof Protocol specifications replace description with proof. PP-SPEC-077 measures what a security control did to committed test traffic. PP-SPEC-078 measures whether an agent containment control stopped an agent that tried to break its policy. PP-SPEC-079 makes those measurements independent of whoever built the control, and comparable across controls of any origin. PP-SPEC-080 lets the parties who pay for risk, insurers, regulators, and Implementors, state in advance what proof they will accept. PP-SPEC-081 makes any of those proofs reproducible by a party that was not there. Together they produce records that a person or a machine can verify without trusting the party the record is about.

**This specification's part:** the independent reproduction of a proof.

### Why this specification

A tamper-evident record answers one question: is this the record that was made? It does not answer the question an underwriter, a regulator, or a court will eventually ask: would anyone else, doing the same thing, have got the same answer?

Those are different questions, and the first does not answer the second. A record can be perfectly sealed, perfectly anchored, perfectly signed, and perfectly wrong. The Issuer chose a corpus that happened to suit the control. The Witness was miscalibrated. The environment was unusual that day. The parties were honest and the result was luck. Or the parties were not honest, and every cryptographic check still passes, because the cryptography proves only that nobody changed the record after it was made, not that the record was true when it was made.

Every discipline that has had to prove something to a skeptic arrived at the same answer. Science requires replication by an independent laboratory. Clinical medicine requires independent trials. Metrology runs proficiency tests between laboratories. Mining and metals trading settle disputes with an umpire assay. The common rule: a result produced once, by one party, is a claim about that party's work. A result produced again, by a party with no stake in the first, is a fact about the world.

Security has never had this. A lab report is not re-run by another lab against the same deployment. A proof of concept is never repeated by anyone but the Provider. A control attestation is re-checked only by reading the same logs again. A record that can be verified but cannot be reproven is a demonstration, not proof (Prior Art Declaration, Category 4a).

This specification exists so that every proof produced under Proof Protocol can be reproven, by anyone qualified, without the cooperation of the parties who produced it, and so that the result of trying is itself proof.

**Scope.** This specification defines how a proof produced under PP-SPEC-077, PP-SPEC-078, or PP-SPEC-079 is independently reproduced, how the reproduction is compared to the original, how disagreement is settled, and how the outcome is recorded. It does not change how any original run is executed, adjudicated, or registered. It does not assign value to any record, and it does not decide whether any reader accepts a record; that is PP-SPEC-080.

**What this is not.** It is not record verification, which any party can already perform under PP-SPEC-077 Section 21. It is not a repeat run by the same parties, which measures consistency, not independence (4.7). It is not an audit of the original parties' procedures, which reviews what they did rather than doing it again. It is not a second opinion on the original data, which re-reads the same evidence. Reproof produces new evidence, by new parties, under the same conditions, and compares outcomes.

## 1. Conventions

The key words MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, NOT RECOMMENDED, MAY, and OPTIONAL in this document are to be interpreted as described in BCP 14 (RFC 2119, RFC 8174) when, and only when, they appear in all capitals.

Section references of the form "077 9.4" refer to PP-SPEC-077; "078", "079", and "080" refer to those specifications in the same way. Unprefixed references are to this specification.

## 2. Terminology

Terms defined in PP-SPEC-077 Section 2 and PP-SPEC-079 Section 2 have the same meaning here. In addition:

- **Head Assay:** The original run, Engagement, or Bundle of records whose outcome is to be reproven. Its records are the **Original Records**.
- **Check Assay:** An independent re-execution of the Head Assay under this specification, by a Check Party Set (4.1).
- **Umpire Assay:** An independent re-execution performed after a Check Assay diverges from the Head Assay, by an Umpire Party Set drawn under Section 8, whose result settles the divergence.
- **Assay:** Any of the Head Assay, a Check Assay, or an Umpire Assay. Every Assay is a complete, Conformant run (077 21.13) in its own right.
- **Repeat Run:** A re-execution in which any party occupies, in the second run, a seam it or its affiliate occupied in the first. A Repeat Run is not a Check Assay and never produces Reproof (4.7).
- **Party Set:** For an Assay, the set of parties occupying its Integration Points (077 18.2), together with their Affiliates.
- **Affiliate:** A party that controls, is controlled by, or is under common control with another party; that employs or is employed by it; that holds equity in it or receives equity from it; that shares key custody (077 IP-10) or operating staff with it; or that has had a paid commercial relationship with it concerning the same DUT or Provider within the Affiliation Window (4.6).
- **Split:** The set of conditions held constant between Assays: the DUT and CUT Fingerprints, the SUT Fingerprint or Comparability Class, the Mine Plan composition, the Claim Sheet, and the Witness Coverage scope (Section 5). Canaries are never part of the Split.
- **Splitting Limit:** The declared maximum difference between Assays, per Compared Metric, within which two Assays agree (Section 7).
- **Compared Metric:** A rate or set computed identically from each Assay's registered records and compared under Section 7.
- **Cell:** One Compared Metric for one comparison stratum (for example, the Stopped rate for one technique class at one target level).
- **Reproof Manifest:** The record, published and anchored before a Check Assay or Umpire Assay commits, that declares what is being reproven, by whom, under what Split, Splitting Limit, and comparison method (Section 6).
- **Comparison Record:** The record of the mechanical comparison between two Assays, Cell by Cell (Section 7).
- **Divergence Finding:** A finding, recorded in a Comparison Record, that one or more Cells differ beyond the Splitting Limit.
- **Umpire Record:** The record of an Umpire Assay's comparison against both the Head Assay and the Check Assay, and its ruling (Section 8).
- **Reproof Status:** The status of an Original Record with respect to reproof, computed from the Registry by the rules of Section 9. Never stored in, and never altering, the Original Record.
- **Commissioner:** The party that commissions a Check Assay or Umpire Assay and publishes its Reproof Manifest.
- **Instance Reproof:** A reproof in which the Check Assay runs against the same SUT as the Head Assay, bound by the same SUT Fingerprint (077 15.2.5).
- **Class Reproof:** A reproof in which the Check Assay runs against a different SUT within the same Comparability Class (079 9.5) under a Parity Declaration (079 5.3).

### 2.1. Relationship to other specifications

| Specification | What it produces | What this specification adds |
|---|---|---|
| PP-SPEC-077 Dead Canary | A proof of efficacy from one run | Its independent reproduction, comparison, and settlement |
| PP-SPEC-078 Jailed Canary | Bookings and verdicts for an Agent Under Test | The same, per offense grade and verdict |
| PP-SPEC-079 Coal Mine | Engagements and Performance Records | Check and Umpire Engagements, linked to the Head Engagement |
| PP-SPEC-080 Pithead | Whether a reader accepts a record | Nothing. A profile MAY require a Reproof Status; this specification never decides acceptance |
| PP-SPEC-004 ProofRegister | Where records are registered | The records of this specification are registered there, like any other |

## 3. Verifying a Record Is Not Reproving It

3.1. Proof Protocol distinguishes four acts that are often confused:

| Act | Who | What it establishes | Produces Reproof |
|---|---|---|---|
| **Record verification** | Anyone | The record is the one that was made: commitment root recomputes (077 9.5), signatures verify (077 21.4), receipt verifies (077 21.5), no Revocation (077 21.6) | No |
| **Repeat Run** | The same parties, or any of them | The same parties get a consistent result | No |
| **Check Assay** | A Party Set independent of the Head Assay (4.2) | An independent party, under the same conditions, gets the same result | Yes, on agreement |
| **Umpire Assay** | A Party Set independent of both Head and Check (8.2) | Which of two divergent results stands | Yes, on ruling |

3.2. A party describing a record MUST NOT describe record verification or a Repeat Run as reproof, reproduction, replication, independent confirmation, or by any equivalent term.

3.3. Record verification is a precondition of reproof. A Head Assay whose records fail verification MUST NOT be the subject of a Check Assay; it is not proof, and there is nothing to reproduce.

3.3a. So is the reproducibility duty of the Head Assay's own specification (077 11.7, 078 17.7a). A run that did not publish what a Check Assay needs cannot be reproven, and is a demonstration, not proof.

3.4. Only Conformant records (077 21.13) can be reproven. A claim, report, attestation, or log produced outside PP-SPEC-077, PP-SPEC-078, or PP-SPEC-079, under any framework, is verification evidence (077 Section 3). It MAY be proven by a new run under those specifications. It cannot be reproven, because there is no committed Head Assay to reproduce.

## 4. Roles and Independence

4.1. **Party Sets.** The Party Set of every Assay MUST be declared in its Interface Manifest (077 18.1.3) and in the Reproof Manifest (Section 6), with each party's disclosed interests (077 4.4) and Affiliates.

4.2. **Independence from the Head Assay.** No member of the Head Assay's Party Set MAY occupy any Integration Point of a Check Assay, with two exceptions: the Time Anchor (077 IP-2), where it is a public randomness beacon no party to either Assay controls, and the Registry (077 IP-9). Independence is tested against every seam, not seam by seam: a party that was the Head Assay's Liveness Prober MUST NOT be the Check Assay's Issuer, Witness, or anything else.

4.3. **Internal separation.** Every separation rule of 077 18.1.6, 078 Section 16, and 079 Section 4 applies within each Assay exactly as it does to any run.

4.4. **The Provider.** The Provider of the DUT MUST NOT occupy any Integration Point of any Assay, and MUST NOT act as Commissioner, Comparator (13.1), or Umpire Selector (13.1). The Provider MAY fund a Check Assay or Umpire Assay, subject to 079 Section 6; the funding MUST be declared in the Reproof Manifest and on every record the Assay produces.

4.5. **Who may commission.** Any party MAY commission a Check Assay of any Head Assay whose records are Registered, including the Holder, an Implementor, an insurer, a regulator, an auditor, a sector body, or a competitor of the Provider. The Commissioner and its interest in the outcome MUST be declared. A Commissioner MAY also occupy seams in the Check Assay, subject to 4.2 and 4.3.

4.6. **Affiliation Window.** The Affiliation Window is declared in the Reproof Manifest and MUST NOT be shorter than twelve months before the Head Assay's first commitment through the publication of the Check Assay's Comparison Record. A relationship that begins inside the window is an affiliation.

4.7. **No self-checking.** A re-execution in which any party, or its Affiliate, occupies any seam in both runs (other than IP-2 and IP-9 under 4.2) is a Repeat Run. It MUST be labeled `repeat` in its records. It MUST NOT be registered as a Check Assay, MUST NOT be linked to the Head Assay as a reproof, and MUST NOT change any Reproof Status.

4.8. **Independence Graph.** From the Party Sets and disclosed interests of all Assays linked to one Head Assay, any verifier MUST be able to compute, from the published records alone, that no party or Affiliate appears in two Party Sets except as 4.2 permits. An Assay for which this cannot be computed is treated as a Repeat Run.

4.9. **False disclosure.** An undisclosed affiliation discovered after registration invalidates the affected Check or Umpire Assay as reproof. Any party MAY publish a Revocation (077 21.6) with reason code `run_invalidated` and the evidence of the affiliation. The Assay's own Units of Proof remain records of what that run observed; only its standing as reproof is withdrawn.

## 5. The Split

A Check Assay reproduces the outcome, not the canaries. What is held constant is the thing under test and the shape of the test. What is never held constant is the test traffic itself, because reusing the Head Assay's canaries would be replay, not reproduction.

5.1. **Same control.** The Check Assay's DUT Fingerprint (077 15.2) MUST equal the Head Assay's. Where the Head Assay attributed results to a CUT, the CUT Fingerprint MUST also be equal. The Fingerprint MUST be captured by the Check Assay's own Fingerprint Capture party (IP-5), independently of the Head Assay's capture. A Check Assay whose captured Fingerprint differs is not a reproof; it is a new proof of a different control, and MUST be registered as such.

5.2. **Same environment.** For an Instance Reproof, the SUT Fingerprint (077 15.2.5) MUST equal the Head Assay's, captured independently. For a Class Reproof, the Check Assay MUST be in the same Comparability Class (079 9.5) under a Parity Declaration (079 5.3) registered before the Check Assay commits. The Reproof Manifest MUST state which, and every resulting status carries the scope (Section 9).

5.3. **Same shape of test.** The Check Assay MUST use the Head Assay's Mine Plan composition (079 7.2), or, for a PP-SPEC-077 run outside an Engagement, the Head Assay's Composition Manifest (077 9.8; for PP-SPEC-078, 078 17.7a), within composition tolerances declared in the Reproof Manifest.

5.4. **Same claims.** Where the Head Assay included Gold canaries (077 5.6.4) against a Claim Sheet (079 8.1), the Check Assay MUST test the same claims.

5.5. **Same field of view.** The Check Assay's Witness Coverage Map (077 Section 14) MUST cover every Effect Point type compared. Where the two maps differ, comparison is restricted to their intersection, and the restriction MUST be stated in the Comparison Record.

5.6. **Fresh canaries.** The Check Assay's Issuer MUST generate its own Proof Swarm from its own corpus, with its own mutation seeds, nonces, and effect tokens, under 077 Sections 5 through 9. It MUST NOT reuse any canary content, nonce, salt, or effect token of the Head Assay. Its Corpus Fingerprint (077 15.2.6) MUST be published and is expected to differ from the Head Assay's. Where a Content Verifier (077 9.4.2) has access to both Assays' content reveals, it MUST confirm that no Check Assay canary content is identical to any Head Assay canary content, and the Comparison Record MUST state whether that check was made, by whom, and on what date.

5.7. **Reproof Window.** The Check Assay MUST complete within the Reproof Window declared in the Reproof Manifest, and in every case before the next Molt of the DUT Fingerprint (077 15.2.3) and before the Head Assay's validity window ends (077 21.8). A Check Assay outside the window is a new proof.

5.8. **Unannounced execution.** The Provider MUST NOT be told the Check Assay's release window in advance. The Implementor's operators MAY be told to the extent safe operation requires, and those told MUST be listed in the Reproof Manifest. A DUT that behaves differently when it detects a test is the failure a Check Assay exists to catch.

## 6. Commitment Order and Blindness

6.1. **Reproof Manifest first.** Before the Check Assay's first commitment (077 9.2), the Commissioner MUST publish a Reproof Manifest to the Registry, bound to a Time Anchor pulse, containing:

- The Head Assay: its Record IDs, or the Record ID of a Bundle (077 21.7) of them, and its Registry Receipts
- Reproof scope: `instance` or `class` (5.2), and the Parity Declaration hash for `class`
- The Commissioner, its interest, and the funding tier and Sponsor (079 Section 6)
- The Check Assay's Party Set with disclosed interests and Affiliates, and the Affiliation Window (4.6)
- The Compared Metrics, the comparison strata, the minimum Units of Proof per Cell, the Splitting Limit per Compared Metric, and the comparison method with all its parameters (Section 7)
- The composition tolerances (5.3) and the Reproof Window (5.7)
- The Umpire rule: the pool or method from which an Umpire Party Set would be drawn, the draw procedure, and who bears the Umpire Assay's cost (Section 8)
- The parties told of the release window, if any (5.8)
- A publication commitment: that the Check Assay, its Comparison Record, and any Umpire Assay will be published whatever their outcome, including invalid, abandoned, and Insufficient results

6.2. **Limits before results.** The Splitting Limit and comparison method are fixed by the Reproof Manifest. They MUST NOT be changed after the Check Assay's commitment. A Commissioner that wishes to compare under different limits MUST commission a new Check Assay under a new manifest.

6.3. **Issuer blindness to the Head Assay's content.** The Check Assay's Issuer MAY use the Head Assay's public reveal (077 9.4.1) and Composition Manifest (077 9.8) to match composition (5.3). It MUST commit its Proof Swarm root before it receives any of the Head Assay's content released at `holder_only` (077 9.4), if it receives that content at all.

6.4. **Adjudication before comparison.** The Check Assay MUST be adjudicated (077 Section 11) and its records registered before any comparison is computed. The Check Assay's Adjudicator (IP-8) MUST NOT receive the Head Assay's outcomes as an input. Comparison is a separate step (Section 7).

6.5. **No early results.** No party to the Check Assay MAY disclose its outcomes to the Head Assay's parties, the Provider, or the Commissioner before its records are registered. The Head Assay's parties and the Provider receive the Comparison Record at the same moment as the Commissioner.

## 7. Comparison

7.1. **Compared Metrics.** Unless the Reproof Manifest declares a superset, the Compared Metrics are, per comparison stratum:

| Compared Metric | Source |
|---|---|
| Stopped rate over adjudicated bad canaries | 077 Section 12 |
| False block rate over delivered good canaries | 077 Section 12 |
| Claim Finding set: each Gold claim, Stopped or Missed | 077 11.6 |
| Blind share and Void share | 077 14.3 |
| For PP-SPEC-078 Assays: booking rate and verdict distribution per offense grade | 078 Sections 6, 10 |

The default comparison strata are technique class and target level (077 2.2). The Manifest MAY declare finer strata; it MUST NOT declare coarser ones than the Head Assay's published rates.

7.2. **Validity gates.** Comparison is computed only between valid runs (077 11.3). If either Assay's Blind share or Void share exceeds the threshold declared in its own run, every Cell is **Insufficient**: the field of view was not good enough to compare.

7.3. **Minimum sample.** A Cell in which either Assay has fewer Units of Proof than the declared minimum is **Insufficient**. Insufficient is neither agreement nor divergence and MUST NOT be presented as either.

7.4. **Splitting Limit.** For each remaining Cell, the Comparator applies the comparison method declared in the Reproof Manifest. The method MUST be fully specified by its parameters, so that any party applying it to the same registered records obtains the same verdict (077 21.14.4). The method MUST combine an absolute limit with the declared statistical test: a Cell **Agrees** only if the absolute difference is within the declared limit and the declared test does not reject agreement at the declared level.

> *Informative example.* Stopped rate, technique class T1059, absolute limit 0.05, two-sided exact test for difference of two proportions at alpha 0.05, minimum 30 Units of Proof per Assay per Cell. Head 47 of 50 Stopped (0.94); Check 44 of 50 Stopped (0.88). Difference 0.06 exceeds 0.05: the Cell **Diverges**, regardless of the test.

7.5. **Claim Findings.** A Gold claim Missed in both Assays is a **Confirmed Claim Finding**. A Gold claim Missed in one Assay and Stopped in the other is a divergent Cell, whatever the rate limits.

7.6. **Cell verdicts.** Each Cell is exactly one of **Agree**, **Diverge**, or **Insufficient**. Every Divergent Cell carries a direction: **Head higher** or **Check higher** for each rate.

7.7. **Assay verdict.** The Comparison Record's verdict is **Agree** if at least one Cell Agrees and none Diverges; **Diverge** if any Cell Diverges; **Insufficient** if no Cell Agrees or Diverges. The verdict MUST be published with the count of Cells in each state, so that "Agree" over one sufficient Cell cannot be presented as agreement over the whole test.

7.8. **Direction is a finding, not an accusation.** A Divergence Finding in which the Head Assay's Stopped rate is higher is recorded as `head_overstated`; the reverse as `head_understated`. Neither implies misconduct by any party. Divergence has honest causes: corpus selection, witness drift, environment drift, and chance. Section 8 decides which result stands; it does not decide why.

7.9. **Mechanical comparison.** The Comparator MUST produce the Comparison Record from the registered records of both Assays and the Reproof Manifest alone, with no other input, and MUST produce output identical to the reference comparator on the published conformance vectors.

## 8. Umpire Assay

8.1. **When.** A Check Assay with verdict Diverge MAY be followed by one Umpire Assay. Any of the Holder, the Commissioner, the Head Assay's Issuer, the Check Assay's Issuer, or the Provider MAY request it. Until an Umpire Assay concludes, or the request window declared in the Reproof Manifest closes without a request, the Head Assay's status is `divergent` (Section 9).

8.2. **Who.** The Umpire Party Set MUST be independent, under Section 4, of both the Head Assay's and the Check Assay's Party Sets.

8.3. **Drawn, not chosen.** The Umpire Issuer and Umpire Witness MUST be drawn from the pool declared in the Reproof Manifest by a procedure seeded from a Time Anchor pulse issued after the Divergence Finding is registered. No party to either Assay, and not the Provider, MAY choose the umpire. A pool member that fails the independence test of 8.2 is skipped by the procedure, and the skip is recorded.

8.4. **Same Split, fresh canaries.** The Umpire Assay follows Sections 5 and 6 in full, against the same Split, with its own Proof Swarm.

8.5. **Ruling.** The Umpire Assay is compared to each prior Assay under Section 7, using the Splitting Limit of the Reproof Manifest. The Umpire Record states one ruling:

| Umpire agrees with | Ruling | Head Assay | Check Assay |
|---|---|---|---|
| Head only | `head_upheld` | Upheld | Not upheld |
| Check only | `check_upheld` | Not upheld | Upheld |
| Both | `both_within_umpire` | Upheld | Upheld |
| Neither | `disputed` | Disputed | Disputed |
| Insufficient against either | `umpire_insufficient` | Divergent | Divergent |

8.6. **One umpire.** There is one Umpire Assay per Divergence Finding. After a ruling, or `umpire_insufficient`, the Split is closed for reproof; further assays against it are new Check Assays under a new Reproof Manifest and are reported beside, never instead of, the earlier ones.

8.7. **Cost.** The Reproof Manifest MAY declare that the party whose Assay is not upheld bears the cost of the Umpire Assay, as is customary in umpire assaying. Cost allocation never affects any verdict.

## 9. Reproof Status

9.1. **Overlay, never edit.** Reproof never edits, re-signs, revokes, or re-registers any Original Record. Reproof Status is computed by any verifier from the Reproof Manifests, Comparison Records, Umpire Records, and Revocations registered against a Head Assay. Two verifiers reading the same Registry state MUST compute the same status.

9.2. **Status values.** For a Head Assay, in this order of precedence:

| Status | Rule |
|---|---|
| `disputed` | An Umpire Record with ruling `disputed` |
| `not_upheld` | An Umpire Record with ruling `check_upheld` |
| `divergent` | A Comparison Record with verdict Diverge and no Umpire Record ruling on it |
| `reproven` | At least one Comparison Record with verdict Agree, or an Umpire Record with ruling `head_upheld` or `both_within_umpire` |
| `checked_insufficient` | Only Insufficient Comparison Records |
| `pending` | A registered Reproof Manifest with no Comparison Record yet, inside its Reproof Window |
| `single` | None of the above |

9.3. **Scope and count.** Every status MUST be reported with its scope, `instance` or `class` (5.2), and with the number of independent Check Party Sets that agreed. `reproven (instance, 2)` means two mutually independent Check Assays, each against the same deployed SUT, agreed with the Head Assay. Check Assays whose Party Sets are not mutually independent under Section 4 count once.

9.4. **Cell-level status.** A status also applies per Cell. A Unit of Proof in the Head Assay takes the status of the Cell it falls in. A Head Assay may be `reproven` for one technique class and `divergent` for another, and MUST be reported that way wherever per-Cell rates are reported.

9.5. **Expiry.** Reproof Status ends with the Head Assay's validity (077 21.8). A Molt of the DUT Fingerprint ends the status of every Head Assay bound to the earlier Fingerprint; the status is then historical, not current.

9.6. **What never changes status.** Repeat Runs (4.7), unregistered runs, runs revoked under 4.9, and Check Assays outside the Reproof Window (5.7) never change any status.

9.7. **Units of Proof.** Reproof creates no Units of Proof for the Head Assay and removes none. Each Check and Umpire Assay produces its own Units of Proof, in its own records, under its own Holder. A Unit of Proof is never counted twice because it was reproven, never merged with its counterpart, and never weighted by its status at the level of the record (077 21.11). Any weighting by status belongs to the consumer and MUST be stated by the consumer (080).

## 10. Publication

10.1. Every Check Assay and Umpire Assay for which a Reproof Manifest was registered MUST be published, with its Comparison Record or Umpire Record, whatever its verdict.

10.2. A Check Assay that is committed but not completed MUST be published as `abandoned`, with the reason. An abandoned Check Assay is counted in the reproof history of the Head Assay and MUST be reported beside its status.

10.3. A Reproof Manifest whose Check Assay never commits before its Reproof Window closes MUST be published as `lapsed`.

10.4. Any rendering of a Head Assay's results that states a Reproof Status MUST also state the counts of Agree, Diverge, Insufficient, abandoned, and lapsed Check Assays against it. A status shown without its history is non-conforming. This is the rule that makes shopping for an agreeing Check Assay visible.

## 11. Reproof Across the Family

11.1. **PP-SPEC-077 runs.** A Check Assay of a 077 run in Bounded Mode is a Bounded Mode run under the same Split. A Check Assay of a 077 Production Stream result series compares over declared clutches; the Manifest MUST name the clutches compared, and the Check Assay MUST run over a concurrent or adjacent window bound to the same Fingerprints.

11.2. **PP-SPEC-078 runs.** A Check Assay of a 078 run uses the same Declared Policy, the same Cell configuration, and the same offense grades, with its own bait canaries. Compared Metrics are per offense grade (7.1). Destructive and agent-escape tests follow 078 Section 14 in the Check Assay exactly as in the Head Assay.

11.3. **PP-SPEC-079 Engagements.** A Check Assay of a Performance Record is a Coal Mine Protocol Engagement whose Engagement Manifest carries `reproof_of` with the Head Engagement's identifier and the Reproof Manifest's Record ID. It MUST be in the same Comparability Class. An Independent Test Lab Mode Check Assay of an In-Situ Head Engagement is a Class Reproof only.

11.4. **Self-Provided Engagements.** A Self-Provided Head Engagement (079 4.4) MAY be checked by the same organization only if every team occupying a seam in the Check Assay is independent, under Section 4 applied between teams, of every team in the Head Assay. The record MUST carry the Self-Provided flag.

## 12. Records

12.1. Every record type this specification defines is a record under 077 Section 21: content-derived Record ID, RFC 8785 canonical form, Holder, signature envelope, Registry Receipt, Disclosure Level, Revocation. Record IDs for this specification's record types are computed as `SHA-256("UAP-1:record" || canonical_form)` under the exclusions of 077 21.1.1.

12.2. The record types are: **Reproof Manifest** (6.1), **Comparison Record** (Section 7), **Umpire Draw** (8.3), **Umpire Record** (8.5), and the publication states `abandoned` and `lapsed` (10.2, 10.3), carried as Comparison Records with that verdict. Divergence Findings are carried inside Comparison Records. Their machine form is [schemas/reproof.schema.json](schemas/reproof.schema.json).

12.3. **Linkage.** Every Check and Umpire Assay's own run records MUST carry `reproof_manifest` with the Reproof Manifest's Record ID. Every Comparison Record and Umpire Record MUST carry the Record IDs, or Bundle Record IDs, of every Assay it compares.

12.4. **Disclosure.** A Comparison Record's verdict, Cell counts, and status effect MUST be at Disclosure Level `public` whenever the Head Assay's result record is `public`. A reproof of a public proof cannot be hidden.

12.5. **Signatures.** A Comparison Record requires the Comparator's signature and the Check Assay's Issuer and Witness signatures. An Umpire Record requires the Comparator's and the Umpire Assay's Issuer and Witness signatures. The Head Assay's parties MAY append endorser signatures (077 21.4.2); they cannot withhold the record.

12.6. **Humans and machines.** 077 21.14 applies to every record of this specification. A Reproof Status computed by a machine from the Registry and by a person from the human renderings MUST be the same.

12.7. **Authorship Disclosure.** 077 21.15 applies to this specification and to every comparator, umpire selector, and renderer implementing it.

## 13. Integration Points

13.1. Each Assay occupies the seams of 077 Section 18 (and 078 Section 16 where applicable) as any run does. This specification adds:

| ID | Integration Point | What plugs in | MUST do | MUST emit |
|---|---|---|---|---|
| **IP-R1** | Commissioner | Implementors, insurers, regulators, auditors, sector bodies, independent laboratories | Publish the Reproof Manifest before the Check Assay commits; commit to publication | Reproof Manifest, anchored |
| **IP-R2** | Comparator | Statistical engines, reporting tools | Apply Section 7 exactly from registered records and the Manifest alone; identical output to the reference comparator on the conformance vectors | Comparison Records, Umpire Records |
| **IP-R3** | Umpire Selector | Randomness-seeded draw services | Draw the Umpire Party Set under 8.3 from a post-divergence Time Anchor pulse; record skips | Umpire Draw record |
| **IP-R4** | Status Resolver | Registries, verifiers, agents, dashboards | Compute Reproof Status under Section 9 from the Registry alone; render with history (10.4) | Status with scope, count, and history |

13.2. **Separation.** The Comparator MUST NOT be a member of any compared Assay's Party Set, and MUST NOT be the Provider. The Umpire Selector MUST NOT be a member of any Party Set, the Commissioner of the Check Assay, or the Provider.

## 14. Security Considerations

- **Check shopping:** A Provider or Holder commissions Check Assays until one agrees and publishes only that one. Mitigated by the anchored Reproof Manifest before commitment (6.1), mandatory publication including abandoned and lapsed assays (Section 10), and the rule that no status is shown without its history (10.4).
- **Umpire shopping:** A party disputes until it wins. Mitigated by one umpire per divergence (8.6), the umpire drawn by beacon rather than chosen (8.3), and the closed Split.
- **Hidden affiliation:** A Check Assay run by a friend of the Head Assay. Mitigated by the Independence Graph (4.8), the Affiliation Window (4.6), and revocation on discovery (4.9). Disclosure alone does not cure a conflict (Proof Economy Code of Ethics, Section 8.6).
- **Copycat check:** A Check Issuer reuses the Head Assay's canaries to guarantee agreement. Mitigated by fresh canaries, nonces, and effect tokens (5.6), commitment before content access (6.3), and Content Verifier confirmation of no overlap.
- **Tuned limits:** A Commissioner declares a Splitting Limit so loose that everything agrees. Mitigated by fixing limits before results (6.2), publishing them with every status, and letting PP-SPEC-080 profiles set the minimum limits a reader will accept.
- **Test detection:** A DUT, or its Provider, recognizes the Check Assay and behaves differently. Mitigated by unannounced execution (5.8), indistinguishability (077 5.2), and Fingerprint equality captured independently (5.1). A divergence caused this way is the protocol working.
- **Induced outages:** A Provider induces black holes in the Check Assay to make it Insufficient. Mitigated by 077 15.6, independent liveness, DUT attribution of DUT-caused outages (077 15.6.6), and publication of every Insufficient result with its Void share.
- **Stale reproof:** A status earned before a change is shown after it. Mitigated by expiry on Molt and validity (9.5).
- **Sybil checkers:** Several nominally independent checkers under common control. Mitigated by the Affiliate definition and by counting only mutually independent Party Sets (9.3).
- **Reproof as attack:** A competitor commissions Check Assays to manufacture divergence. Mitigated by the same independence, commitment, and umpire rules that bind every other Commissioner, by the requirement that the Commissioner's interest be declared (4.5), and by the umpire.

## 15. Reserved

Additional witness requirements within a single run remain reserved under PP-SPEC-077 Section 21.16. Nothing in this specification defines them, and nothing in this specification assigns value to any record.

## 16. Interpretation

Craig Thomas Ellrod, as maintainer of Proof Protocol, is responsible for the editorial text of this specification. Whether an Assay, comparison, ruling, or status conforms is determined from its records against the normative text, and is not decided by the maintainer.

## Revision History

| Version | Date | Notes |
|---|---|---|
| 0.1.0 | 2026-10-23 | Initial draft. Reproof as independent re-execution: Head, Check, and Umpire Assays; record verification and Repeat Runs distinguished (Section 3); Party Set independence across every seam, Affiliates, Affiliation Window, Independence Graph (Section 4); the Split held constant with fresh canaries, Instance and Class Reproof, Reproof Window, unannounced execution (Section 5); Reproof Manifest before commitment, limits fixed before results (Section 6); Cell-level comparison with absolute and statistical Splitting Limits, Insufficient as a third state, Confirmed Claim Findings (Section 7); beacon-drawn Umpire Assay and rulings (Section 8); Reproof Status as a computed overlay with scope, count, Cell level, and expiry (Section 9); mandatory publication including abandoned and lapsed (Section 10); application to 077, 078, 079 (Section 11); records, `UAP-1:record` tag, schema (Section 12); IP-R1 to IP-R4 (Section 13). |
