# Phase 4: Partner swap and peer review

## GDPR Audit  | Ecommerce Company GmbH

**Reviewer:** Dilia Navarro


---

## Scoring key

| Score | Meaning |
|---|---|
| 1 | Does not meet the criterion: not addressed or addressed incorrectly |
| 2 | Partially meets the criterion: present but has relevant gaps |
| 3 | Fully meets the criterion: specific, correct, and requires no further work |


# GDPR Memo Scorecard — Ecommerce Company GmbH

| Criterion | Score (1–3) | Comment |
|---|---|---|
| Clear bottom-line recommendation | 3 | Bottom line is present, direct, and actionable: "Go with conditions" with a one-sentence reason identifying the two specific gaps. |
| Lawful basis selection is justified | 3 | Consent (ePrivacy / Art. 6(1)(a)) and legitimate interests (Art. 6(1)(f)) are correctly identified per purpose; the distinction between the cookie layer and the profiling purpose is maintained. |
| Top actions are specific and sequenced | 3 | Actions are concrete, vendor-named, and logically ordered. Revised sequence following review: (1) Update DataPulse DPA and SCCs → (2) Conduct DPIA → (3) Audit cookie consent layer and update privacy notice in light of DPIA findings. |
| Residual risks are named honestly | 3 | Three residual risks identified. Additional risk flagged: if DataPulse's pipeline generates email subject lines using a generative model, Art. 50 AI Act transparency obligations may apply — requiring disclosure that content is AI-generated. This is currently undocumented and not covered by the existing DPA or privacy notice. |
| Law stacking is addressed (AI Act / ePrivacy) | 2 | ePrivacy is addressed in the memo (cookie consent layer, device-level data). AI Act is not addressed in the memo itself but is covered in the audit worksheet, where the recommendation engine is classified as **minimal risk** — no prohibited-use category, no Annex III high-risk application — with a caveat around Art. 50 transparency obligations if AI-generated subject lines are in use. |


---

## Client Response

Thank you for the thorough advisory note. We accept the three recommendations as sequenced and will prioritise executing the updated DPA and SCCs with our U.S. vendor before the next scheduled retraining cycle. We have noted the residual risks, in particular the erasure-against-model-weights issue and the DPF instability exposure, and will ensure these are escalated to board level and documented as accepted risks in our internal risk register.