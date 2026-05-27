# Phase 1: Build the fact pattern

### Fact Pattern:

**Scenario: LLM Fine-Tuning on B2B SaaS Support Logs**

The client is a mid-sized B2B SaaS company (approx. 150–400 employees) headquartered in Hamburg, Germany, operating in the enterprise software sector and generating the majority of its revenue from subscription contracts with business customers across the EU, the United States, the United Kingdom, and the Asia-Pacific region. The company intends to fine-tune a large language model on approximately two years of archived live-chat support logs, a dataset likely comprising tens of thousands of conversation threads and containing directly identifiable personal data — specifically the full names, business email addresses, job titles, and IP addresses of the human support agents and the end-user representatives of its corporate customers who initiated or participated in those chats, as well as free-text complaint and query content that may incidentally include sensitive operational, contractual, or financial information about the customer organisations. 

The data subjects are therefore a mixed population: employees of the client company (the support agents) and employees or authorised representatives of third-party business customers, located across multiple jurisdictions including EU/EEA Member States, the United Kingdom, the United States, and potentially further third countries. 

For the fine-tuning workload, the company plans to use a U.S.-based foundation model provider and cloud infrastructure vendor — either via API-based training services or a managed MLOps platform — meaning raw or minimally pre-processed training data will be transferred to and processed by a non-EU entity acting as a data processor. The resulting fine-tuned model is intended to power an internal customer-service assistant that autonomously handles or triages incoming support requests, drafts or sends responses, and potentially classifies tickets by urgency or escalation risk. 

While the system is not presented as making legally binding decisions, automated triage and escalation scoring may produce similarly significant effects on the quality and speed of service received by data subjects, and the model's outputs will directly influence how support staff — or the system itself — responds to individual complaints, placing this use case at the boundary of Art. 22 GDPR and the AI Act's risk classification framework.

# Phase 2: Mini GDPR audit worksheet

### Section A — Data Map

> **Scenario:** LLM fine-tuning on B2B SaaS support logs | Client HQ: Hamburg, Germany

| Field | Your Answer |
|---|---|
| **Categories of personal data** | Full names and business email addresses of support agents (client employees) and customer-side end-user representatives; job titles; IP addresses captured in chat metadata; free-text complaint and query content (may incidentally contain financial, contractual, or operational details about customer organisations) |
| **Sources (where data comes from)** | Internal live-chat support platform logs archived over a two-year period; data was originally collected directly from data subjects (agents and customer representatives) during active support sessions |
| **Purpose(s) — one row per purpose** | **P1:** Original collection purpose — provision of customer support services under B2B SaaS contracts **P2:** New/secondary purpose — fine-tuning a proprietary LLM to automate or assist future customer-service interactions **P3:** Ongoing model operation — automated triage, response drafting, and escalation scoring of incoming support tickets |
| **Lawful basis per purpose** | **P1:** Art. 6(1)(b) GDPR — processing necessary for performance of a contract (support obligations under SaaS agreement); for agents: Art. 6(1)(f) legitimate interests (employer's operational interest in logging support work) **P2:** TBD — legal review required; most likely candidate is Art. 6(1)(f) legitimate interests (LIA required: *purpose* = improving service quality; *necessity* = arguable if pseudonymisation or synthetic data is not feasible; *balancing* = significant risk given re-use of personal data far beyond original context — outcome uncertain without DPA guidance) **P3:** Art. 6(1)(f) legitimate interests, conditional on P2 being lawfully established; automated output must be assessed under Art. 22 if escalation scoring produces similarly significant effects |
| **Retention period per purpose** | **P1:** Duration of customer contract + applicable statutory retention period (HGB § 257: 6 years for business correspondence; UStG § 147: 10 years where invoicing-related) **P2:** Training dataset should be deleted or irreversibly anonymised immediately after fine-tuning run is complete; no ongoing retention of raw logs justified **P3:** Model weights do not constitute personal data per se, but any inference logs (inputs/outputs during live operation) should be retained only as long as necessary for quality assurance — suggested maximum 90 days unless a specific legal basis extends this |
| **Recipients and sub-processors** | Internal: ML engineering team (Hamburg); customer support team (Hamburg and remote) — acting as authorised staff, not separate recipients. External processors: U.S.-based foundation model / MLOps vendor (receives training data for fine-tuning via API or managed platform — **requires DPA under Art. 28**); cloud infrastructure provider (may be the same U.S. entity or a separate IaaS vendor); potentially a third-party data labelling or pre-processing service if logs are cleaned externally |
| **International transfers and transfer mechanism** | Transfer to U.S.-based vendor(s) constitutes a Chapter V transfer to a third country. Applicable mechanism depends on vendor's status: if vendor participates in the **EU–U.S. Data Privacy Framework (DPF)** (adequacy decision, July 2023), transfer may rely on that — but DPF stability risk should be noted (ongoing legal challenges). If DPF not available: **Standard Contractual Clauses (SCCs), 2021 Moduleset 2** (controller-to-processor) are the fallback, supplemented by a **Transfer Impact Assessment (TIA)** given U.S. intelligence access laws (FISA § 702, EO 14086). UK data subjects require a separate **UK IDTA** or UK Addendum to SCCs. No adequacy decision covers the U.S. unconditionally — TIA is best practice in all cases |

---

### Section B — Risk and Rights

* **1.- Are any special-category data present or inferable from the outputs (Article 9)?**

No special-category data is explicitly collected, but it is **readily inferable** from free-text complaint content. Support conversations may reveal health conditions (e.g., a user explaining an absence), trade-union membership, financial distress, or immigration status incidentally embedded in complaint narratives. Because the LLM is trained on raw, unfiltered logs, the model may learn and later reproduce or act upon such inferences — triggering Art. 9 obligations even absent deliberate collection. A pre-training data audit and redaction pipeline is strongly advisable before any transfer to a processor.

---

* **2.- Is there automated decision-making with legal or similarly significant effects (Article 22)? If yes, what safeguard applies?**

The escalation scoring and triage classification functions sit at the boundary of Art. 22: they do not produce legally binding outcomes, but automated deprioritisation of a complaint can materially delay resolution, affecting contractual service levels and, for individual end-users, access to a product they depend on professionally — this likely meets the **"similarly significant effect"** threshold as interpreted by the EDPB (Guidelines 05/2020). If Art. 22 applies, the available safeguards under Art. 22(2) are: **(a)** necessity for contract performance, **(b)** explicit consent, or **(c)** Union/Member State law authorisation — in each case supplemented by the mandatory rights to human review, to contest the decision, and to obtain an explanation. Given the B2B context, Art. 22(2)(a) is the most plausible route, but only if the automated triage is genuinely necessary rather than merely convenient.

---

* **3.- Is a DPIA required? Use the EDPB's nine criteria: explain which apply and why.**

A DPIA is **required**; at minimum four of the EDPB's nine criteria are met, and the German supervisory authority (HmbBfDI — Hamburg's data protection authority) has published a mandatory DPIA list that explicitly covers AI-based profiling systems, making this non-discretionary:

