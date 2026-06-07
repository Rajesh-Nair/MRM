# Global Regulatory Landscape for AI/ML Model Risk Management

## File Metadata
- **Scope:** Global regulatory landscape for AI/ML model risk management across US, EU, UK, and APAC jurisdictions
- **Cluster:** A — Regulatory Foundations
- **Reading order:** 1/14
- **Related files:** [02_sr11_7_deep_dive.md](02_sr11_7_deep_dive.md), [03_eu_ai_act_finance.md](03_eu_ai_act_finance.md), [04_bank_mrm_frameworks.md](04_bank_mrm_frameworks.md)
- **Regulators/bodies covered:** Federal Reserve, OCC, FDIC, CFPB, EBA, ECB, EU Commission, FCA, PRA, MAS, FINMA, HKMA, BCBS, FSB
- **Tags:** regulation, SR-11-7, EU-AI-Act, EBA, FCA, PRA, MAS, FINMA, HKMA, BCBS, compliance, governance, timeline

---

Model risk management (MRM) has evolved from a niche discipline practiced by quant-heavy trading desks into a cross-jurisdictional regulatory imperative that reaches every corner of financial services. What began with the Federal Reserve's SR 11-7 in 2011 — itself a post-crisis response to the catastrophic model failures of 2007–2009 — has expanded into a global patchwork of binding rules, supervisory statements, principles-based frameworks, and AI-specific legislation. As of mid-2026, no major financial services jurisdiction is without some form of regulatory expectation on how models must be developed, validated, governed, and monitored. This document maps that landscape in full: the instruments, the obligations, the enforcement history, the key open questions, and the trajectory of regulation through 2028.

---

## 1. United States

### 1.1 Federal Reserve — SR 11-7 (2011) and SR 26-2 (2026)

**Regulator:** Board of Governors of the Federal Reserve System  
**Instrument:** Supervisory Letter SR 11-7, "Supervisory Guidance on Model Risk Management," April 4, 2011; superseded by SR 26-2, "Revised Guidance on Model Risk Management," April 17, 2026  
**Status:** SR 26-2 is current guidance (principles-based, non-binding supervisory guidance); SR 11-7 formally rescinded April 17, 2026  
**Effective date:** SR 11-7 was effective from April 2011; SR 26-2 effective immediately upon issuance

**Background and scope.** SR 11-7 was issued jointly with OCC Bulletin 2011-12 in the aftermath of the 2008 global financial crisis. Banking supervisors observed that major institutions had placed excessive confidence in quantitative models — particularly those underlying credit risk, market risk, and securitization — without adequately managing the risk that those models were flawed, misused, or misunderstood. SR 11-7 established, for the first time, a comprehensive supervisory expectation for how US banking organizations should identify, measure, monitor, and control model risk. The guidance applied to all Federal Reserve-supervised institutions.

**Key obligations under SR 11-7.** The guidance organized expectations around three interconnected domains: (1) model development, implementation, and use; (2) model validation; and (3) governance, policies, and controls. It required a comprehensive model inventory; independent validation proportionate to model materiality; ongoing monitoring through performance metrics, backtesting, and periodic revalidation; clear board and senior management accountability; and robust documentation. The guidance introduced the concept of **effective challenge** — critical analysis by objective, informed parties capable of identifying model limitations and driving appropriate changes.

**The 2026 revision.** On April 17, 2026, the Federal Reserve, OCC, and FDIC jointly issued SR 26-2, rescinding SR 11-7, OCC Bulletin 2011-12, and related guidance including SR 21-8 (BSA/AML model risk). SR 26-2 makes four significant shifts. First, it narrows the primary scope to banking organizations with over $30 billion in total assets, though smaller institutions with significant model complexity remain subject to examiner scrutiny under general safety-and-soundness authority. Second, it adopts a **risk-based, materiality-driven framework** where control intensity is proportionate to each model's inherent risk, exposure, and purpose — abandoning the one-size-fits-all approach of SR 11-7. Third, it explicitly excludes **generative AI and agentic AI** models from scope, noting their novel and rapidly evolving nature; the agencies plan a separate rulemaking or guidance specifically for these technologies. Fourth, SR 26-2 clarifies the model definition to exclude simple arithmetic calculations, deterministic rule-based processes, and basic spreadsheets — correcting what many banks experienced as SR 11-7's overly expansive boundary. Importantly, SR 26-2 states that "non-compliance with this guidance will not result in supervisory criticism," signaling a shift toward outcome-based supervision.

**Enforcement history.** SR 11-7 generated a substantial enforcement record over fifteen years. Model risk deficiencies routinely appeared in Matters Requiring Attention (MRAs) and Matters Requiring Immediate Attention (MRIAs) in examination reports. Common findings included incomplete model inventories (particularly "shadow" models operating outside governance frameworks), inadequate validation documentation lacking effective challenge, weak ongoing monitoring post-implementation, insufficient oversight of third-party vendor models, and validation teams lacking true independence. The 2023 Silicon Valley Bank failure analysis highlighted model risk de-prioritization within a broader risk governance breakdown.

