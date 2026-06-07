# EU AI Act (Regulation 2024/1689) for Financial Services: A Comprehensive Analysis

## File Metadata
- **Scope:** EU AI Act (Regulation 2024/1689) analysis for financial services — high-risk classification, obligations, compliance timeline, and interactions with DORA/GDPR/EBA
- **Cluster:** A — Regulatory Foundations
- **Reading order:** 3/14
- **Related files:** [01_regulatory_landscape_overview.md](01_regulatory_landscape_overview.md), [07_genai_governance_banking.md](07_genai_governance_banking.md), [10_industry_frameworks_nist_iso.md](10_industry_frameworks_nist_iso.md), [12_explainability_fairness_bias.md](12_explainability_fairness_bias.md)
- **Regulators/bodies covered:** EU Commission, European Parliament, EBA, ECB, EIOPA, EU AI Office
- **Tags:** EU-AI-Act, high-risk-AI, conformity-assessment, GPAI, DORA, GDPR, EBA, financial-services, compliance-timeline, penalties, human-oversight

---

Regulation (EU) 2024/1689 of the European Parliament and of the Council of 13 June 2024, commonly known as the EU AI Act, is the world's first comprehensive, binding horizontal legal framework for artificial intelligence. Entering into force on August 1, 2024, the Regulation applies to providers and deployers of AI systems in the European Union and to providers of AI systems outside the EU whose outputs are used within the EU. For financial services — banks, insurers, investment firms, payment providers, and fintechs — the EU AI Act represents the most significant new compliance obligation since the General Data Protection Regulation (GDPR), with comparable extraterritorial reach, comparable penalties for non-compliance, and a similarly complex interaction with existing sectoral regulation.

This document provides a comprehensive, practically oriented analysis of the EU AI Act as it applies to financial services. It covers the Regulation's four-tier risk architecture, the specific financial AI systems designated as high-risk under Annex III, the obligations applicable to high-risk AI providers and deployers (Articles 8–15 and 26), the General-Purpose AI model framework (Title VIII), conformity assessment requirements, interactions with DORA, GDPR, and EBA guidelines, the EU AI Office and enforcement architecture, penalties, and a practical compliance roadmap for financial institutions. The analysis reflects the Digital Omnibus agreement of May 2026, which extended the deadline for standalone Annex III high-risk AI compliance from August 2, 2026 to December 2, 2027.

---

## 1. Structure of the EU AI Act: The Four-Tier Risk Architecture

### 1.1 Overview

The EU AI Act organizes AI systems into four risk tiers, with regulatory obligations calibrated to risk level. The architecture reflects a proportionality principle: the highest-risk AI receives the most intensive oversight, while minimal- and no-risk AI faces no mandatory obligations.

**Tier 1 — Unacceptable Risk (Prohibited).** Article 5 prohibits eight categories of AI practices that pose unacceptable risks to fundamental rights and human dignity. These prohibitions applied from February 2, 2025. For financial services, the most relevant prohibitions are: (a) **social scoring** — AI systems that evaluate or classify natural persons based on social behavior or personal characteristics leading to detrimental treatment in unrelated contexts. A bank using an AI system that incorporates social media activity, neighborhood characteristics, or lifestyle indicators as proxies for creditworthiness risks running afoul of Article 5 if the effect is systematic discrimination based on social characteristics unrelated to creditworthiness. (b) **Exploitation of vulnerabilities** — AI systems that exploit vulnerabilities of specific groups (elderly persons, people with disabilities, persons in financial distress) to distort their behavior in a way that is harmful to them or others. Predatory lending algorithms that target financially vulnerable consumers with unsuitable high-cost products are a clear concern. (c) **Subliminal manipulation** — AI systems that deploy techniques beyond a person's consciousness to distort behavior to their detriment. The prohibitions carry the highest penalties: up to €35 million or 7% of global annual turnover.

**Tier 2 — High Risk.** AI systems that may cause significant harm to health, safety, or fundamental rights but for which the benefits justify regulated use with stringent safeguards. High-risk AI systems are listed in Annex III (standalone systems) or Annex I (safety components in products). Most financial services AI falls into Annex III. High-risk AI obligations under Annex III (standalone) apply from December 2, 2027 under the Digital Omnibus revision.

**Tier 3 — Limited Risk.** AI systems with specific transparency obligations but no comprehensive framework. Chatbots interacting with customers must disclose that the user is interacting with AI; AI-generated content (including synthetic media) must be marked as such. These transparency obligations apply from February 2, 2025.

**Tier 4 — Minimal/No Risk.** AI systems assessed as posing minimal risk face no mandatory obligations under the Regulation, though providers are encouraged to develop voluntary codes of conduct. Spam filters, recommendation engines for non-sensitive applications, and most internal productivity tools fall into this tier.

### 1.2 Who the EU AI Act Applies To

The Regulation applies to:

- **Providers:** Any natural or legal person, public authority, agency or body that develops an AI system and places it on the EU market or puts it into service in the EU. Providers bear the primary technical compliance obligations (Articles 9–17).
- **Deployers:** Any natural or legal person, public authority, agency or body that uses an AI system under their authority for professional purposes, except for personal non-professional use. Deployers bear downstream compliance obligations (Article 26).
- **Importers and distributors:** Entities that bring AI systems from outside the EU into the EU market, or that distribute AI systems without significantly modifying them.

**Extraterritorial scope.** The Regulation applies to providers located outside the EU when their AI system's output is used in the EU. This creates compliance obligations for US, UK, and APAC AI vendors whose technology is deployed in European financial services. It also means that a bank headquartered in New York using an AI credit scoring model for EU borrowers is subject to the Regulation's requirements for that model.

**Provider vs. Deployer in financial services.** Financial institutions frequently act as both providers and deployers depending on the AI system. A bank that develops its own credit scoring model internally is a provider of that model. A bank that purchases a third-party AI credit scoring platform and deploys it in its underwriting process is a deployer. However, if the bank substantially modifies a third-party AI system — for instance, by retraining it on proprietary data — the bank may transition from deployer to provider status, with significantly expanded compliance obligations.