| EDPB Criterion | Applies? | Reasoning |
|---|---|---|
| 1. Evaluation or scoring / profiling | **Yes** | Escalation scoring and ticket classification constitute profiling of data subjects by behavioural inference |
| 2. Automated decision-making with significant effects | **Yes** | See Art. 22 analysis above — triage outcomes affect service quality at individual level |
| 3. Systematic monitoring | **Arguably yes** | Continuous ingestion of support interactions during live model operation amounts to ongoing monitoring of communication behaviour |
| 4. Sensitive data or data of highly personal nature | **Yes** | Art. 9-inferable content in free-text logs; financial and operational data of business customers |
| 5. Data processed at large scale | **Yes** | Tens of thousands of conversations over two years; worldwide data subjects |
| 6. Matching or combining datasets | **Arguably yes** | Fine-tuning combines archived logs with a foundation model trained on third-party corpora — provenance of combined outputs is opaque |
| 7. Data concerning vulnerable subjects | **No / not established** | B2B context; no evidence of consumer or vulnerable-individual exposure |
| 8. Innovative technology or novel organisational solution | **Yes** | LLM fine-tuning for autonomous customer service is an emerging technology with poorly understood risks per Art. 35(1) |
| 9. Prevents data subjects from exercising a right or accessing a service | **Arguably yes** | Automated deprioritisation could effectively deny timely access to support |

EDPB guidance states that meeting **two or more criteria** triggers a DPIA obligation. With at minimum five criteria clearly met here, a DPIA is mandatory before processing begins.

---

* **4.- What data subject friction points are most likely? (Most commonly: right of access, right to erasure, right to object to profiling)**

**Right of erasure (Art. 17):** The hardest operational problem. Once personal data has been used to fine-tune model weights, erasure is technically not equivalent to deleting a database record — the data is distributed across billions of parameters. A credible erasure response requires either retraining the model from scratch (expensive) or demonstrating that the data is no longer "present" in any recoverable sense, which is currently unresolved in EU regulatory guidance. This single issue may be the strongest argument for pseudonymising or synthetically replacing the training corpus before fine-tuning.

**Right of access (Art. 15):** Data subjects (both agents and customer representatives) are entitled to know that their chat logs were used as training data, what inferences were drawn, and to whom the data was transferred — including the U.S. vendor. The company's existing privacy notices almost certainly do not cover this secondary use, creating an immediate transparency deficit under Art. 13/14.

