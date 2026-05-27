# Phase 3: Client recommendation memo

---

**PRIVILEGED AND CONFIDENTIAL — ADVISORY MEMORANDUM**
**To:** Legal Team / CTO, SaasX GmbH, Hamburg
**From:** Dilia Navarro
**Re:** LLM Fine-Tuning on Support Logs — GDPR & AI Act Readiness
**Date:** May 2026

---

**Bottom line: Go — but only with conditions met first.**
The project is legally viable, but as currently scoped it would begin in breach of GDPR on at least three independent grounds. Do not transfer data to any vendor, and do not initiate fine-tuning, until the three actions below are complete.

---

**Top Three Actions**

**(1) Pseudonymise the training corpus before anything else moves.**
Before any data leaves your environment — including for pre-processing or upload to the MLOps vendor — run the archived chat logs through a structured redaction pipeline: strip or hash names, email addresses, and IP addresses, and flag free-text fields for automated PII(Personally Identifiable Information) scrubbing. This is not optional hygiene; it is the single step that most directly reduces your Art. 9 exposure, strengthens your legitimate interests balancing under Art. 6(1)(f), and significantly narrows the blast radius if the U.S. transfer mechanism is later challenged. Budget for this before you budget for compute.

**(2) Execute a compliant Art. 28 DPA with the U.S. vendor and confirm your transfer mechanism.**
Check whether the vendor holds a current Data Privacy Framework certification. If yes, document reliance on the EU–U.S. DPF adequacy decision and keep a copy on file. If not — or if you have any doubt — attach the 2021 SCCs Module 2 to the DPA and complete a Transfer Impact Assessment before signing. This must be done before a single byte of personal data crosses the border. Also confirm the vendor's sub-processor list and ensure it is incorporated into your agreement.

**(3) Complete a DPIA(Data Protection Impact Assessment) and update your privacy notices before go-live.**
A DPIA is mandatory here — there is no discretion on this point given the scale, the novel technology, and the automated scoring function. Run it in parallel with actions one and two so it does not delay launch. Simultaneously, your existing privacy notices do not cover fine-tuning or automated triage as processing purposes; data subjects have a right to know. Draft a supplementary notice covering the new purposes, the U.S. transfer, and the logic of the escalation-scoring function, and publish it before the model goes live.

---

**Residual Risks — Even If You Do Everything Right**

**Erasure requests against model weights.** Pseudonymisation reduces the risk but does not eliminate it. If a data subject successfully argues their data influenced the model and demands erasure under Art. 17, there is currently no regulatory consensus on what a compliant response looks like short of full retraining. This risk cannot be contracted away.

**DPF instability.** The EU–U.S. Data Privacy Framework is currently subject to legal challenge before the CJEU. If it is invalidated — as its two predecessors were — any transfer relying solely on DPF adequacy becomes unlawful overnight. Maintain SCCs as a parallel fallback mechanism from day one rather than treating them as a contingency.

**Regulatory unpredictability at the Hamburg DPA.** The HmbBfDI has historically taken assertive positions on AI and data re-use. Even a well-documented legitimate interests assessment for the fine-tuning purpose may not survive supervisory scrutiny. There is genuine legal uncertainty here, and no amount of documentation eliminates the possibility that the authority concludes the secondary purpose is incompatible with the original collection. Your DPIA should explicitly address this and record that the risk was acknowledged at board or senior management level.

---

*This note reflects the regulatory position as of May 2026 and is intended as internal advisory input, not as formal legal opinion.*