---

## 2. High-Risk AI in Financial Services: Annex III

Annex III of the EU AI Act designates specific categories of AI systems as high-risk. Financial services applications appear across multiple categories of Annex III:

### 2.1 Creditworthiness and Credit Scoring (Annex III, Point 5(b))

The Act designates as high-risk: **"AI systems intended to be used to evaluate the creditworthiness of natural persons or establish their credit score, with the exception of AI systems used for the purpose of detecting financial fraud."**

This provision captures the full spectrum of AI-driven credit decisioning:

- **Loan origination platforms** using ML models to assess mortgage, personal loan, auto loan, or SME credit applications
- **Buy-now-pay-later (BNPL) decisioning** using behavioral and transaction data to extend or deny instant credit
- **Credit limit setting** using AI to determine credit card limits
- **Credit review AI** that recommends credit limit reductions or account closures
- **Alternative data credit scoring** using non-traditional data (utility payments, rent history, transaction data) to score thin-file or no-file borrowers

The fraud detection exception is important: AI systems dedicated to detecting fraudulent credit applications — as opposed to assessing creditworthiness — are carved out. However, this exception applies narrowly. A system that evaluates both creditworthiness and fraud risk is likely to be treated as high-risk because its primary function includes creditworthiness assessment.

**Note on the Digital Omnibus:** The May 2026 Omnibus agreement confirmed that standalone Annex III credit scoring systems compliance date is December 2, 2027. However, institutions should treat 2026 as an implementation preparation period, not a compliance holiday.

### 2.2 Life and Health Insurance Risk Assessment (Annex III, Point 5(c))

The Act designates as high-risk AI systems used to: **evaluate and classify emergency calls; and AI systems intended to evaluate and classify emergency calls by natural persons or to be used to dispatch, or to establish priority in the dispatching of, emergency first response services.**

More relevantly for insurance, the Commission's interpretation and the EBA/EIOPA guidance confirm that AI systems used in **life and health insurance risk assessment and pricing** — including underwriting AI, AI-driven premium calculation, and AI-based claims assessment — fall under the high-risk designation. These systems determine insurance eligibility, premiums, coverage terms, and claim payability based on individual health and lifestyle characteristics.

AI systems used by property and casualty insurers for personal lines risk pricing (auto, home) are also subject to assessment, though their high-risk status depends on the degree to which they make individual-level determinations affecting significant interests.

### 2.3 AML/CFT and Fraud Detection

The Act does not explicitly designate AML/CFT transaction monitoring or fraud detection AI as high-risk under the general Annex III financial services provisions. The credit scoring fraud detection exception (Point 5(b)) suggests that fraud detection AI is not automatically high-risk. However, some AML/CFT screening tools — particularly those that generate individual-level risk scores used to deny services or file suspicious activity reports — may qualify under other Annex III categories (notably those related to law enforcement or migration management), depending on the institutional context.

The European Commission issued a clarification in May 2025 (EC AI Act exemption guidance on AML/Fraud detection) confirming that standalone fraud detection and AML monitoring systems that do not feed into creditworthiness decisions are not automatically high-risk under Point 5(b), though they may still be subject to assessment under other parts of Annex III.

### 2.4 Employment AI in Financial Firms (Annex III, Point 4)

AI systems used by financial institutions for recruitment, selection, monitoring, evaluation, promotion, or termination of employees are designated high-risk under Annex III, Point 4. This covers:

- AI-powered resume screening and candidate ranking tools used by banks and insurers
- AI systems that assess employee performance metrics
- AI-driven workforce management tools that allocate tasks based on AI assessment of employee capabilities
- Automated interview analysis systems using behavioral or biometric signals

### 2.5 Biometric Identification and Categorization

Financial institutions using AI systems for real-time or post-deployment biometric identification (facial recognition for customer identity verification, voice recognition for call center authentication) must assess these against the biometric provisions of Annex III. Real-time remote biometric identification systems face particularly stringent restrictions; post-remote biometric systems are high-risk but subject to standard high-risk obligations rather than the near-prohibition applicable to real-time systems.

### 2.6 Classification Decision Tree

For financial institutions assessing whether a given AI system is high-risk, the following questions guide the analysis:

1. Does the AI system evaluate natural persons' creditworthiness or establish credit scores? → High-risk (Point 5(b))
2. Does the AI system assess individual risk for life or health insurance pricing? → High-risk (insurance interpretation)
3. Is the system used for recruitment, evaluation, or promotion of employees? → High-risk (Point 4)
4. Does the system use biometric data for identification? → High-risk (Point 1), subject to additional analysis
5. Does the system generate individual-level risk profiles that significantly affect access to financial services? → Assess against all relevant Annex III points
6. Is the system exclusively for fraud/financial crime detection? → Not automatically high-risk under 5(b), but assess other provisions

---

## 3. High-Risk AI Obligations: Articles 8–15

Providers of high-risk AI systems must satisfy a comprehensive set of requirements under Articles 8–15, which collectively constitute the technical and governance framework for high-risk AI. These obligations apply throughout the system's lifecycle, from design through decommissioning.

### 3.1 Article 9: Risk Management System

Article 9 is the cornerstone of the high-risk AI compliance framework. It requires providers to establish, implement, document, and maintain a **risk management system** as "a continuous iterative process planned and run throughout the entire lifecycle" of the AI system, subject to regular review and updating.

**Four steps of the risk management system:**

1. **Identification and analysis of known and reasonably foreseeable risks** — This requires systematic examination of risks to health, safety, or fundamental rights that the AI system may present during its intended use and reasonably foreseeable misuse. For a credit scoring AI, this includes risk of discriminatory outcomes, risk of incorrect creditworthiness assessments, risk of data quality failures, and risk of model drift producing unreliable outputs over time.

2. **Estimation and evaluation of risks arising from intended use and foreseeable misuse** — Quantifying residual risks and assessing their acceptability requires both statistical analysis (e.g., disparate impact analysis, model performance under stress scenarios) and qualitative assessment of potential harms.