**Right to object to profiling (Art. 21):** Any data subject whose data contributed to the training set, or who is subject to escalation scoring during live operation, has a right to object on grounds relating to their particular situation. In the live-operation phase, objection to automated triage must be operationally actionable — the company needs a documented human-review fallback pathway.

---

* **5.- What is the controller / processor split? Name each entity and its role.**

| Entity | Role | Legal Basis |
|---|---|---|
| B2B SaaS company (Hamburg) | **Data Controller** — determines purposes and means of both original support logging and the fine-tuning project | Art. 4(7) GDPR |
| U.S. foundation model / MLOps vendor | **Data Processor** — processes training data on documented instructions from the controller to perform fine-tuning; has no independent purpose | Art. 4(8) GDPR; Art. 28 agreement required |
| Cloud infrastructure provider (if separate) | **Sub-processor** — provides compute and storage infrastructure on which the processor operates; must be listed and approved under the Art. 28 DPA | Art. 28(2) GDPR |
| External data labelling / pre-processing vendor (if used) | **Sub-processor** — processes a subset of raw logs for cleaning or annotation; same Art. 28 chain applies | Art. 28(2) GDPR |
| Customer organisations (B2B clients) | **Independent controllers** in their own right for their employees' data — the SaaS company may also be acting as a **processor** for those clients regarding the end-user data generated during support, depending on contractual structure | Requires careful review of existing B2B contracts |

---

* **6.- Is a DPA (Data Processing Agreement) needed with any vendor? Which ones?**

A written DPA compliant with Art. 28(3) is **required with every external vendor** in the processor chain. Concretely: the U.S. foundation model/MLOps vendor (highest priority — receives raw training data), the cloud infrastructure provider if separate, and any data labelling service. Each DPA must specify subject matter, duration, nature and purpose of processing, type of personal data, categories of data subjects, and the controller's documented instructions. For U.S.-based processors, the DPA should incorporate the 2021 SCCs Module 2 as the transfer mechanism (or reference the vendor's DPF certification) and append a Transfer Impact Assessment.

---

### Section C — Law Stacking

* **AI Act Cross-Check: What tier did the AI system fall into (or would you hypothesize)? Does the AI Act add any obligation that GDPR does not cover?**

The customer-service LLM most naturally falls into the **Limited Risk** tier under the AI Act (Art. 50 transparency obligations apply: users must be informed they are interacting with an AI system). However, if the escalation-scoring component is read as an AI system used to evaluate individuals in the context of access to services, an argument exists for **High Risk** classification under Annex III, point 5(a) — AI systems used to evaluate creditworthiness or similar eligibility for services — though this is a stretch in a pure B2B support context. The AI Act adds obligations GDPR does not cover: mandatory fundamental rights impact assessment for high-risk systems (Art. 9 AI Act, distinct from the GDPR DPIA), technical documentation and logging requirements (Arts. 11–12), and human oversight measures (Art. 14) — none of which are directly required by GDPR alone. Additionally, as the company fine-tunes a general-purpose AI model, it must assess whether GPAI model transparency obligations (Arts. 53–55) apply to its relationship with the foundation model provider.

---

* **ePrivacy Check: Does the scenario involve cookies, tracking pixels, or device-level data? If yes, does ePrivacy's consent requirement override GDPR's flexibility?**

ePrivacy is **not directly triggered** in the training-data phase, as the fine-tuning pipeline operates on archived server-side logs rather than client-side device access. However, if the deployed customer-service assistant is embedded in a web interface or SaaS dashboard and captures real-time interaction data, session metadata, or uses any client-side storage (cookies, local storage, pixel-level event tracking), the ePrivacy Directive (and its forthcoming Regulation) **would** apply — requiring prior informed consent for any non-strictly-necessary storage or access to terminal equipment, and that consent requirement is not overridable by invoking GDPR's legitimate interests basis, since ePrivacy operates as *lex specialis* and forecloses that flexibility at the device-access layer.

---

* **Data Act Check: Is there connected product or cloud switching data involved? (Usually N/A for most AI scenarios — but flag it if your scenario touches IoT or infrastructure.)**

The Data Act is **not materially engaged** in this scenario. There is no connected product (IoT device) generating the data, and the scenario does not involve cloud-switching or interoperability obligations under the Data Act's Chapter VI provisions. The only marginal contact point would be if the U.S. MLOps vendor's contract creates lock-in around the fine-tuned model weights or training artefacts — in that case, the Data Act's cloud-switching facilitation obligations (Art. 23–31) could theoretically be invoked if the company later wishes to migrate to a different vendor and the processor impedes portability of the model or the underlying data. Flag for contractual review, but not a primary compliance risk here.