---

### 1.2 OCC — Bulletin 2011-12 and Bulletin 2026-13

**Regulator:** Office of the Comptroller of the Currency  
**Instruments:** OCC Bulletin 2011-12 (April 2011, parallel to SR 11-7); OCC Bulletin 2021-39 (Model Risk Management Comptroller's Handbook, August 2021); OCC Bulletin 2025-26 (October 2025, community bank clarification); OCC Bulletin 2026-13 (April 2026, revised guidance)  
**Status:** Bulletin 2026-13 is current; prior bulletins rescinded

OCC Bulletin 2011-12 mirrored SR 11-7 and applied to national banks and federal savings associations. The 2021 Handbook expanded on 2011-12's principles with AI/ML-specific commentary, emphasizing explainability, bias testing, and the treatment of third-party AI vendors. In October 2025, OCC Bulletin 2025-26 provided interim clarification for community banks (institutions under $30 billion in assets), explicitly stating that annual model validation is not required for community banks and that examination findings would not be issued solely for validation frequency decisions made reasonably in light of the bank's risk profile. OCC Bulletin 2026-13 then codified the full joint revision (SR 26-2) for OCC-supervised institutions.

---

### 1.3 FDIC — Model Risk Expectations

**Regulator:** Federal Deposit Insurance Corporation  
**Instruments:** FDIC has historically applied SR 11-7 principles to state non-member banks through its examination process; FDIC joined SR 26-2 as a co-issuer in April 2026  
**Status:** FDIC is now a formal co-issuer of the joint 2026 guidance

The FDIC did not issue independent model risk guidance separate from SR 11-7, but applied its principles through the examination process for state non-member banks. FDIC examiner guidance directed examiners to assess model risk frameworks against SR 11-7 standards. As a co-issuer of SR 26-2, the FDIC formally aligned its supervisory expectations with those of the Fed and OCC.

---

### 1.4 CFPB — Algorithmic Models and Adverse Action

**Regulator:** Consumer Financial Protection Bureau  
**Instruments:** Consumer Financial Protection Circular 2022-03 (May 2022); Consumer Financial Protection Circular 2023-03 (September 2023)  
**Status:** Final (effective upon issuance); subject to policy evolution under current administration  
**Key legal framework:** Equal Credit Opportunity Act (ECOA) and Regulation B

The CFPB has focused specifically on the application of SR 11-7's principles to consumer-facing credit models, with particular emphasis on **adverse action notice requirements** under ECOA and Regulation B. CFPB Circular 2022-03 stated unequivocally that creditors using complex AI/ML models to make credit decisions must still provide specific, accurate reasons for adverse action — and that the complexity of an algorithm does not excuse a creditor from this obligation. The circular noted that if a model "makes it difficult — if not impossible — to accurately identify the specific reasons for denying credit," the creditor may not use that model. This effectively created an **explainability requirement** for consumer credit AI models in the United States.

CFPB Circular 2023-03 reinforced these requirements and provided additional guidance on the use of Sample Forms under Regulation B when AI models are involved. The CFPB encouraged industry adoption of interpretability tools such as SHAP (Shapley Additive Explanations) and LIME (Local Interpretable Model-agnostic Explanations) to generate meaningful adverse action reasons from black-box models. The circulars also emphasized fair lending testing obligations, requiring creditors to assess AI models for disparate impact and document business justifications for model features.

---

### 1.5 NCUA — Credit Union Model Risk

**Regulator:** National Credit Union Administration  
**Instruments:** NCUA joined the April 2021 interagency statement on BSA/AML model risk management (SR 21-8); no independent NCUA model risk management guidance  
**Status:** NCUA applies SR 11-7/SR 26-2 principles to federally-insured credit unions through examination

The NCUA participated in the 2021 joint statement clarifying how model risk management principles relate to BSA/AML compliance systems. The NCUA Examiner's Guide incorporates model risk concepts, and examiners assess credit union model risk frameworks against federal banking agency principles scaled to the size and complexity of individual institutions.

---

## 2. European Union

### 2.1 EBA — Guidelines on Internal Models (IRB)

**Regulator:** European Banking Authority  
**Instruments:** EBA/GL/2017/16 (Guidelines on PD estimation, LGD estimation, and treatment of defaulted exposures for IRB credit risk); EBA/GL/2023/01 (Guidelines on credit risk mitigation); ongoing validation guidelines  
**Status:** Final, in force; updated periodically  
**Effective dates:** Various, with IRB guidelines phased in from 2021

The EBA has issued extensive technical guidelines governing internal models for credit risk under the Capital Requirements Regulation (CRR). These guidelines set out detailed requirements for the development, validation, and governance of internal ratings-based (IRB) probability of default (PD) and loss given default (LGD) models. Key obligations include documented model development methodology, independent validation, back-testing against realized outcomes, ongoing performance monitoring, and clear escalation and approval processes for model changes. The guidelines also address the use of statistical techniques including machine learning, requiring that banks be able to explain and justify the models' outputs to supervisors.

---

### 2.2 ECB — Targeted Review of Internal Models (TRIM)

**Regulator:** European Central Bank Banking Supervision  
**Instruments:** TRIM Guide (published January 2019); TRIM Project Report (April 2021); ECB Guide to Internal Models (updated July 2025)  
**Status:** TRIM concluded April 2021; ongoing supervisory engagement through regular model inspections

The ECB's Targeted Review of Internal Models (TRIM) was the most ambitious supervisory exercise of its kind globally. Launched in 2016 and completed in 2021, TRIM involved 200 on-site investigations at significant institutions within the Single Supervisory Mechanism (SSM): 161 focused on credit risk models, 31 on market risk models, and 8 on counterparty credit risk models. The program aimed to assess whether Pillar I internal models complied with applicable regulatory requirements and produced reliable, comparable outputs.

TRIM's findings were sobering: the ECB identified more than **5,000 findings** across all risk types, issuing binding supervisory measures and requiring corrective action within specified deadlines. The cumulative impact was approximately a **12% increase (€275 billion)** in risk-weighted assets for investigated models. Common deficiencies included insufficient rating philosophy documentation, inadequate data quality for parameter estimation, weaknesses in internal model governance, and insufficient independent validation. The TRIM methodology has since been incorporated into the ECB's standard internal model inspection framework, which continues through the SSM's regular supervisory cycle.

---

### 2.3 EBA — Machine Learning and AI in Credit Risk

**Regulator:** European Banking Authority  
**Instruments:** EBA Discussion Paper on ML in IRB (EBA/DP/2021/04, November 2021); EBA Roadmap on Sustainable Finance and Digital Finance  
**Status:** Discussion paper; no final binding guidelines specific to ML in IRB models as of mid-2026

In November 2021, the EBA published a Discussion Paper on ML for IRB models (EBA/DP/2021/04) exploring how machine learning methods can be used within the regulatory capital framework and what additional supervisory expectations may be needed. The paper identified four key challenges for ML in credit risk: **interpretability** (the ability to explain model outputs to supervisors and customers), **stability** (ML models can change behavior rapidly), **data bias** (historical data may embed discriminatory patterns), and **extrapolation risk** (ML models trained on benign periods may perform poorly in stress). The EBA signaled that future guidelines would address these ML-specific issues but has not yet issued final binding technical standards on the topic.

---

### 2.4 EU AI Act (Regulation 2024/1689)

**Regulator:** European Commission, European Parliament, EU AI Office, national market surveillance authorities, sectoral regulators (EBA, ESMA, EIOPA)  
**Instrument:** Regulation (EU) 2024/1689 of the European Parliament and of the Council of 13 June 2024 laying down harmonised rules on artificial intelligence  
**Status:** In force August 1, 2024; phased implementation through 2028 (with Omnibus extension)  
**Key compliance deadlines:**
- February 2, 2025: Prohibited AI practices (Article 5) enforceable
- August 2, 2025: GPAI obligations (Title VIII) enforceable
- **December 2, 2027** (revised from August 2, 2026 by Digital Omnibus, May 2026): Standalone Annex III high-risk AI obligations enforceable
- August 2, 2028 (revised): High-risk AI embedded in regulated products (Annex I)

The EU AI Act is the world's first comprehensive, binding horizontal AI law. It establishes a four-tier risk classification system (unacceptable, high, limited, minimal/no risk) and imposes mandatory obligations on providers and deployers of high-risk AI systems. For detailed analysis, see [03_eu_ai_act_finance.md](03_eu_ai_act_finance.md).

**Annex III financial services applications.** Several financial services AI use cases are designated as high-risk under Annex III: (a) creditworthiness assessment and credit scoring of natural persons (Point 5(b)); (b) life and health insurance risk assessment and pricing; and (c) certain AI used for employment decisions in financial firms. The Digital Omnibus agreement of May 2026 extended standalone Annex III compliance to December 2, 2027.

**Penalties.** Violations of prohibited practices (Article 5): up to €35 million or 7% of global annual turnover, whichever is higher. Violations of high-risk AI obligations (Articles 8–15): up to €15 million or 3% of global annual turnover. Provision of false information to authorities: up to €7.5 million or 1%.

---

### 2.5 EIOPA — AI Governance for Insurers

**Regulator:** European Insurance and Occupational Pensions Authority  
**Instruments:** EIOPA Opinion on AI Governance and Risk Management (EIOPA-BoS-25-360, August 2025)  
**Status:** Final opinion, addressed to national supervisors  
**Effective date:** Applicable from issuance; national supervisors expected to integrate into their frameworks

In August 2025, EIOPA published its Opinion on AI Governance and Risk Management, providing insurance-sector-specific guidance on implementing AI oversight obligations under existing sectoral legislation (Solvency II, Insurance Distribution Directive, DORA) and the EU AI Act. The Opinion builds on EIOPA's earlier work on big data analytics and establishes expectations for data governance, record-keeping, fairness, cybersecurity, explainability, and human oversight throughout the AI lifecycle. EIOPA specifically calls out actuarial models — traditionally subject to light governance — as now requiring the same rigor as other AI systems when they incorporate machine learning components. The Opinion also addresses the interaction between the EU AI Act's high-risk classifications and Solvency II's internal model approval process, noting that insurers using ML in their internal capital models must satisfy both regulatory frameworks.

---

## 3. United Kingdom

### 3.1 PRA — SS1/23 Model Risk Management Principles for Banks

**Regulator:** Prudential Regulation Authority (Bank of England)  
**Instrument:** Supervisory Statement SS1/23, "Model Risk Management Principles for Banks" (published May 17, 2023; effective May 17, 2024); Policy Statement PS6/23  
**Status:** Final, in force  
**Effective date:** May 17, 2024

SS1/23 is the UK's first supervisory statement dedicated exclusively to model risk management. It was developed in consultation with industry following the PRA's recognition that model risk had grown substantially in scale and complexity — particularly with the proliferation of ML/AI models — and that existing guidance (largely following SR 11-7 principles) needed to be elevated to a formal supervisory statement with clearer PRA expectations.

**Initial scope.** SS1/23 initially applied to UK-incorporated banks, building societies, and PRA-designated investment firms that hold internal model approval for regulatory capital calculations under credit risk (IRB), market risk (IMA), or counterparty credit risk (IMM). However, the five principles are intended to be applied proportionately across all model types, and the PRA has signaled intent to extend the scope over time.

**The five principles.** SS1/23 organizes its expectations around five principles:

1. **Model Risk Identification and Classification** — Firms must define what constitutes a model and maintain a comprehensive, current model inventory with risk classification for all models. The PRA adopts a broad model definition similar to SR 11-7, explicitly including EUC (end-user computing) tools and offline spreadsheet calculations where they contribute to material decisions.

2. **Governance** — Clear accountability at the most appropriate Senior Management Function (SMF) holder level for the MRM framework. The Board must understand and approve the model risk appetite, and a senior individual must be designated as owning model risk at the enterprise level. MRM is positioned as a risk discipline on par with credit and market risk.

3. **Model Development and Implementation** — Robust policies and procedures for model development ensuring adequate documentation, testing, and validation processes. Standards must cover the full development lifecycle, including data sourcing, methodology selection, challenger model testing, and sign-off procedures.

4. **Independent Validation and Ongoing Monitoring** — Documented practices for continuous validation and performance assessment. Validation must provide "ongoing, independent, and effective challenge" to models throughout their lifecycle, not just at initial deployment. The PRA requires periodic revalidation based on model materiality and triggers such as significant data changes or model performance deterioration.

5. **Model Risk Mitigation and Reporting** — Clear escalation paths, remediation tracking, and reporting to the Board and senior management on model risk exposures, key limitations, and outstanding findings.

**Differences from SR 11-7.** SS1/23 differs from SR 11-7 in several important ways: it is structured as five principles rather than detailed prescriptive requirements; it explicitly calls out AI as a distinct sub-category requiring additional governance attention; it requires SMF holder accountability (a UK-specific regulatory concept under the Senior Managers Regime); and it establishes model risk as a standalone risk discipline with its own appetite statement.

---

### 3.2 FCA — AI/ML Feedback Statements

**Regulator:** Financial Conduct Authority  
**Instruments:** Discussion Paper DP22/4 / PRA DP5/22, "Artificial Intelligence and Machine Learning" (joint FCA/PRA, October 2022); Feedback Statement FS23/6 (FCA, October 2023); Feedback Statement FS2/23 (PRA, October 2023)  
**Status:** Feedback statements published; no standalone binding AI/ML rules as of mid-2026

In October 2022, the FCA and PRA jointly published a discussion paper exploring the regulatory treatment of AI and machine learning in UK financial services. The paper invited industry comment on topics including governance frameworks, explainability standards, data quality, third-party AI risk, and regulatory coherence across the UK framework (FCA consumer protection rules, PRA prudential rules, Senior Managers Regime).

The October 2023 feedback statements (FS23/6 for FCA and FS2/23 for PRA) summarized industry responses and signaled regulatory intentions. Key themes from responses included: industry concerns about regulatory fragmentation (multiple overlapping frameworks); calls for proportionate application given the diversity of AI use cases; support for outcome-based rather than prescriptive regulation; and requests for more regulatory clarity on model explainability standards for complex AI. Both regulators indicated they do not plan to create a separate standalone AI regulation (preferring to extend existing financial services regulation) but acknowledged that AI presents novel challenges requiring updated supervisory approaches. The FCA's consumer duty (effective July 2023) is the primary mechanism through which the FCA addresses AI fairness in consumer-facing applications.

---

## 4. Singapore

### 4.1 MAS — Technology Risk Management Guidelines (TRM 2021)

**Regulator:** Monetary Authority of Singapore  
**Instrument:** Technology Risk Management Guidelines (January 2021)  
**Status:** Final guidelines (non-binding but supervisory expectations)  
**Effective date:** January 2021

The MAS TRM Guidelines (2021) provide comprehensive guidance on technology risk management for financial institutions (FIs) in Singapore, including model risk management obligations. The guidelines establish expectations for AI/ML model governance, requiring FIs to maintain a technology risk management framework that covers model development, validation, performance monitoring, and change management. Specifically, the TRM guidelines require FIs to: document model assumptions and limitations; conduct pre-deployment testing; maintain version control; monitor model performance on an ongoing basis; and assess model risk as part of the institution's overall technology risk framework.

---

### 4.2 MAS — FEAT Principles (2018)

**Regulator:** Monetary Authority of Singapore  
**Instrument:** "Principles to Promote Fairness, Ethics, Accountability and Transparency (FEAT) in the Use of Artificial Intelligence and Data Analytics in Singapore's Financial Sector" (November 2018)  
**Status:** Non-binding principles

Published in November 2018, the FEAT Principles were the first AI governance principles issued by a central bank or financial regulator globally. They established four foundational pillars for AI governance in Singapore's financial sector:

- **Fairness:** Outcomes across individuals or groups should avoid systematic disadvantage unless justified and documented. FIs must test AI systems for bias and discriminatory effects.
- **Ethics:** AI use must align with the firm's values and societal norms. Models must not be used in ways that exploit or manipulate customers.
- **Accountability:** Explicit governance structures with defined roles and responsibilities for AI projects, including model owners, independent validators, and board oversight.
- **Transparency:** Meaningful disclosure and explainability; documentation sufficient for supervisors and, where appropriate, customers to understand material AI-driven decisions.

FEAT was developed in consultation with the Personal Data Protection Commission and IMDA, and is aligned with OECD AI principles. It has served as the conceptual foundation for subsequent MAS AI governance instruments.

---

### 4.3 MAS — AI Model Risk Management Information Paper (December 2024)

**Regulator:** Monetary Authority of Singapore  
**Instrument:** MAS Information Paper, "Artificial Intelligence Model Risk Management" (December 2024)  
**Status:** Non-binding information paper (good practices from thematic review)

In December 2024, the MAS published an information paper following a thematic review of selected banks' AI model risk management practices conducted in mid-2024. The paper identified good practices across three domains: (1) governance and oversight, including cross-functional AI oversight forums and responsible AI principles embedded in bank policies; (2) risk management systems and processes, including formal AI inventories with lifecycle tracking; and (3) development and deployment, including pre-deployment testing and ongoing post-deployment monitoring. The paper is explicitly applicable to all financial institutions, not only banks.

---

### 4.4 MAS — AI Risk Management Guidelines (2025 Consultation)

**Regulator:** Monetary Authority of Singapore  
**Instrument:** Consultation Paper, "Guidelines on Artificial Intelligence Risk Management for Financial Institutions" (November 2025)  
**Status:** Consultation; final guidelines expected 2026

In November 2025, MAS published a consultation paper proposing binding Guidelines on AI Risk Management for FIs. The proposed guidelines would require FIs to: maintain an AI use case inventory with Risk Materiality Assessments; implement lifecycle controls covering data management, fairness testing, transparency, explainability, human oversight, third-party risk, and change management; and assign board and senior management accountability for AI risk governance. The guidelines build on FEAT, TRM 2021, and the December 2024 Information Paper, and represent MAS's shift from principles-based to more formal supervisory expectations for AI.

---

## 5. Switzerland

### 5.1 FINMA — Circular 2023/1 on Operational Risks and Resilience

**Regulator:** Swiss Financial Market Supervisory Authority (FINMA)  
**Instrument:** FINMA Circular 2023/1, "Operational Risks and Resilience — Banks" (published December 13, 2022; effective January 1, 2024; transitional provisions to 2026)  
**Status:** Final, in force  
**Effective date:** January 1, 2024 for operational risk provisions; January 1, 2026 for resilience provisions

FINMA Circular 2023/1 is a comprehensive revision of FINMA's operational risk framework for Swiss banks, incorporating the Basel Committee's 2021 Principles for the Sound Management of Operational Risk. While the circular does not address model risk as a standalone category, it creates significant obligations relevant to model risk through its treatment of critical data, ICT governance, and operational resilience. Swiss banks must identify, classify, and protect "critical data" — a category that explicitly includes model inputs and outputs used in material business decisions. The circular establishes a 24-hour notification requirement to FINMA for significant cyber incidents and requires financial institutions to demonstrate that their operations remain resilient in the face of ICT disruptions, including disruptions to model infrastructure.

FINMA has been clear through supervisory communications that model risk falls within the scope of operational risk under the circular, and that AI/ML models used in credit decisions, pricing, and risk management must satisfy the circular's governance and resilience requirements.

---

## 6. Hong Kong

### 6.1 HKMA — Supervisory Policy Manual and AI Governance

**Regulator:** Hong Kong Monetary Authority  
**Instruments:** Supervisory Policy Manual (SPM) CA-G-3, "Use of Internal Models Approach to Calculate Market Risk Capital Charge" (2010, updated); SPM CA-G-4, "Validating Risk Rating Systems" (2006, updated 2025); Circular on AI Principles (2019); Circular on AI in AML/CFT (September 2024); Circular on GenAI in customer-facing activities (August 2024)  
**Status:** Various (some legally binding under Banking Ordinance, some circular guidance)

The HKMA's model risk governance framework is built through its Supervisory Policy Manual, which includes specific modules on internal model validation. SPM CA-G-4 establishes detailed expectations for validating credit risk rating systems, including requirements for independent validation, back-testing, and documentation. The HKMA has been an active regulator on AI governance: its 2019 circular established 12 high-level principles for AI deployment by authorized institutions, covering governance, transparency, explainability, fairness, and consumer protection. These principles are proportionate, allowing institutions to calibrate governance to their AI footprint.

In 2024, HKMA issued two notable AI-specific circulars. The August 2024 circular on generative AI in customer-facing activities provided clear expectations for transparency (disclosure to customers of AI involvement), explainability, fairness testing, and human oversight for GenAI-powered customer service functions. The September 2024 circular actively encouraged authorized institutions to use AI for AML/CFT monitoring, noting AI's advantages over rules-based systems while requiring robust model governance. The HKMA's GenA.I. Sandbox initiative provides a regulatory testing environment for financial institutions to pilot AI innovations with HKMA supervisory involvement.

---

## 7. Australia

### 7.1 APRA — CPS 220 and CPG 220 Risk Management

**Regulator:** Australian Prudential Regulation Authority  
**Instruments:** Prudential Standard CPS 220, "Risk Management" (effective January 1, 2015; updated); Prudential Practice Guide CPG 220, "Risk Management" (April 2018)  
**Status:** CPS 220 is binding; CPG 220 is non-binding guidance

APRA's CPS 220 requires APRA-regulated institutions to maintain an effective risk management framework (RMF) covering all material risks, including model risk. While APRA does not have a standalone model risk management prudential standard, CPS 220 creates model risk obligations through its requirements for: board-approved risk appetite statements (which must address model risk for institutions with material model use); a Chief Risk Officer with authority over all risk types; the three lines of defense model; and independent risk function oversight.

CPG 220 elaborates on best practices and explicitly references model risk as a risk category requiring management within the RMF. APRA supervisors assess model risk practices during prudential reviews and have issued findings to institutions with inadequate model governance. APRA is watching the EU AI Act and MAS developments closely and has signaled through thematic reviews that enhanced AI governance expectations are forthcoming, though no formal consultation paper on AI/ML model risk had been issued as of mid-2026.

---

## 8. Global and Multilateral Bodies

### 8.1 Basel Committee on Banking Supervision (BCBS)

**Body:** Basel Committee on Banking Supervision  
**Relevant instruments:**
- BCBS "Principles for the Sound Management of Operational Risk" (BCBS 195, June 2011; revised BCBS d515, March 2021): Model risk is addressed under Principle 5 (internal loss data), Principle 6 (external data), and Principle 8 (change management). The 2021 revision updated the principles to reflect lessons from the 2014 BCBS review that found inadequate implementation.
- BCBS "Principles for the effective management and supervision of climate-related financial risks" (BCBS d532, June 2022): Establishes expectations for scenario analysis and stress testing models used in climate risk assessment, including requirements for model validation and governance proportionate to the use of outputs in capital planning and risk management decisions.
- BCBS update to "Principles for the management of credit risk" (BCBS d595, 2023): Revised to address ML/AI in credit risk assessment, requiring banks to ensure that AI-driven credit decisions are explainable, auditable, and subject to the same governance standards as traditional credit models.

**Status:** BCBS principles are adopted by national regulators into domestic frameworks; not directly binding on institutions

The BCBS has been deliberate in addressing model risk under the operational risk framework rather than creating a standalone model risk pillar. The Basel III operational risk capital charge framework (Standardized Approach, effective January 2023) does not include an explicit model risk component, meaning model risk capital is embedded within operational risk capital and the quality of model governance is addressed through supervisory review (Pillar 2) rather than minimum capital (Pillar 1).

---

### 8.2 Financial Stability Board (FSB)

**Body:** Financial Stability Board  
**Relevant instruments:**
- FSB "Artificial Intelligence and Machine Learning in Financial Services" (November 2017): Identified model risk, opacity, and data bias as key financial stability concerns from AI/ML adoption.
- FSB "The Financial Stability Implications of Artificial Intelligence" (November 2024): Updated the 2017 analysis with findings from a decade of AI adoption, identifying new systemic risks from model herding (many institutions using similar AI models), third-party concentration (dependence on a few AI vendors), and AI-driven market dynamics.

**Status:** FSB reports are not binding; they inform policy decisions by member national authorities

The FSB's November 2024 report on AI financial stability implications is significant for model risk management because it identified **model correlation risk** as a new systemic concern: if many financial institutions use similar AI models (particularly from common third-party providers such as large technology companies), correlated model failures could amplify financial stress. This concern is shaping regulatory discussions around AI model diversity, third-party concentration risk, and the adequacy of current model risk frameworks for systemic risk management.

---

## 9. Chronological Timeline of Major MRM Regulatory Events (2011–2026)

| Year | Event |
|------|-------|
| April 2011 | US Federal Reserve SR 11-7 and OCC Bulletin 2011-12 issued — establishes foundational MRM framework for US banks |
| November 2012 | Basel Committee BCBS 239 "Principles for Effective Risk Data Aggregation" — creates data quality backbone for model inputs |
| 2016 | ECB launches Targeted Review of Internal Models (TRIM) — first systematic pan-European review of Pillar I internal model compliance |
| January 2019 | ECB publishes TRIM Guide — comprehensive methodology for internal model assessment |
| November 2018 | MAS publishes FEAT Principles — world's first AI governance principles from a central bank |
| 2019 | HKMA issues AI Principles circular for authorized institutions |
| March 2021 | BCBS revises Principles for Sound Management of Operational Risk (d515) |
| April 2021 | ECB TRIM project concludes — 5,000+ findings, €275bn RWA impact |
| April 2021 | US agencies (Fed, OCC, FDIC, NCUA) joint statement on BSA/AML model risk (SR 21-8) |
| August 2021 | OCC publishes updated Model Risk Management Comptroller's Handbook (Bulletin 2021-39) |
| November 2021 | EBA Discussion Paper on ML in IRB credit risk (EBA/DP/2021/04) |
| May 2022 | CFPB Circular 2022-03 — adverse action notice requirements for AI/ML credit models |
| June 2022 | BCBS publishes climate risk principles (d532) including model governance for scenario analysis |
| October 2022 | FCA/PRA joint Discussion Paper DP22/4/DP5/22 on AI and ML in UK financial services |
| May 2023 | PRA publishes SS1/23 "Model Risk Management Principles for Banks" (UK) |
| June 2023 | EU AI Act political agreement reached between European Parliament and Council |
| September 2023 | CFPB Circular 2023-03 — reinforces adverse action notice requirements for AI |
| October 2023 | FCA FS23/6 and PRA FS2/23 feedback statements on AI/ML Discussion Paper |
| August 2024 | EU AI Act (Regulation 2024/1689) enters into force |
| August 2024 | HKMA circular on GenAI in customer-facing banking |
| September 2024 | HKMA circular encouraging AI in AML/CFT monitoring |
| May 2024 | PRA SS1/23 becomes effective for in-scope UK banks |
| December 2024 | MAS publishes AI Model Risk Management Information Paper (thematic review findings) |
| February 2025 | EU AI Act prohibited practices (Article 5) enforceable |
| July 2025 | ECB publishes updated Guide to Internal Models |
| August 2025 | EU AI Act GPAI obligations (Title VIII) enforceable |
| August 2025 | EIOPA Opinion on AI Governance and Risk Management |
| October 2025 | OCC Bulletin 2025-26 — community bank model risk clarification |
| November 2025 | EU Commission Digital Omnibus on AI proposed — high-risk deadline extension to December 2027 |
| November 2025 | MAS consultation on AI Risk Management Guidelines |
| April 2026 | US Federal Reserve SR 26-2, OCC Bulletin 2026-13 — joint revised guidance replaces SR 11-7 |
| May 2026 | EU AI Act Digital Omnibus provisional agreement — Annex III high-risk deadline moved to December 2, 2027 |
| December 2027 | EU AI Act high-risk AI obligations for standalone Annex III systems (revised deadline) |
| August 2028 | EU AI Act high-risk AI obligations for AI embedded in regulated products (Annex I) |

---

## 10. Comparison: Binding Rules vs. Guidance vs. Principles

| Jurisdiction | Instrument | Nature | Binding? | Scope |
|---|---|---|---|---|
| US — Federal Reserve | SR 26-2 (2026) | Supervisory guidance | Non-binding (but examinable) | Banks >$30bn assets |
| US — OCC | OCC Bulletin 2026-13 | Supervisory guidance | Non-binding (examinable) | National banks |
| US — CFPB | Circulars 2022-03 / 2023-03 | Supervisory circular | Non-binding but enforceable via ECOA | Consumer credit lenders |
| EU | EU AI Act | Regulation | Binding law | All deployers/providers in EU |
| EU — EBA | IRB Guidelines | Binding technical guidelines | Binding on EU institutions | IRB credit risk models |
| UK — PRA | SS1/23 | Supervisory statement | Binding on in-scope firms | Banks with internal model approval |
| UK — FCA | FS23/6 | Feedback statement | Non-binding (principles) | All FCA-regulated firms |
| Singapore — MAS | TRM 2021 | Guidelines | Non-binding (supervisory expectations) | All MAS-regulated FIs |
| Singapore — MAS | FEAT Principles | Principles | Non-binding | All MAS-regulated FIs |
| Switzerland — FINMA | Circular 2023/1 | Circular (binding) | Binding | Swiss banks |
| Hong Kong — HKMA | SPM modules | Statutory guideline / circular | Partially binding (CA-G-4) | Authorized institutions |
| Australia — APRA | CPS 220 | Prudential standard | Binding | APRA-regulated entities |
| Global — BCBS | Operational risk principles | International principles | Non-binding (adopted domestically) | Globally significant banks |

---

## 11. Key Open Regulatory Questions and Upcoming Consultations

**Generative AI and agentic AI governance.** The most pressing open question globally is how to govern generative AI (LLMs) and agentic AI systems that act autonomously. SR 26-2 explicitly excluded GenAI from scope pending separate rulemaking; the EU AI Act's GPAI framework addresses systemic risk models but not the use of LLMs as decision-support tools within financial firms; and no jurisdiction has yet issued comprehensive binding guidance on agentic AI in financial services. The US agencies have signaled a request for information on AI usage to inform future guidance.

**Model definition boundaries.** SR 26-2 narrowed the model definition, but the boundary between a model and a non-model tool remains contested — particularly for AI systems that combine rule-based logic with statistical components. The EU AI Act definition of "AI system" (covering machine-based systems that generate outputs such as predictions, recommendations, or decisions influencing environments) is broader than the SR 26-2 model definition, creating a potential gap where systems regulated under the AI Act are not subject to formal MRM governance.

**Third-party and vendor AI concentration risk.** As financial institutions increasingly rely on a small number of AI platform providers (Google, Microsoft, Amazon, Anthropic, OpenAI), regulators are concerned about systemic model concentration. The FSB's 2024 report highlighted this explicitly. Expect guidance from multiple jurisdictions on managing third-party AI concentration risk, likely building on existing third-party risk management frameworks (DORA in the EU, SR 13-19 in the US).

**Climate risk model validation standards.** Climate risk models — scenarios, transition risk models, physical risk models — are increasingly used in capital planning and risk management. No jurisdiction has yet issued detailed model validation standards specific to climate models, though the ECB and BCBS have established principles. Model validators lack standardized benchmarks for assessing climate model quality.

**Cross-border regulatory coherence.** Financial institutions operating globally face an increasingly complex patchwork of national MRM frameworks. The EU AI Act's extraterritorial scope (applying to any AI system with output used in the EU) combined with US, UK, and APAC domestic frameworks creates overlapping compliance obligations. Industry bodies (EBF, IIF, AFME) have called for greater supervisory coordination. The FSB and BCBS are monitoring international coherence but have not initiated a formal harmonization exercise.

**Small and mid-size institution applicability.** The shift in SR 26-2 to focus on $30bn+ institutions has created clarity for community banks in the US but uncertainty for mid-size institutions ($10–30bn in assets). Similarly, PRA SS1/23's initial scope is limited to internal model banks, leaving open the question of when and how the principles extend to all UK banks. Expect both jurisdictions to provide further clarity on proportionate application.

---

## Cross-References

- [02_sr11_7_deep_dive.md](02_sr11_7_deep_dive.md) — Comprehensive deep-dive into SR 11-7 / OCC 2011-12, the foundational US MRM framework, and its 2026 replacement SR 26-2
- [03_eu_ai_act_finance.md](03_eu_ai_act_finance.md) — Full analysis of EU AI Act obligations for financial services, Annex III high-risk classification, GPAI, conformity assessment, and DORA/GDPR interactions
- [04_bank_mrm_frameworks.md](04_bank_mrm_frameworks.md) — Industry MRM implementation frameworks at major banks
- [06_model_inventory_and_governance_ops.md](06_model_inventory_and_governance_ops.md) — Operational details of model inventory management and governance committee structures
- [07_genai_governance_banking.md](07_genai_governance_banking.md) — GenAI and agentic AI governance in financial services
- [10_industry_frameworks_nist_iso.md](10_industry_frameworks_nist_iso.md) — NIST AI RMF, ISO 42001, and other voluntary AI governance frameworks
- [12_explainability_fairness_bias.md](12_explainability_fairness_bias.md) — Explainability requirements, fairness testing, and bias mitigation in financial AI models