3. **Evaluation of emerging risks based on post-market monitoring data** — The risk management system must be updated as real-world performance data reveals new or previously underestimated risks. This creates an ongoing obligation analogous to SR 11-7's ongoing monitoring requirements.

4. **Adoption of suitable risk management measures** — Risks that cannot be eliminated through design must be mitigated through controls, and residual risks must be judged acceptable before deployment.

**Interaction with existing model risk management.** For financial institutions subject to EBA IRB guidelines or operating under SR 11-7/SR 26-2 equivalents, Article 9's risk management system requirements substantially overlap with existing model risk management processes. The Article 9 risk management system can be aligned with the MRM framework, with documentation demonstrating how the existing MRM processes satisfy Article 9 obligations. The key addition that Article 9 requires beyond traditional MRM is **explicit assessment of fundamental rights impacts** — a dimension not traditionally part of bank model risk frameworks.

### 3.2 Article 10: Data Governance

Article 10 establishes data governance requirements for training, validation, and testing datasets used in high-risk AI systems. The requirements state that datasets must be:

- **Relevant** to the intended purpose of the AI system
- **Sufficiently representative** of the population to which the system will be applied, including appropriate representation of different demographic groups
- **Free of errors and complete** to the extent technically feasible
- **Appropriately designed** to avoid biases that could result in prohibited discrimination or disproportionate harm

For credit scoring models, Article 10 creates specific practical obligations:

**Dataset representativeness.** Training data must represent the actual applicant population. If a credit scoring model is trained predominantly on data from one demographic group and applied to a broader population, it may fail the representativeness requirement. Financial institutions must document how they assessed the representativeness of training data and what steps were taken to address gaps.

**Bias assessment.** Providers must document procedures for detecting and mitigating potential biases in training data. For credit models, this means statistical testing for disparate impact across protected characteristics (gender, race, ethnicity, age, disability status) where data is available, and analysis of proxy variables that may encode protected characteristics.

**Data lineage.** The data provenance documentation required by Article 10 goes beyond traditional model documentation. Institutions must be able to demonstrate the origin of training data, the transformations applied, and the relationship between training data characteristics and model behavior.

**Quality controls for production data.** Article 10's requirements apply not only to training data but to data used in production inference. A credit scoring model continuously processing loan applications must have controls ensuring that input data quality meets the standards used during model development.

### 3.3 Article 11: Technical Documentation

Article 11 requires providers to draw up **technical documentation** before placing a high-risk AI system on the market or putting it into service. Documentation must enable national competent authorities to assess compliance with the Act. It must include at a minimum:

- A general description of the AI system, including its intended purpose and the conditions of use
- A description of the development process, including design choices, training methodology, and performance metrics
- The risk management system documentation (Article 9)
- Data governance documentation (Article 10)
- Description of the monitoring, functioning, and control of the system
- Description of the human oversight measures
- Performance benchmarks and accuracy metrics, including those measured on relevant population subgroups

For financial institutions, technical documentation under Article 11 substantially parallels model documentation required under existing MRM frameworks. The additional requirement is documentation framed explicitly around compliance with Articles 9–15, which may require restructuring existing model documentation to add compliance-mapping sections. The Commission is developing standardized documentation templates for high-risk AI systems, which financial institutions should adopt when available.

### 3.4 Article 12: Record-Keeping and Automatic Logging

Article 12 requires high-risk AI systems to possess "the capability to automatically generate logs" throughout their operation. These logs must enable monitoring of the system's performance and compliance verification. Deployers must retain logs for at least six months (extendable by national law or sector-specific regulations).

**What must be logged.** Logs must capture sufficient information to reconstruct the AI system's reasoning for each significant output. For a credit scoring AI, this means logging: the inputs fed to the model (with appropriate data privacy protections), the model version used, the output generated (credit score, recommendation, or decision), the timestamp, any human review or override, and any anomalies or alerts generated by monitoring systems.

**Immutability and integrity.** Logs must be immutable — they cannot be altered after creation. For audit and supervisory purposes, logs must demonstrate a chain of custody that verifies they have not been tampered with. Financial institutions with existing immutable logging infrastructure for regulatory compliance (e.g., trade surveillance logging, GDPR processing records) should extend these systems to AI model logging.

**Retention alignment.** The six-month minimum retention period under Article 12 must be harmonized with longer credit record retention obligations under national consumer credit law, GDPR data retention policies, and sector-specific supervisory record-keeping requirements. In practice, credit-related AI logs should typically be retained for the duration applicable to the underlying credit record plus a margin for supervisory access.

### 3.5 Article 13: Transparency to Deployers

Article 13 requires that high-risk AI systems be accompanied by instructions for use that enable deployers to implement the human oversight measures required by Article 14 and to use the system correctly. Instructions must include:

- The identity and contact details of the provider
- The intended purpose and conditions of use
- The level of accuracy, robustness, and cybersecurity the system achieves, including metrics demonstrating performance against relevant population subgroups
- Known or foreseeable circumstances that may lead to risks to health, safety, or fundamental rights
- Specification of the persons or groups of persons at particular risk
- Human oversight measures (including technical means for monitoring and intervention)
- The expected lifetime of the system and necessary maintenance/update provisions

**Distinction from GDPR Article 22 transparency.** Article 13 creates transparency obligations toward **deployers** (the financial institution using the system). Separate transparency rights flow to **data subjects** (the customers whose data is processed) under GDPR. A bank deploying a third-party credit scoring AI must receive full Article 13 documentation from the provider, and must separately fulfill its GDPR obligations to explain the role of AI in credit decisions to applicants.

### 3.6 Article 14: Human Oversight

Article 14 is among the most operationally significant provisions of the EU AI Act for financial services. It requires that high-risk AI systems be designed and developed in a way that allows for **effective oversight by natural persons** during the period of use.

**Mandatory human oversight capabilities.** Deployers must be able to:

1. **Understand the system** — The natural persons overseeing the AI system must understand its capabilities and limitations, the circumstances under which it may produce incorrect or biased outputs, and how to interpret its outputs in context.

