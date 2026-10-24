# Overview

*Informative. The normative text is [SPEC.md](../SPEC.md).*

## The problem

A Proof Protocol record can be checked by anyone. Recompute the commitment root, verify the signatures, confirm the Registry Receipt, and you know the record is the one that was made. You do not know whether anyone else would have got the same answer. The Issuer might have picked a corpus that suited the control. The Witness might have been miscalibrated. The day might have been unusual. Every cryptographic check passes either way, because cryptography proves the record was not changed, not that it was right.

## The fix

Do it again, with different people, and see if the answer holds. That is reproof.

1. Someone, the **Commissioner**, wants to reproduce a registered proof, the **Head Assay**. It might be the Implementor, an insurer, a regulator, or a competitor.
2. The Commissioner publishes a **Reproof Manifest** first: what is being reproven, who will do it, and how close the result must be to count as agreement (the **Splitting Limit**). It is anchored in time before anything runs.
3. A new team runs the **Check Assay**. No one from the original, and no affiliate, sits in any seam. Same control, proven by an independently captured Fingerprint. Same shape of test. Entirely fresh canaries. The Provider is not told when.
4. A **Comparator** lines the two results up, technique class by technique class, and marks each **Cell** Agree, Diverge, or Insufficient. No judgment involved; the rules were fixed in step 2.
5. If they agree, the Head Assay is **Reproven**. If they diverge, a third team, the **Umpire**, is drawn from a declared pool by public randomness beacon and runs its own assay. Its ruling stands.
6. Everything is published. Agreeing checks, diverging checks, checks that ran out of sample, checks that were started and abandoned. A status shown without that history does not conform.

## What it is not

- Not record verification: that is already free to anyone under PP-SPEC-077 Section 21.
- Not a repeat run: the same people getting the same answer proves consistency, not independence.
- Not an audit: an audit reviews what was done; reproof does it again.

## Why mining

When a buyer and a seller assay the same ore and disagree beyond the agreed splitting limit, an umpire laboratory assays its own split and decides. The practice is centuries old because it works: one assay is a claim, two independent assays are a fact.
