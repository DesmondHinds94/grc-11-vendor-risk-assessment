# 01 — Vendor Profile, Tiering, and Security Requirements

## 1. Vendor profile

| | |
|---|---|
| **Vendor** | VeriFi Income Services, Inc. *(fictional)* |
| **Service** | Income and employment verification API. HAP sends an applicant's identity data and receives verified wage and benefit income, used for Housing Choice Voucher eligibility |
| **Data shared** | Name, DOB, **full SSN**, current employer (optional). Returned: employer names, pay-period wages for the last 12 months, benefit income |
| **Volume** | ~1,800 verification calls per month; ~40,000 applicants over the contract life |
| **Integration** | Server-to-server REST API from the HAP eligibility service; outbound allow-listed FQDN (SC-7(5)) |
| **Hosting** | Commercial AWS us-east-1 / us-west-2 (not GovCloud) |
| **Assurance provided** | CAIQ v4 (completed 2026-08-22) · SOC 2 Type II report, period 2025-07-01 → 2026-06-30 · Pen-test executive summary (2026-04) |
| **Linked items** | POA&M-07 (SR-3, SR-5, SR-6, SR-8) · Risk R-07 ([GRC-03](https://github.com/DesmondHinds94/grc-03-risk-register)) |

## 2. Tiering

| Factor | Score | Basis |
|---|---|---|
| Data sensitivity | **High** | Full SSN + income for a Moderate-categorized system |
| Volume | High | Most of the applicant population over time |
| Operational dependency | Moderate | Manual income verification is possible, but slow (~10 days vs. seconds) |
| Access into HAP | Low | Vendor has no access *into* HAP; HAP calls out |
| Substitutability | Moderate | Two competitors exist; switching takes about 6 months |
| **Tier** | **Tier 1 — Critical** | Any High on data sensitivity → Tier 1. Full assessment plus annual review |

## 3. CivicStack Tier-1 vendor security requirements

Derived from the HAP GovRAMP Moderate baseline and the CMHA MSA. Each requirement names the 800-53 control CivicStack must satisfy **through** the vendor.

| Req | Requirement | Driver |
|---|---|---|
| VR-01 | Current independent attestation: SOC 2 Type II (≤ 12 months old), ISO 27001, or GovRAMP/FedRAMP authorization | SA-9, SR-6 |
| VR-02 | Customer data stored and processed only in the United States | SA-9(5), MSA §8 |
| VR-03 | Encryption in transit (TLS 1.2+) and at rest (AES-256, managed keys) | SC-8, SC-28 |
| VR-04 | Phishing-resistant MFA for every vendor workforce account with access to customer data or production | IA-2(1), IA-2(2) |
| VR-05 | Least-privilege access to customer data, with quarterly access reviews | AC-6, AC-6(7) |
| VR-06 | Security incident notification to CivicStack **within 24 hours** of discovery | SR-8, IR-6(3), MSA §11 |
| VR-07 | Data retained only as long as needed for the verification; **deleted within 30 days** unless law requires otherwise; deletion attested | SI-12, PT-2, MP-6 |
| VR-08 | Audit logging of access to customer data, retained ≥ 1 year, available on request | AU-2, AU-11 |
| VR-09 | Vulnerability management: Critical remediated ≤ 15 days, High ≤ 30 days; annual third-party pen test | RA-5, SI-2, CA-8 |
| VR-10 | Background checks for personnel with access to customer data | PS-3 |
| VR-11 | Subprocessors disclosed; flow-down of these requirements; 30-day notice of changes | SR-3, SA-9(2) |
| VR-12 | Business continuity: documented BCP/DR, tested annually; API RTO ≤ 24h | CP-2, CP-4 |
| VR-13 | Right to audit, or to receive evidence on request | SR-6, SA-9 |
| VR-14 | No use of customer data for any secondary purpose (marketing, model training, resale) | PT-3, PT-4 |