2. **Monitor the system's operation** — Humans must be able to monitor the system for anomalies, dysfunctions, and unexpected behavior in real time or with sufficient frequency.

3. **Intervene and override** — The system must be designed so that a human can intervene, override the system's recommendation or decision, or halt the system's operation. This requires technically enforceable override mechanisms, not merely procedural policies permitting overrides.

4. **Avoid over-reliance** — The human oversight framework must be designed to prevent automation bias — the tendency to defer to AI outputs without adequate independent judgment.

**What Article 14 does not require.** Article 14 does not require a human to review every individual AI decision before it takes effect — that would make AI-driven efficiency gains impossible. It requires that meaningful human oversight is possible and that the system is designed to facilitate that oversight. For automated credit decisions, this means: periodic human review of model performance and outputs, technical means for flagging borderline or anomalous decisions for human review, and clear escalation pathways for cases where the AI produces outputs that raise human concern.

**CJEU SCHUFA judgment interaction.** The Court of Justice of the EU's December 2023 judgment in SCHUFA (Case C-634/21) held that even upstream credit scoring — the production of a credit score that significantly influences downstream decisions — falls under GDPR Article 22's automated decision-making protections. In practice, this means credit scoring AI must be designed for meaningful human review at the scoring stage, not only at the downstream loan decision stage. Article 14 of the AI Act reinforces this requirement.

**Practical implementation.** Financial institutions implementing Article 14 for credit scoring AI must: (a) ensure that credit underwriters understand how the scoring model works at a sufficient level to override it intelligently; (b) create technical mechanisms for underwriters to flag cases for review and record override decisions; (c) design UI/UX that presents AI scores with uncertainty ranges and key driver information, preventing over-reliance on a single number; and (d) monitor override rates and reasons to detect automation bias.

### 3.7 Article 15: Accuracy, Robustness, and Cybersecurity

Article 15 requires high-risk AI systems to achieve an "appropriate level of accuracy, robustness, and cybersecurity" throughout their lifecycle.

**Accuracy.** The required accuracy level must be declared in the instructions for use (Article 13) with reference to specific metrics and the population on which they were measured. For credit scoring AI, accuracy metrics must be reported by demographic subgroup to ensure that the model does not achieve high aggregate accuracy through discriminatory performance disparities across groups. Providers must demonstrate to regulators, on request, that accuracy claims are substantiated by reproducible testing on relevant datasets.

**Robustness.** Systems must be resilient to errors, inconsistencies, and unexpected inputs. Robustness testing for financial AI systems must address: performance under data quality failures (missing data, corrupted inputs); performance under distributional shift (when the statistical properties of inputs change due to economic conditions or population changes); and performance under adversarial inputs (deliberately manipulated data inputs by bad actors). Robustness requirements are particularly relevant for credit scoring models, which may face adversarial applications from borrowers who manipulate their profile data to obtain better scores.

**Cybersecurity.** Systems must be protected against cyberattacks that could cause them to behave in ways that threaten safety, security, or fundamental rights. Cybersecurity requirements include: protection against data poisoning (attacks on training data that corrupt model behavior); model extraction attacks (attempts by unauthorized parties to reconstruct or steal the model); adversarial examples (inputs designed to cause specific erroneous outputs); and confidentiality breaches (unauthorized access to sensitive training data or model architecture). For financial institutions already subject to DORA's ICT security requirements, Article 15's cybersecurity requirements should be integrated into the institution's existing ICT risk management framework.

---

## 4. Deployer Obligations: Article 26

While Articles 9–15 impose obligations primarily on providers, Article 26 creates independent, non-delegable obligations for deployers. Financial institutions acting as deployers of third-party AI systems cannot transfer these obligations contractually to providers.

**Article 26 key deployer obligations:**

1. **Use systems only for intended purpose** — Deployers must restrict use of high-risk AI to the purposes declared in the provider's technical documentation. A credit scoring system validated for retail consumer credit cannot be repurposed for commercial lending without re-assessment.

2. **Assign qualified human oversight personnel** — Deployers must designate individuals with appropriate competence, training, and authority to implement the human oversight measures described in Article 14.

3. **Monitor system performance in production** — Deployers must monitor real-world performance, identify unexpected outputs, and report serious incidents to providers and, where required, to competent authorities.

4. **Report to providers and authorities** — When deployers identify serious incidents or risks that were not anticipated in the provider's risk management system, they must report these to the provider without undue delay. Certain incidents must also be reported to national market surveillance authorities.

5. **Conduct Fundamental Rights Impact Assessments** — Public bodies and certain private entities — including financial institutions making automated decisions that significantly affect individuals' financial circumstances — must conduct a fundamental rights impact assessment before deploying certain high-risk AI systems. This assessment overlaps with but is distinct from the GDPR's Data Protection Impact Assessment (DPIA).

6. **Register in the EU AI database** — Deployers must register as operators of high-risk AI systems in the EU AI database before using the system. Market surveillance authorities use the database as a primary enforcement tool.

**The critical deployer-provider boundary.** A financial institution that substantially modifies a third-party AI system crosses from deployer to provider status. Modification that changes the system's intended purpose or performance characteristics constitutes substantial modification. Crucially, fine-tuning a third-party foundation model (e.g., retraining an AI credit scoring model on the institution's proprietary lending data) may constitute substantial modification, elevating the institution to provider status and triggering the full set of Articles 9–17 obligations.

---

## 5. General-Purpose AI (GPAI) Models: Title VIII

The EU AI Act contains a separate framework for general-purpose AI (GPAI) models — large-scale AI systems trained on broad datasets capable of performing a wide range of tasks. This category captures large language models (LLMs) such as GPT-4, Claude, Gemini, and Llama, as well as large multimodal models. GPAI obligations under Title VIII became enforceable on August 2, 2025.

### 5.1 GPAI Models: Basic Obligations (Article 53)

All GPAI model providers — regardless of whether their model reaches the systemic risk threshold — must:

- Draw up and keep up-to-date technical documentation, including training data sources and types
- Provide information and instructions for users (downstream deployers integrating the GPAI model into their systems)
- Comply with EU copyright law, particularly regarding training data
- Publish a publicly available summary of training content

