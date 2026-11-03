# GRC-11 — Vendor Risk Assessment (CAIQ Review)

> **SR-6 / SI-12: The income-verification vendor kept full SSNs for 7 years against a 30-day requirement. Rated High; closed through contract (retain the result + last-4 only, quarterly deletion attestation).**
> **The vendor answered "Yes" to 29 of 31 CAIQ questions. Checked against the SOC 2 report, tests and contract text, 18 held up: 6 partial, 4 gaps, 3 unverified.**
> **Risk acceptance memo to the AO for two residual risks (SMS MFA for support staff, no GovRAMP authorization), with compensating controls, conditions, and a 2027-11-15 expiry.**

`Section 04 // Resilience & Third Party` · Part of the [GRC Control Lab Docket](https://github.com/DesmondHinds94/grc-portfolio)

---

## The engagement

The fictional **Marlowe Housing Assistance Portal** sends applicant SSNs to a third-party income-verification API. POA&M-07 in [GRC-02](https://github.com/DesmondHinds94/grc-02-gap-analysis-poam) found that this subprocessor had never been assessed. This lab is that assessment, from tiering to a signed-off decision.

```
Tier the vendor → derive requirements from the HAP baseline → validate every CAIQ answer
  → rate gaps → negotiate contract fixes → list CUECs CivicStack owns → accept what's left, in writing
```

## What's in this repo

| File | What it is |
|---|---|
| [01-vendor-profile-and-requirements.md](01-vendor-profile-and-requirements.md) | Vendor profile, tiering rationale (Tier 1), 14 security requirements each traced to an 800-53 control |
| [02-caiq-review.csv](02-caiq-review.csv) | 31 CAIQ v4 questions: vendor answer, requirement, **what the answer was validated against**, assessor result |
| [03-gap-analysis.md](03-gap-analysis.md) | Validation method, 10 gaps with inherent risk → treatment → residual, CUECs CivicStack must operate, overall rating |
| [04-risk-acceptance-memo.md](04-risk-acceptance-memo.md) | Decision memo to the AO: risk analysis, alternatives considered, conditions, expiry, signature block |

## Key judgments

- **A "Yes" on a CAIQ is a claim, not evidence.** Every answer was checked against the SOC 2 report, a direct test, contract text, or an interview, and marked Unverified where none of those existed.
- **The SOC 2 report has requirements of its own.** Its carve-outs and CUECs show what the vendor isn't covering and what CivicStack has to do itself. One CUEC (reviewing vendor access logs) wasn't being done and is now an action.
- **Only the system's AO can accept the risk.** CivicStack recommends; the City's AO decides, because the data belongs to the City.

---

*Fictional vendor and organizations. CAIQ question IDs follow CSA CAIQ v4 numbering with paraphrased topics; check them against CSA's published CAIQ before reuse. CAIQ and CCM are © Cloud Security Alliance.*
