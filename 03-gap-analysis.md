# 03 — Gap Analysis and Vendor Risk Rating

## 1. How the CAIQ was reviewed

A CAIQ is self-attestation. Each answer relevant to a requirement in [01](01-vendor-profile-and-requirements.md) was **validated** against something other than the vendor's word, in this order of preference:

1. **Tested directly** (e.g., a TLS scan of the API endpoint)
2. **Independent evidence**: the SOC 2 Type II report, including its exceptions, carve-outs and complementary user entity controls (CUECs)
3. **Contract or policy text** the vendor would be held to
4. **Interview** (2026-10-14, VeriFi Director of Security)
5. Otherwise marked **Unverified**

| Result | Count | Meaning |
|---|---|---|
| Meets | 18 | Answer supported by evidence |
| Partial | 6 | Control exists but falls short of the requirement |
| Gap | 4 | Requirement not met |
| Unverified | 3 | Self-attested only; evidence requested |
| **Total reviewed** | **31** | The vendor answered "Yes" to 29 of them. **18 held up.** |

## 2. Gaps and partials

| # | Gap | Req | CAIQ | Inherent risk | Treatment | Residual |
|---|---|---|---|---|---|---|
| **V-1** | Full SSN + income kept **7 years**. FCRA requires keeping the verification *result*, not the full SSN | VR-07 | DSP-16.1 | **High** | **Contract:** keep the verification result + last-4 SSN; purge full SSN within 30 days; quarterly deletion attestation. Vendor **agreed** (addendum §3) | Low |
| **V-2** | Breach notice 72h *from confirmation* | VR-06 | SEF-07.1 | **High** | **Contract:** 24h from discovery of a suspected incident affecting CivicStack data. Vendor **agreed** (addendum §5) | Low |
| **V-3** | Support staff (12) use **SMS MFA** and can see verification results | VR-04 | IAM-14.1 | Moderate | Vendor will move support staff to FIDO2 by **2027-03-31**. Until then, support views mask SSN entirely (vendor confirmed a config change, 2026-10-28) | Low → **accept until 2027-03-31** |
| **V-4** | **No GovRAMP/FedRAMP authorization**; not pursuing before 2028 | VR-01 (pref.) | SUPP-01 | Moderate | VR-01 is met by the SOC 2 Type II. The remaining risk is that CMHA prefers authorized vendors for Moderate systems | Moderate → **accept, annual review** |
| V-5 | Privacy policy allows "de-identified data for product improvement" | VR-14 | DSP-07.1 | Moderate | **Contract:** no secondary use of CivicStack data, de-identified or not (addendum §4). Vendor agreed | Low |
| V-6 | Critical vulnerability SLA 30d vs 15d | VR-09 | TVM-08.1 | Low | Vendor commits to 15d for internet-facing API components (addendum §6) | Low |
| V-7 | AWS carved out of the SOC 2; vendor's review of the AWS SOC report not evidenced | VR-11 | STA-07.1 | Low | Request evidence of their annual subservice review. AWS's own reports are publicly available | Low |
| V-8 | No supply-chain risk assessment program (planned 2027) | VR-11 | STA-14.1 | Low | Track; re-check at annual review | Low |
| V-9 | SOC 2 exception: 2 of 25 terminations late | VR-05 | IAM-08.1 | Low | Management response in the SOC 2 states automation was added in 2026-05. Re-check in the next report | Low |
| V-10 | No right-to-audit clause | VR-13 | STA-09.1 | Low | Accept evidence-on-request plus a right to audit after a breach (addendum §7) | Low |

## 3. CUECs CivicStack must operate

The SOC 2 lists complementary user entity controls. If CivicStack doesn't perform them, the vendor's controls don't fully work. They become CivicStack's own control obligations:

| CUEC (from the SOC 2) | CivicStack control | Status |
|---|---|---|
| Customers protect and rotate API credentials | API key in AWS Secrets Manager, rotated every 90 days (IA-5) | Implemented |
| Customers restrict API access to known source IPs | Vendor allow-list contains the HAP NAT gateway IPs only (SC-7) | Implemented |
| Customers send only data needed for verification | HAP sends name, DOB, SSN only, with no documents (PT-2 minimization) | Implemented |
| Customers review vendor-provided access logs | **Not performed** → add to the AU-6 weekly review | **New action** |

## 4. Overall rating

| | Before treatment | After contract addendum + compensating controls |
|---|---|---|
| Vendor risk | **High** (V-1, V-2) | **Moderate** (V-4 remains; V-3 Low pending FIDO2) |
| Decision | — | **Approve with conditions.** Accept V-3 and V-4 by memo ([04](04-risk-acceptance-memo.md)) |