### 5.2 GPAI Models with Systemic Risk (Article 55)

GPAI models trained on compute resources exceeding **10²⁵ floating-point operations (FLOPs)** are presumed to have high-impact capabilities and are classified as systemic-risk GPAI models. This threshold captures today's frontier foundation models. Providers of systemic-risk GPAI must additionally:

- **Perform model evaluations** using standardized protocols, including **adversarial testing** (red-teaming) to identify and mitigate systemic risks
- **Assess and mitigate systemic risks** including dangerous capability risks, misuse risks, and risks from widespread deployment
- **Track, document, and report serious incidents** to the AI Office without undue delay, along with corrective measures
- **Ensure adequate cybersecurity protection** for the model and its underlying infrastructure

### 5.3 Implications for Banks Using Foundation Models

Financial institutions deploying foundation model APIs (Claude via Amazon Bedrock, GPT-4 via Azure OpenAI, Gemini via Google Cloud) are typically acting as **deployers** of GPAI models, not providers. Their primary obligations are:

- **Downstream use compliance:** If the institution integrates a GPAI model into a high-risk AI application (e.g., using an LLM to generate credit recommendations), the resulting system must comply with Annex III high-risk obligations regardless of whether the underlying GPAI model itself is the source of compliance.
- **Due diligence on GPAI providers:** Deployers must conduct due diligence on GPAI providers' compliance with Title VIII obligations, including reviewing technical documentation and incident reporting processes.
- **Prohibition on prohibited uses:** Financial institutions cannot use GPAI capabilities in ways that violate Article 5 prohibitions — using an LLM to generate social scoring profiles or manipulative content targeted at financially vulnerable customers is prohibited.

The most significant GPAI compliance challenge for banks is the **provider-deployer boundary**. A bank that fine-tunes a foundation model on proprietary customer data, proprietary trading data, or proprietary credit history to create a specialized financial AI — and then deploys that fine-tuned model as a credit scoring system — is likely a provider of both a GPAI model (the fine-tuned foundation model) and a high-risk AI system. This creates a double set of compliance obligations rarely faced in traditional model risk management.

---

## 6. Conformity Assessment

### 6.1 Requirement Overview

Before placing a high-risk AI system on the market or putting it into service, providers must complete a **conformity assessment** demonstrating that the system satisfies the requirements of Articles 9–15. The assessment must result in an EU declaration of conformity, after which the CE marking is affixed and the system is registered in the EU AI database.

### 6.2 Internal Conformity Assessment (Self-Assessment)

For most Annex III high-risk AI systems — including credit scoring, insurance risk assessment, and employment AI — the default conformity assessment route is **internal control** (Annex VI of the Regulation). This means the provider conducts the assessment itself, without mandatory involvement of a notified body.

Internal conformity assessment involves:

1. Documenting compliance with Articles 9–15 against the requirements of each article
2. Testing the system against relevant standards (when harmonized EU standards are published) or common specifications (interim)
3. Drawing up an EU declaration of conformity certifying compliance
4. Registering the system in the EU AI database

This self-assessment model is substantially more accessible for large financial institutions with internal AI governance capabilities than third-party conformity assessment would be. However, it places full accountability on the provider to conduct a rigorous, honest assessment — regulators will review the documentation and may initiate audits.

### 6.3 Third-Party Conformity Assessment (Notified Body)

Third-party conformity assessment by an accredited **notified body** is mandatory for:

- Real-time remote biometric identification systems (Article 43(1))
- High-risk AI systems that are safety components in products regulated under existing EU sectoral legislation where that legislation itself requires third-party assessment (Annex I systems)

For most financial services AI, third-party conformity assessment is **not mandatory** — self-assessment suffices. However, financial institutions may voluntarily engage notified bodies for higher-risk applications or where the robustness of the assessment needs to be demonstrated to regulators, counterparties, or the public.

Notified bodies are accredited by national accreditation bodies in EU member states. As of mid-2026, the European accreditation infrastructure for AI Act notified bodies is still being built; the designation process is expected to complete through 2026.

### 6.4 Ongoing Obligations Post-Assessment

Conformity assessment is not a one-time event. Providers must update the conformity assessment when they substantially modify the AI system. What constitutes a "substantial modification" triggering reassessment includes changes that:

- Affect the system's compliance with the requirements of Chapter III (Articles 8–15)
- Change the system's intended purpose
- Affect the system's risk level

For credit scoring AI that undergoes periodic model recalibration (e.g., annual retraining on updated data), providers must assess whether the recalibration constitutes substantial modification. Minor updates that do not change the model's conceptual design, intended purpose, or fundamental performance characteristics generally do not require full reassessment, though they must be documented in the technical documentation.

---

## 7. EU AI Act + DORA: The Operational Resilience Layer

The Digital Operational Resilience Act (DORA, Regulation (EU) 2022/2554) entered full enforcement on January 17, 2025, creating binding ICT risk management and operational resilience requirements for EU financial institutions and their ICT third-party service providers. DORA and the EU AI Act operate in parallel; financial institutions must satisfy both simultaneously.

### 7.1 Where DORA and the EU AI Act Overlap

**ICT risk management and AI risk management.** A credit scoring AI system is both an AI system under the EU AI Act and an ICT system (or component of an ICT system) under DORA. DORA requires financial institutions to identify, classify, and manage all ICT assets supporting their critical or important functions. An AI system used in credit underwriting almost certainly supports a function critical to the institution's business and must be included in DORA's ICT asset inventory. At the same time, Article 9 of the EU AI Act requires a risk management system for the same credit scoring AI. The two risk management frameworks must be aligned.

