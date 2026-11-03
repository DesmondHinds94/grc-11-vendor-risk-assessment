# 04 — Risk Acceptance Memorandum

| | |
|---|---|
| **Memo ID** | RA-2026-011 |
| **Date** | 2026-11-03 |
| **To** | City of Marlowe Housing Authority, Authorizing Official (AO) |
| **Cc** | CMHA ISSO; CivicStack CISO; CivicStack Vendor Manager |
| **From** | GRC Analyst, CivicStack |
| **Subject** | Acceptance of residual risk: VeriFi Income Services (Tier 1 subprocessor to HAP) |
| **Related** | POA&M-07 · Risk R-07 · Vendor assessment VRA-2026-04 |

## 1. Decision requested

Approve continued use of VeriFi Income Services for income verification in HAP, accepting two residual risks that cannot be remediated before the contract renewal on 2026-11-15:

| # | Residual risk | Rating |
|---|---|---|
| V-3 | 12 VeriFi support staff authenticate with SMS one-time codes rather than phishing-resistant MFA | Low (6) after compensating controls |
| V-4 | VeriFi holds no GovRAMP or FedRAMP authorization | Moderate (8) |

## 2. Background

VeriFi verifies wage and benefit income for voucher eligibility. Doing it manually adds about 10 days per applicant and would build a backlog of about 600 cases within the first month. The vendor assessment ([03-gap-analysis.md](03-gap-analysis.md)) found two **High** gaps: 7-year retention of full SSNs, and 72-hour breach notice. VeriFi has **agreed contract terms that close both**. The two items below are what remain.

## 3. Risk analysis

**V-3: SMS MFA for support staff.** SMS codes can be phished or intercepted through SIM swapping. If a support account were compromised, the attacker could see verification results. *Compensating controls:* support views no longer show any SSN digits (configuration verified 2026-10-28); the support role cannot export or call the API in bulk; and VeriFi's SOC monitors support sessions. *Likelihood 2 × Impact 3 = **6, Low***. VeriFi has committed to FIDO2 for support staff by 2027-03-31.

**V-4: No GovRAMP authorization.** CMHA's guidance prefers authorized vendors for Moderate systems. VeriFi's SOC 2 Type II covers Security, Availability and Confidentiality, with no qualified opinion and one minor exception. GovRAMP would add continuous monitoring reported to the state and a control set aligned to 800-53. *Compensating controls:* a contractual 24-hour breach notice; data minimization (no documents sent, full SSN purged within 30 days); quarterly deletion attestation; a review of each new SOC 2 report; and HAP-side egress and API-key controls. *Likelihood 2 × Impact 4 = **8, Moderate (at tolerance)***.

Both residual scores are within the **≤ 9 tolerance** set in the HAP risk appetite ([GRC-03](https://github.com/DesmondHinds94/grc-03-risk-register)).

## 4. Alternatives considered

| Option | Why not chosen |
|---|---|
| Terminate and verify income manually | ~10-day delay per applicant; harms applicants and Fair Housing timeliness obligations; staff cost of about $140k a year |
| Switch to a GovRAMP-authorized competitor | Only one exists. Its contract would take about 6 months to put in place, and it requires uploading pay stubs, which means **more** PII leaves HAP |
| Accept (with conditions) | **Recommended** |

## 5. Conditions of acceptance

1. Contract addendum §§3–7 (retention, breach notice, secondary use, vulnerability SLA, post-breach audit right) signed **before** 2026-11-15 renewal.
2. VeriFi provides FIDO2 rollout evidence by **2027-03-31**. If it misses that date, this acceptance lapses for V-3 and the AO decides again.
3. CivicStack reviews each new SOC 2 report within 30 days of receipt, and receives a quarterly deletion attestation.
4. Any security incident at VeriFi involving CivicStack data **voids this acceptance** and triggers a reassessment.

## 6. Expiry

This acceptance **expires 2027-11-15** (one year, at the next contract renewal), or earlier under condition 2 or 4.

## 7. Approval

| Role | Name | Decision | Signature | Date |
|---|---|---|---|---|
| Authorizing Official, CMHA | | ☐ Accept ☐ Reject | | |
| CISO, CivicStack | | ☐ Concur | | |
| ISSO, CMHA | | ☐ Concur | | |

*The AO accepts risk on behalf of the City because HAP operates under the City's authorization. CivicStack can recommend, but cannot accept risk to the City's data.*