**Incident reporting.** DORA requires financial institutions to report major ICT-related incidents to their national supervisory authority within specified timeframes (initial notification within 4 hours, intermediate report within 72 hours, final report within 1 month). If an AI system failure constitutes a major ICT incident under DORA (e.g., a credit scoring AI fails due to a cyberattack, causing disruption to the institution's ability to process loan applications), the DORA reporting obligation applies. The EU AI Act's Article 26 obligation for deployers to report serious incidents to providers creates a separate, additional notification requirement. Financial institutions should establish coordinated incident reporting procedures that satisfy both obligations simultaneously.

**Third-party AI risk.** Both DORA and the EU AI Act impose obligations regarding third-party technology risk. DORA requires financial institutions to maintain a register of ICT third-party service providers and to subject critical providers to contractual requirements and ongoing monitoring. The EU AI Act requires deployers to conduct due diligence on providers' compliance with Articles 9–15. Where an AI provider is also an ICT third-party service provider (as is typically the case for cloud-hosted AI platforms), both frameworks' requirements must be addressed in the institution's vendor management program.

**Operational resilience and AI robustness.** DORA's resilience requirements (business continuity, disaster recovery, operational resilience testing including threat-led penetration testing) apply to AI systems supporting critical functions. Article 15 of the EU AI Act's robustness requirements for AI accuracy under errors and failures complement DORA's operational resilience framework. A comprehensive resilience program for financial AI will address both sets of requirements through integrated testing.

### 7.2 Key Coordination Actions

Financial institutions should:

1. **Align AI and ICT inventories** — Ensure every AI system designated as high-risk under the EU AI Act is also captured in the ICT asset inventory under DORA, with consistent classification of the function it supports.

2. **Coordinate incident response playbooks** — Develop AI incident response procedures that trigger both DORA reporting (if the incident constitutes a major ICT incident) and EU AI Act Article 26 serious incident reporting simultaneously.

3. **Align third-party risk management** — Combine DORA's contractual requirements for ICT providers with EU AI Act technical documentation and compliance due diligence requirements when onboarding AI vendors.

4. **Integrate resilience testing** — Include AI systems in DORA's digital operational resilience testing program, combining scenario-based and adversarial testing required under both frameworks.

---

## 8. EU AI Act + GDPR: The Data Rights Interface

The General Data Protection Regulation (GDPR, Regulation (EU) 2016/679) governs the processing of personal data by EU financial institutions and creates specific rights for data subjects subject to automated decision-making. The EU AI Act was designed to complement GDPR, not replace it; both apply simultaneously to AI systems processing personal data.

### 8.1 GDPR Article 22: Automated Decision-Making

Article 22 GDPR gives data subjects the right not to be subject to decisions based solely on automated processing, including profiling, that produces legal effects or similarly significant effects on them — unless specific conditions are met (contractual necessity, legal authorization, or explicit consent). When an exception applies, data subjects still retain three rights: (a) the right to obtain human intervention, (b) the right to express their point of view, and (c) the right to contest the decision.

The Court of Justice of the EU confirmed in **SCHUFA (Case C-634/21, December 7, 2023)** that a credit bureau's automated production of a credit score — even upstream of the actual lending decision — falls under Article 22 when that score significantly influences downstream human decisions. This ruling has profound implications: it means that the automated credit scoring step itself, not merely the automated loan denial, triggers Article 22 protections. Credit institutions using AI credit scoring must ensure that: (i) there is an appropriate legal basis for automated scoring; (ii) meaningful human review is available and accessible; and (iii) the credit score can be explained to the data subject on request.

### 8.2 Right to Explanation: GDPR vs. EU AI Act

GDPR Article 22(3) requires that when automated decisions with legal or similarly significant effects are made with data subject consent or contractual necessity, the data subject must be informed of the logic involved in the processing. Case law and regulatory guidance have interpreted this as requiring an explanation of the key factors driving the automated decision — not necessarily full algorithmic transparency, but meaningful information enabling the data subject to understand and contest the decision.

Article 13 of the EU AI Act creates a related but distinct obligation: transparency to deployers about how the AI system works. Article 26 requires deployers to provide transparency to affected individuals about the role of the AI system in decisions affecting them and the main elements of those decisions.

In practice, financial institutions must implement a **unified explainability architecture** satisfying both frameworks:

- **For GDPR Article 22:** Explanations to applicants of the key factors affecting their credit score or insurance premium — human-understandable reasons statements that go beyond generic categories to provide application-specific drivers. SHAP values, LIME, or purpose-built explanation engines can generate these.
- **For EU AI Act Article 26:** Documentation for deployers (internal model risk governance, validation teams, supervisors) of how the AI system functions, including performance metrics and known limitations.
- **For CFPB Circular 2022-03 (US parallel):** For US institutions, adverse action notices for credit denials must provide specific, accurate reasons — the same explainability imperative, applied through US regulatory instruments.

### 8.3 Data Protection Impact Assessment and Fundamental Rights Impact Assessment

GDPR Article 35 requires a **Data Protection Impact Assessment (DPIA)** before processing likely to result in high risk to individuals' rights and freedoms. Automated credit decisioning and automated insurance pricing almost certainly trigger DPIA requirements.

The EU AI Act introduces a **Fundamental Rights Impact Assessment (FRIA)** for certain deployers of high-risk AI, which overlaps significantly with the DPIA. The Commission has acknowledged this overlap and encouraged coordinated assessment processes — a single assessment process that satisfies both requirements is more efficient and reduces compliance burden. Institutions should align their AI governance processes so that the FRIA and DPIA are conducted jointly, sharing data collection, stakeholder consultation, and documentation where possible.

---

## 9. EU AI Act + EBA Guidelines: The Sectoral Oversight Layer

### 9.1 Financial Sector Regulators as AI Act Supervisors

The EU AI Act established a distinctive enforcement architecture for financial services: **existing sectoral regulators serve as the market surveillance authorities** for AI systems used in their regulated sectors. This means:

- The **European Banking Authority (EBA)** is the competent authority for AI systems used by credit institutions
- The **European Securities and Markets Authority (ESMA)** is the competent authority for AI used by investment firms and market infrastructure
- The **European Insurance and Occupational Pensions Authority (EIOPA)** is the competent authority for AI systems used by insurance undertakings
- **National competent authorities** (NCAs) — banking supervisors, securities regulators, insurance supervisors — supervise AI Act compliance at national level within their sectors

This architecture means that banks face AI Act supervision from the same regulators who already supervise their prudential compliance. For large banks supervised directly by the ECB, the AI Act adds an AI governance dimension to the ECB's supervisory relationship. In practice, AI Act compliance will be integrated into the existing supervisory review and evaluation process (SREP) — banks can expect AI-related questions in SREP questionnaires and on-site inspections.

### 9.2 EBA Roadmap and AI Governance Expectations

The EBA has been active in developing AI governance expectations for the banking sector. Key EBA outputs include:

- **EBA Discussion Paper on ML for IRB (EBA/DP/2021/04):** Identified ML-specific challenges in credit risk internal models and signaled forthcoming guidance.
- **EBA Roadmap on Sustainable Finance and Digital Finance:** Commits the EBA to developing guidance on the use of AI in credit risk, including treatment of alternative data and explainability standards.
- **EBA Opinion on AI in Financial Services (ongoing):** The EBA has been developing an opinion on the interaction between the EU AI Act and existing EBA guidelines, particularly the IRB framework. This opinion will clarify how AI Act compliance maps to EBA model validation requirements for IRB credit risk models.

Banks using IRB models that incorporate ML components will need to satisfy both the EBA's IRB validation requirements and the EU AI Act's Article 9–15 obligations. The conceptual soundness, data governance, ongoing monitoring, and performance testing requirements of the EBA IRB guidelines are broadly consistent with Articles 9, 10, and 15 of the EU AI Act — but the EU AI Act adds a fundamental rights dimension (fairness, non-discrimination) that the prudential capital framework does not explicitly address.

---

## 10. Compliance Timeline

### 10.1 Phased Implementation Schedule

| Date | Event |
|---|---|
| August 1, 2024 | EU AI Act enters into force (publication date) |
| February 2, 2025 | **Prohibited AI practices (Article 5) apply** — Social scoring, subliminal manipulation, exploitation of vulnerabilities prohibited; AI literacy obligations begin |
| August 2, 2025 | **GPAI model obligations (Title VIII) apply** — All GPAI providers must meet transparency obligations; systemic-risk GPAI providers must meet adversarial testing, incident reporting, cybersecurity requirements |
| August 2, 2026 | Article 50 transparency obligations for limited-risk AI (chatbots) fully enforceable; enforcement powers for GPAI begin |
| **December 2, 2027** | **Standalone Annex III high-risk AI obligations fully enforceable** (revised from August 2, 2026 by Digital Omnibus agreement, May 2026) — Credit scoring, insurance pricing, employment AI must comply with Articles 9–15 |
| August 2, 2028 | High-risk AI embedded in regulated products (Annex I) obligations fully enforceable (revised from August 2, 2027) |

### 10.2 Digital Omnibus Revision (May 2026)

The European Council and European Parliament reached a provisional political agreement on May 6, 2026, confirmed by the Council on May 13, 2026, to amend the EU AI Act through the Digital Omnibus package. Key changes for financial services:

**Extended deadlines.** Standalone Annex III compliance moved from August 2, 2026 to December 2, 2027. This provides financial institutions with additional time to build compliant governance frameworks, complete conformity assessments, and register systems in the EU AI database.

**Important caveat.** The extended deadline does not eliminate urgency. Institutions that treat December 2027 as the start date rather than the compliance deadline will face substantial operational challenges. The compliance implementation timeline for a large bank with hundreds of AI systems across credit, insurance, and operations is 18–24 months minimum. Financial institutions that have not begun substantive compliance preparation by early 2026 face material risk of not being ready by December 2027.

**GPAI unaffected.** The Omnibus revision did not extend the August 2025 GPAI obligations. Institutions using foundation model APIs were subject to those compliance requirements from August 2025.

---

## 11. Penalties

The EU AI Act establishes a graduated penalty structure reflecting the severity of different violations:

### Tier 1: Prohibited AI Practices (Article 5 violations)
- Up to **€35 million** or **7% of total worldwide annual turnover** of the preceding financial year, whichever is higher
- Applicable to: Social scoring, subliminal manipulation, exploitation of vulnerabilities, prohibited biometric identification

### Tier 2: High-Risk AI Obligations (Articles 8–15 violations)
- Up to **€15 million** or **3% of total worldwide annual turnover**, whichever is higher
- Applicable to: Failures in risk management system, data governance, technical documentation, logging, transparency, human oversight, accuracy/robustness

### Tier 3: Provision of Incorrect Information
- Up to **€7.5 million** or **1% of total worldwide annual turnover**, whichever is higher
- Applicable to: False or misleading information provided to notified bodies or competent authorities

**Penalty calculation basis.** The "total worldwide annual turnover" basis means penalties are calculated on global group revenue — significant for large multinational banks. A global bank with €50 billion in annual revenue faces potential penalties of up to €3.5 billion for a prohibited AI violation (7% of €50bn) or up to €1.5 billion for high-risk AI violations.

**Extraterritorial enforcement.** Penalties apply to non-EU providers and deployers whose AI systems have outputs used in the EU. For US, UK, or APAC financial institutions serving EU customers, this creates real enforcement exposure even without EU legal presence.

**Concurrent enforcement.** Because financial sector regulators serve as market surveillance authorities, AI Act violations may trigger concurrent enforcement actions under both the AI Act and applicable sectoral regulation (CRR, Solvency II, MiFID II). A credit scoring AI that violates EU AI Act obligations and produces discriminatory outcomes may face simultaneous enforcement under the AI Act and GDPR, and supervisory scrutiny under CRR IRB guidelines.

---

## 12. The EU AI Office

### 12.1 Structure and Mandate

The **European AI Office** was established within the European Commission as the central institutional pillar of the EU AI Act's governance architecture. Operationally active from early 2025, the AI Office has specific responsibilities:

- **GPAI supervision and enforcement:** The AI Office has exclusive competence to supervise and enforce GPAI model providers' obligations under Title VIII (Chapter V). From August 2026, the AI Office exercises full enforcement powers including investigation authority and fine-imposition powers.
- **Cross-border coordination:** The AI Office coordinates between national market surveillance authorities to ensure consistent enforcement across member states.
- **Standardization support:** The AI Office coordinates development of harmonized EU standards for AI (through CEN-CENELEC), common specifications, and codes of practice.
- **Scientific advice:** The AI Office operates a Scientific Advisory Panel providing independent expert guidance on AI capabilities, risks, and standards.

### 12.2 Two-Tiered Governance Architecture

The AI Act establishes a two-tiered governance system:

**National level:** Each member state designates a national market surveillance authority (MSA) responsible for supervising and enforcing compliance of AI systems (other than GPAI) deployed in their territory. For financial services AI, the national financial supervisor (banking regulator, insurance regulator) typically serves as the MSA. Member states were required to designate and empower MSAs by August 2, 2025.

**EU level:** The AI Office at the Commission level supervises GPAI model providers and coordinates the overall framework. The European AI Board (EAIB), composed of representatives from national MSAs and the AI Office, facilitates coordination and harmonized enforcement.

### 12.3 Enforcement Powers

The AI Office's enforcement powers for GPAI include:

- Requesting information from GPAI model providers
- Conducting evaluations of GPAI models
- Ordering access to models for testing and assessment
- Ordering risk mitigation measures
- Withdrawing GPAI models from the EU market in extreme cases
- Imposing fines up to 3% of global turnover for GPAI obligation violations

National MSAs (including financial supervisors for financial services AI) have parallel powers for high-risk AI system enforcement: requesting information, conducting inspections, ordering corrections, withdrawing non-compliant systems, and imposing fines.

---

## 13. Practical Compliance Checklist for Financial Institutions

### Phase 1: Immediate Actions (by end of 2026)

- [ ] **Audit for prohibited AI practices.** Assess whether any deployed AI systems potentially violate Article 5 prohibitions (social scoring, exploitation of vulnerabilities, manipulative techniques). Discontinue or redesign any systems with Article 5 exposure immediately.
- [ ] **Complete AI inventory.** Identify and document every AI system deployed across all business lines. Many institutions underestimate by 30–50% through shadow AI. The inventory must cover owned models, fine-tuned foundation models, and third-party AI services.
- [ ] **Classify each AI system against the four risk tiers.** Apply the Annex III classification criteria with documented decision logic. Record the classification rationale for audit purposes.
- [ ] **Assess GPAI exposure.** Identify all deployments of foundation model APIs. Assess which use cases integrate GPAI into high-risk applications. Ensure GPAI provider compliance documentation is obtained.
- [ ] **Begin Article 9 risk management for high-risk AI.** Start the continuous risk management process for systems classified as high-risk under Annex III. Risk management documentation should be in development now, not starting in 2027.
- [ ] **Align with DORA.** Ensure AI systems are captured in ICT asset inventory, and that AI incident response integrates with DORA incident reporting procedures.
- [ ] **Review existing MRM documentation.** Assess how existing model risk management documentation satisfies Articles 9–15. Identify gaps and begin remediation.

### Phase 2: Compliance Preparation (2026–2027)

- [ ] **Complete data governance assessment.** For each high-risk AI system, document training data provenance, representativeness assessment, and bias testing (Article 10).
- [ ] **Develop technical documentation.** Produce or restructure technical documentation to meet Article 11 requirements, including compliance-mapping sections.
- [ ] **Implement automatic logging.** Ensure all high-risk AI systems generate immutable operational logs satisfying Article 12 requirements. Establish retention policies aligned with credit record retention obligations.
- [ ] **Design human oversight mechanisms.** Implement technical means for effective human oversight (Article 14): override capabilities, anomaly flags, uncertainty communication in UI. Test that oversight mechanisms are genuinely meaningful, not cosmetic.
- [ ] **Conduct accuracy and robustness testing.** Document model performance against Article 15 standards, including subgroup analysis and adversarial/stress testing.
- [ ] **Complete conformity assessments.** Conduct internal conformity assessments (Annex VI) for all standalone Annex III systems.
- [ ] **Register in EU AI database.** Register all high-risk AI systems as required before the December 2, 2027 deadline.
- [ ] **Align deployer contracts.** Ensure contracts with AI providers include provisions requiring compliance with Articles 9–15 and provision of technical documentation.
- [ ] **Coordinate GDPR and FRIA.** Align Fundamental Rights Impact Assessments with existing DPIAs for automated decision-making systems.
- [ ] **Train oversight personnel.** Ensure staff responsible for human oversight understand the systems they oversee at a level enabling meaningful override judgment (Article 14 requirement).

### Phase 3: Ongoing Compliance (Post-December 2027)

- [ ] **Continuously update risk management system** (Article 9) based on post-market monitoring data.
- [ ] **Monitor and report serious incidents** to providers and national MSAs as required.
- [ ] **Track model changes and assess whether substantial modification triggers** conformity reassessment.
- [ ] **Engage with national MSA** (banking supervisor) as they integrate AI Act supervision into SREP.
- [ ] **Monitor evolving harmonized standards** from CEN-CENELEC and Commission implementing acts and update compliance documentation accordingly.

---

## Cross-References

- [01_regulatory_landscape_overview.md](01_regulatory_landscape_overview.md) — Global regulatory landscape including EU AI Act placement within the broader MRM regulatory architecture
- [02_sr11_7_deep_dive.md](02_sr11_7_deep_dive.md) — US SR 11-7/SR 26-2 framework and comparison with EU AI Act Article 9–15 obligations
- [07_genai_governance_banking.md](07_genai_governance_banking.md) — GPAI model governance, LLM deployment in financial services, and the EU AI Act Title VIII framework for banks
- [10_industry_frameworks_nist_iso.md](10_industry_frameworks_nist_iso.md) — NIST AI RMF and ISO 42001 as frameworks that can be used to structure EU AI Act Article 9 risk management systems
- [12_explainability_fairness_bias.md](12_explainability_fairness_bias.md) — Explainability techniques (SHAP, LIME) satisfying EU AI Act Article 14 and GDPR Article 22 obligations; fairness testing for Article 10 data governance
