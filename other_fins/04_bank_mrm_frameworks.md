# Bank MRM Frameworks: How the World's Largest Banks Govern Model Risk

## File Metadata
- **Scope:** MRM governance structures, three-lines-of-defense, model lifecycle, and Model Risk Committee frameworks at major global banks
- **Cluster:** B — Bank Practice: Traditional ML MRM
- **Reading order:** 4/14
- **Related files:** [02_sr11_7_deep_dive.md](02_sr11_7_deep_dive.md), [05_model_validation_methodology.md](05_model_validation_methodology.md), [06_model_inventory_and_governance_ops.md](06_model_inventory_and_governance_ops.md), [07_genai_governance_banking.md](07_genai_governance_banking.md)
- **Regulators/bodies covered:** Federal Reserve, OCC, PRA, ECB/SSM, FINMA
- **Tags:** three-lines-of-defense, model-lifecycle, model-validation-unit, model-risk-committee, JPMorgan, Goldman-Sachs, Wells-Fargo, Deutsche-Bank, HSBC, Barclays, consent-order, bank-governance

---

## 1. Introduction: Why Bank MRM Frameworks Matter

Model Risk Management (MRM) at the world's largest financial institutions has evolved from a narrow technical discipline focused on derivatives pricing into a comprehensive enterprise risk function spanning thousands of models across every line of business. The financial crisis of 2008, followed by a decade of regulatory enforcement actions, transformed what had been an informal practice into a heavily structured governance apparatus with board-level visibility, independent validation units staffed by PhD-level quantitative experts, and multi-year remediation programmes costing hundreds of millions of dollars.

The scale at which global systemically important banks (G-SIBs) operate their model inventories is difficult to overstate. Large banks are known to maintain inventories of 3,000 to 10,000 or more models, spanning credit risk, market risk, operational risk, liquidity, fraud detection, anti-money laundering, IFRS 9 expected credit loss, CCAR stress testing, customer pricing, and increasingly generative AI applications. Each of these models carries the potential for significant financial loss, regulatory capital miscalculation, customer harm, or reputational damage if it performs incorrectly or is used outside its intended scope.

This document examines how eleven of the world's largest banks structure their MRM programmes, the governance frameworks they operate, the regulatory environments they navigate, and the common patterns — and notable failures — that define the state of bank model governance in the mid-2020s.

---

## 2. The Three Lines of Defense Applied to Model Risk

The **Three Lines of Defense** (3LoD) framework, as originally articulated by the Institute of Internal Auditors and embedded in regulatory expectations by SR 11-7 (Federal Reserve, 2011), OCC Bulletin 2011-12, and the UK PRA's Supervisory Statement SS1/23 (May 2024), provides the foundational governance architecture for model risk at banks.

### 2.1 First Line of Defense: Model Owners, Developers, and Business Units

The first line of defense comprises every person and function that develops, implements, maintains, or uses a model in the ordinary course of business. This includes:

- **Front-office quantitative analysts** who build pricing and risk models for trading desks
- **Risk analytics teams** embedded in credit, market risk, and operational risk functions who develop scorecards, IRB models, and stress-testing frameworks
- **Business unit model users** who apply model outputs to business decisions (lending decisions, limit-setting, product pricing)
- **Model owners**, typically a senior business professional accountable for the model's performance, documentation, and lifecycle management within the first line
- **Data science and machine learning teams** embedded in technology or innovation divisions who build AI/ML models for fraud detection, customer segmentation, AML transaction monitoring, or digital product recommendations
- **MLOps and model deployment teams** responsible for production infrastructure

The first line's core obligations under regulatory frameworks include: registering all models in the enterprise inventory, producing comprehensive model documentation (methodology documentation, data documentation, implementation documentation), performing initial development testing and user acceptance testing, maintaining models in production within approved use boundaries, monitoring model performance on an ongoing basis, and escalating performance degradation or material changes to the second line.

The key tension at the first line is one of incentives. Model developers are evaluated on the performance and usefulness of their models; they may have unconscious bias toward validating their own assumptions. This is precisely why regulatory frameworks insist on independent validation at the second line.

**Emerging 1.5-Line Debate:** One of the most contentious governance debates in MRM concerns the concept of a "1.5 line" — a validation function that sits between business development teams and the fully independent second-line validation unit. This structure arises in several contexts:

- Large banks with dedicated **quantitative research groups** (e.g., Goldman Sachs's "Strats" teams) who review model methodology as part of development but are not fully independent validators
- **Model development centres of excellence** that perform peer review within the first line
- **Technology risk teams** with deep technical expertise who conduct implementation reviews but report within the business rather than to the CRO

Regulators generally look unfavourably on using 1.5-line reviews as a substitute for independent validation. SR 11-7 is explicit that "validation should be conducted by staff who are not responsible for model development or use and who do not have a stake in whether a model is found to be valid." However, 1.5-line review is increasingly accepted as a complement — a way of increasing the quality of models entering the formal validation queue, reducing the backlog pressure on second-line MVUs, and enabling faster time-to-market for lower-materiality models.

### 2.2 Second Line of Defense: The Model Validation Unit (MVU)

The second line — variously called the **Model Validation Unit (MVU)**, **Model Risk Management (MRM) group**, **Independent Model Review**, or **Quantitative Risk Management** — is the heart of bank MRM governance. Its independence from the first line is non-negotiable under both U.S. and international regulatory frameworks.

Structurally, the MVU typically:
- Reports to the **Chief Risk Officer (CRO)** or a **Chief Model Risk Officer (CMRO)**, separate from business line management
- Is staffed by quantitative specialists with advanced degrees (PhDs in mathematics, statistics, financial engineering, physics, economics) and increasing numbers of data scientists and machine learning engineers as AI/ML models proliferate
- Maintains a **Model Risk Policy** and **Validation Standards** that define what validation is required, at what tier level, with what frequency, and to what documentation standard
- Issues **validation opinions** (approved, approved with conditions, use-with-exceptions, or not approved) on models submitted for initial or periodic review
- Tracks **model findings** and **limitations** in a central register
- Reports to senior management and the Board on aggregate model risk exposures

The second line's role goes beyond one-time validation. Under SR 11-7 and SS1/23, ongoing monitoring is also a second-line responsibility — including periodic outcome analysis, benchmarking, and escalation when model performance deteriorates materially.

**Chief Model Risk Officer (CMRO):** Several of the largest banks have created a dedicated CMRO role, separate from the CRO, to provide single-point accountability for the enterprise model risk function. This role typically oversees the MVU, chairs or serves on the Model Risk Committee, produces the firmwide model risk report for the Board, and manages relationships with model risk regulators.

### 2.3 Third Line of Defense: Internal Audit

Internal Audit provides independent assurance that the first and second lines are operating their respective controls effectively. In the context of model risk, Internal Audit typically:

- Reviews whether the Model Risk Policy is complete, up-to-date, and appropriately approved
- Samples completed validation reports to assess their quality, independence, and completeness
- Audits whether the model inventory is complete (testing for undiscovered or "shadow" models)
- Reviews the Model Risk Committee's functioning and governance records
- Assesses whether model monitoring and escalation processes function as designed
- Evaluates the adequacy of model risk reporting to senior management and the Board

Internal Audit does not validate models itself — that would create a second-line function within the third line. Rather, it assesses the design and operating effectiveness of the MVU's processes. Audit findings that identify systemic weaknesses in the MRM programme are among the most serious escalation signals available to senior leadership.

---

## 3. Standard Model Lifecycle Stages

Regulatory guidance — particularly SR 11-7 and its international equivalents — requires that banks manage models across a **full lifecycle**, from initial conception through retirement. Each stage has defined governance requirements.

### 3.1 Model Registration and Discovery

Every model in use at a bank must be registered in the **enterprise model inventory** before it is used for any business purpose. Registration typically involves:

- Assignment of a unique model identifier
- Completion of a model registration form (model name, purpose, business owner, model type, intended use, data inputs, outputs)
- Preliminary risk tiering based on stated purpose and expected financial materiality
- Assignment of a second-line model risk manager counterpart

**Discovery** is the proactive process of finding models that are already in use but have not been registered — including spreadsheet models, Python scripts, third-party vendor tools, and AI/ML models developed without formal governance involvement. Discovery is a perpetual challenge at large banks and is discussed further in the section on shadow model proliferation.

### 3.2 Model Development and Documentation

Once registered, the model enters formal development with required documentation standards:

- **Conceptual design document** (or development notebook): describes the theoretical basis, the modelling approach considered, the data sources used, key assumptions, limitations, and scope restrictions
- **Technical implementation documentation**: describes the code, implementation logic, testing results, and version control records
- **User guide**: describes how model users should correctly apply the model, including the boundaries of appropriate use
- **Data lineage documentation**: describes the origin, processing, and quality-control of all input data

Documentation quality is one of the most frequently cited deficiencies in regulatory examinations and internal audit findings. Even technically sound models fail validation when documentation does not adequately support independent review.

### 3.3 Pre-Implementation Validation and Approval

Before a model is deployed into production, it must receive a **pre-implementation validation opinion** from the second line. This is typically the most resource-intensive validation event in a model's lifecycle, involving the full validation workplan described in File 5.

The validation process culminates in a **validation report** that includes:
- A rating of overall model risk (commonly: Low / Medium / High / Very High, or a numerical score)
- A findings register documenting every identified limitation or deficiency
- A validation opinion: Approved / Approved with Conditions / Use-with-Exceptions / Not Approved

**Approval authority** varies by model tier (described further in Section 4).

### 3.4 Production Deployment and Ongoing Monitoring

Once approved, models enter production. The first line's monitoring obligations include:

- **Performance monitoring**: tracking model outputs and key performance metrics against expected ranges
- **Data quality monitoring**: ensuring input data continues to meet the quality standards assumed during development
- **Population stability monitoring**: detecting shifts in the input population using PSI and CSI metrics
- **Outcome analysis**: comparing model predictions against actual outcomes as they become available

The second line maintains independent monitoring oversight, reviewing first-line monitoring reports, conducting periodic outcome analysis, and escalating concerns.

### 3.5 Periodic Revalidation and Event-Triggered Revalidation

Models require **periodic revalidation** at a frequency commensurate with their risk tier. Typical frequencies:
- **Critical/High tier**: annual revalidation
- **Medium tier**: every 2–3 years
- **Low tier**: every 3–5 years, or lighter-touch monitoring review

**Event-triggered revalidation** is required when:
- A material model change occurs (new version, new variables, recalibration, methodology change)
- The regulatory capital or business use of the model changes materially
- Monitoring indicates performance deterioration beyond defined thresholds
- A change in market conditions, economic regime, or population shift is identified that may affect model assumptions
- A regulatory examination or internal audit identifies a model limitation that requires reassessment

### 3.6 Model Retirement and Decommissioning

When a model is no longer in use — replaced by a successor model, discontinued alongside a business activity, or decommissioned due to persistent performance issues — it must be formally retired through a **decommissioning process**:

- Updated status in the model inventory (Retired)
- Documentation of the retirement rationale and effective date
- Archiving of all model artefacts (code, documentation, validation reports) for the regulatory retention period (typically 7 years in the U.S. under federal record-keeping requirements)
- Assessment of **transition risk** if the model was used in regulatory capital calculations or customer-facing decisions that may require explanation post-retirement

Model retirement is often neglected in resource-constrained MRM programmes. Banks have been found by regulators to maintain models in "zombie" status — technically registered as active but no longer used, or used by business units who lost contact with the model owner after organisational changes. This creates phantom risk in the inventory and distorts model risk metrics.

### 3.7 Use-with-Exception and Emergency Override

When a model is required immediately for a business purpose but has not yet completed full validation, or when a validation has raised findings that prevent full approval but business need is urgent, banks maintain a **use-with-exception (UWE)** or **emergency override** process:

- Formal documentation of the exception, including the business justification
- Identification of compensating controls (manual review of outputs, conservative adjustments, enhanced monitoring)
- Time-limited approval (typically 90 days, renewable once)
- Escalation to appropriate approval authority (typically higher than normal for the tier)
- Mandatory tracking in the model findings register

Regulatory guidance expects UWE to be the exception, not the norm. A pattern of persistent use-with-exceptions for the same model is a governance failure signal.

---

## 4. Model Approval Tiering

### 4.1 The Tiering Framework

One of the most consequential structural decisions in any bank's MRM programme is the **model tiering framework** — the system by which models are assigned to risk categories that then drive the intensity of validation, monitoring, approval authority, and oversight.

Tiering frameworks typically use a multi-criteria scoring approach. The most common criteria are:

| Criterion | What It Captures |
|---|---|
| **Financial Materiality** | The potential P&L impact or capital impact if the model fails or is materially wrong |
| **Regulatory Capital Use** | Whether the model is used in the computation of regulatory capital (IRB, FRTB, SA-CCR, etc.) |
| **Customer-Facing Impact** | Whether model outputs directly affect customers (credit decisions, pricing, product eligibility) |
| **Systemic Risk Contribution** | Whether model failure could cascade across the institution |
| **Data Sensitivity** | Whether the model processes sensitive personal data |
| **Operational Dependency** | Whether operations would be severely disrupted if the model became unavailable |
| **Model Complexity** | The technical complexity of the model (linear regression vs. deep neural network) |
| **Novelty** | Whether the model uses new techniques or data sources without historical validation precedent |
| **Regulatory Scrutiny** | Whether the model is subject to regulatory review (DFAST, CCAR, ECB TRIM) |

A typical four-tier framework:

| Tier | Label | Description |
|---|---|---|
| **Tier 1 / Critical** | Critical | Regulatory capital models; CCAR/DFAST stress models; models with financial impact >$500M; flagship credit models |
| **Tier 2 / High** | High | Material credit risk models; customer-facing models with significant population; key fraud and AML models |
| **Tier 3 / Medium** | Medium | Significant pricing or risk models used in specific business lines; models with moderate financial impact |
| **Tier 4 / Low** | Low | Analytical tools; decision-support models; low-impact scoring models; internal management reporting models |

### 4.2 Approval Authority by Tier

Approval authority escalates with model tier:

| Tier | Typical Approval Authority |
|---|---|
| Critical | Model Risk Committee + Board Risk Committee ratification |
| High | Model Risk Committee or CMRO |
| Medium | Head of Model Risk Management / Senior validation leader |
| Low | Validation team lead / designated reviewer |

Banks may also require escalation to the Board Risk Committee for any model that receives a "Not Approved" opinion at any tier, or for any model where a use-with-exception is requested for a Tier 1/Critical model.

### 4.3 Annual Tiering Review

Model tiers are not static. Banks are expected to conduct an **annual tiering review** to reassess whether models are in the appropriate tier given:
- Changes in business use or financial exposure
- Changes in regulatory requirements
- Changes in model complexity (e.g., a model that has been significantly enhanced with ML components)
- New information from monitoring results

---

## 5. Model Risk Committees: Structure and Operation

### 5.1 The Management-Level Model Risk Committee

The **Model Risk Committee (MRC)** is the primary governance body for model risk at the management level. It sits between the model-level approval decisions made by the MVU and the Board-level risk committee.

Typical Model Risk Committee charter elements:

**Purpose:** Provide senior management oversight of the enterprise model risk profile; approve high-tier models; set and monitor model risk appetite; escalate material model risk issues to the Board Risk Committee.

**Typical Membership:**
- Chief Risk Officer (Chair or Co-Chair)
- Chief Financial Officer or representative
- Chief Technology Officer or Chief Data Officer
- Chief Model Risk Officer / Head of Model Validation (Secretary)
- Heads of key business lines (Retail Banking, Corporate/Institutional Banking, Capital Markets, Treasury)
- Chief Compliance Officer (standing invitee)
- Head of Internal Audit (standing observer, non-voting)

**Meeting Cadence:** Monthly for standing business; quarterly for full model risk appetite review; ad hoc for material escalations.

**Standard Agenda Items:**
1. Review and approval of high/critical tier model validation reports
2. Model risk appetite dashboard and KRI review
3. Open findings and overdue remediation status
4. Use-with-exception approvals
5. Regulatory and supervisory updates affecting model governance
6. Material model changes requiring MRC-level review
7. New model pipeline and upcoming validations

**Quorum and Voting:** Typically requires CRO (or designee) plus a majority of other standing members; voting for model approval typically requires majority of members present.

### 5.2 Sub-Committee Structure

Large banks frequently operate sub-committees beneath the firmwide MRC:

- **Regulatory Capital Model Sub-Committee**: specialized oversight of IRB, FRTB, SA-CCR, and IFRS 9 models, reflecting their elevated regulatory sensitivity
- **AI/GenAI Governance Forum**: dedicated oversight for generative AI and advanced ML models, often with CTO/CDO involvement
- **Stress Testing Model Oversight Committee**: specific to CCAR/DFAST models with the CFO function heavily involved
- **Fraud and AML Model Committee**: operationally focused oversight for real-time detection models

### 5.3 Board-Level Reporting

The Board Risk Committee (or equivalent — some banks use an Audit and Risk Committee) receives regular model risk reporting, typically:

- **Quarterly**: Model risk dashboard showing tier distribution, validation backlog, open critical findings, use-with-exceptions outstanding
- **Annually**: Firmwide model risk report summarizing the year's validation activity, aggregate model risk, regulatory examination outcomes, and outlook for the coming year
- **Ad hoc**: Escalation of material model failures, regulatory enforcement actions related to model risk, or model risk appetite breaches

---

## 6. Bank-by-Bank Profiles

### 6.1 JPMorgan Chase

**Overview:** JPMorgan Chase is among the world's most sophisticated practitioners of model risk management, operating one of the largest model inventories in banking. The firm's 2024 10-K filing references "Estimations and Model Risk" as a standalone risk category within its Enterprise Risk Management framework, reflecting the institutional priority placed on model governance.

**Scale:** JPMorgan has deployed AI tools to more than 200,000 employees and operates an AI use-case inventory exceeding 500 live applications. The firm's formal model inventory is believed to be among the largest in the industry, though it does not publicly disclose a specific count.

**Governance Structure:**
JPMorgan operates its MRM function through a **Firmwide Model Risk (FMR)** group, which sits within the Risk Management organization reporting to the Chief Risk Officer. The FMR group is responsible for:
- Maintaining and enforcing the Firmwide Model Risk Policy
- Operating the independent Model Validation Unit
- Producing the Firmwide Model Risk Report for senior leadership and the Board
- Overseeing the model inventory and tiering framework

In 2024, JPMorgan introduced a formal **AI Model Risk Management Framework** that aligns internal standards with both the EU AI Act and the NIST AI Risk Management Framework. This framework requires that all AI systems deployed at the firm be explainable, auditable, and traceable — requirements that go beyond the minimum demands of SR 11-7 but reflect the firm's awareness of the rapidly evolving regulatory landscape for AI in financial services.

**AI Governance:** The firm operates under the oversight of a **Chief Data and Analytics Officer** (Teresa Heitsenrether as of 2024) with enterprise-wide accountability for AI governance. The firm's AI governance structure integrates legal, compliance, cybersecurity, and data ethics teams into AI initiative reviews, with the Firmwide Chief Data Officer function aligning data platforms with MRM, legal, and security.

**Regulatory Environment:** Regulated by the Federal Reserve as the holding company regulator, and the OCC as the primary regulator of JPMorgan Chase Bank, N.A. The firm's model risk programme is reviewed annually by OCC examiners as part of the Large Bank Supervision framework.

**Key Governance Tool:** JPMorgan has invested heavily in proprietary model governance infrastructure, including bespoke model registry and workflow tools that connect model development environments to the formal governance pipeline.

---

### 6.2 Goldman Sachs

**Overview:** Goldman Sachs has a distinctive model risk culture shaped by its "Strats" (Quantitative Strategies) heritage — a deep tradition of mathematically rigorous quantitative analysis embedded throughout the firm's businesses. The Model Risk Management group at Goldman Sachs is described as "a multidisciplinary group of quantitative experts" located across New York, Dallas, London, Warsaw, Hong Kong, and Bangalore.

**Model Universe:** Goldman's models span derivatives valuation (including complex structured products), risk management (VaR, stress), electronic trading algorithms, credit risk, and increasingly machine learning applications. The firm uses "stochastic processes, machine learning, optimization techniques, statistical analyses and numerical techniques" across its model portfolio.

**Governance Structure:**
Goldman's Risk Committee (Board-level) established a **Technology Risk Subcommittee (TRiS)** in June 2024, specifically to enhance oversight of technology-related risk matters, including model and AI risk. This reflects the firm's recognition that technology risk — including model risk for AI-embedded systems — requires dedicated board-level attention.

The **Model Risk Management group** reports within the firm's risk management function and provides independent oversight and approval of all quantitative models. Goldman's MRM maintains the Quantitative Research validation function, which reviews the most complex models (derivatives pricing, exotic structured products) with PhDs in mathematics, physics, and finance.

**"Strats" Culture:** Goldman's quantitative strategists are embedded in every major business: equities, fixed income, commodities, currencies (FICC), investment banking, and asset management. This creates a complex first-line landscape where the boundary between model development and model use is often less distinct than at more traditional commercial banks. The MVU must maintain independence while engaging constructively with highly sophisticated first-line quants.

**Regulatory Environment:** Supervised by the Federal Reserve as a bank holding company following Goldman's conversion to a bank holding company in 2008. Also subject to SEC, CFTC, PRA (for its London entity Goldman Sachs International), and MAS (for its Singapore operations).

---

### 6.3 Wells Fargo

**Overview:** Wells Fargo's MRM programme has been shaped more than any other U.S. bank's by a protracted series of regulatory enforcement actions that exposed deep weaknesses in its risk management culture and governance infrastructure.

**The Consent Order History:**
- **April 2018 (OCC)**: OCC Consent Order (EA2018-025) arising from the bank's failure to maintain a compliance risk management programme commensurate with its size and complexity. While focused primarily on compliance risk, this order reflected a broader governance failure that extended to model risk — Wells Fargo had applied models (for mortgage interest rate locks and collateral protection insurance) without adequate controls, resulting in customer harm and regulatory violations.
- **February 2018 (Federal Reserve)**: The Federal Reserve imposed an unprecedented **asset cap** on Wells Fargo, limiting the bank to its year-end 2017 total assets of approximately $1.95 trillion until it demonstrated sufficient improvements to its board governance and risk management. This order specifically cited deficiencies in enterprise risk management that encompassed the bank's model risk infrastructure.
- **September 2024 (OCC)**: A new OCC Consent Order addressed anti-money laundering and financial crimes risk management, including requirements to enhance AML and sanctions risk management practices and obtain OCC approval before expanding into certain product categories.

**Enterprise Risk Transformation:** In response to the Federal Reserve's 2018 asset cap order, Wells Fargo undertook a multi-year, multi-billion dollar enterprise risk management transformation. This included:
- Rebuilding the Model Risk Management function from the ground up with new leadership
- Substantially increasing MVU staffing and expertise
- Implementing new model governance technology platforms
- Enhancing model inventory completeness and quality
- Creating a more rigorous model approval process with clearer escalation paths

The bank confirmed termination of the 2018 OCC compliance consent order in February 2025, a significant milestone in its remediation journey. However, the Federal Reserve asset cap remained in place as of mid-2026, and new enforcement actions in AML continued to demonstrate the breadth of Wells Fargo's governance challenges.

**Lessons:** The Wells Fargo experience demonstrates that MRM failures rarely occur in isolation. They typically co-occur with failures in broader risk culture, compliance infrastructure, and board oversight. A technically competent MVU cannot compensate for an organisation that does not treat model risk as a genuine constraint on business conduct.

---

### 6.4 Bank of America

**Overview:** Bank of America articulates its overall business philosophy through the "Responsible Growth" framework, which commits the bank to growing within its risk framework and serving clients and communities responsibly. This philosophy extends directly to model governance.

**Scale:** Bank of America operates approximately 270 AI models across its operations (as of late 2025), across applications including Erica (virtual assistant), fraud detection, credit scoring, AML, and treasury management. The bank's formal model inventory spans thousands of models across all risk and business domains.

**MRM Framework:** Under the **Enterprise Model Risk Policy**, the bank's Model Risk Management function is required to perform "end-to-end model oversight, including independent validation before initial use, implementation monitoring, ongoing monitoring reviews through outcomes analysis and benchmarking, and periodic revalidation."

**AI Governance:** Bank of America has established an AI governance framework with **human oversight, transparency, and accountability** as its central tenets. The bank specifically acknowledges in its 10-K that "models are subject to inherent limitations from simplifying assumptions, uncertainty regarding economic and financial outcomes, and emerging risks, including from applications that rely on AI" — a direct acknowledgement that AI-specific model risk requires disclosure-level attention.

**Responsible Growth Alignment:** The bank integrates model risk appetite with its broader risk appetite framework, ensuring that the growth ambitions of individual business lines are constrained by the model governance capacity available to appropriately validate and monitor new models.

**Regulatory Environment:** Supervised by the Federal Reserve (holding company) and OCC (Bank of America, N.A.). Subject to annual CCAR stress testing model requirements and EBA reporting requirements for its European operations.

---

### 6.5 Citigroup

**Overview:** Citigroup's model risk management programme has been profoundly shaped by a regulatory transformation effort that began in 2020 and continued through the mid-2020s in response to multiple regulatory enforcement actions.

**The Regulatory Transformation:** In October 2020, the OCC issued a Consent Order against Citibank, N.A. identifying critical deficiencies in risk management, internal controls, and **data governance**. The OCC found that Citibank had failed to:
- Establish effective front-line units, independent risk management, internal audit, and control functions
- Develop and execute on a comprehensive plan to address data governance deficiencies, including data quality errors
- Produce timely and accurate management and regulatory reporting

The OCC assessed a $400 million civil money penalty at initial issuance. In July 2024, both the OCC and the Federal Reserve issued additional Civil Money Penalty Consent Orders (totalling $135.6 million) because of Citigroup's "insufficient progress" in rectifying data quality and risk management issues. The OCC specifically amended its 2020 order to reflect Citi's "failure to meet remediation milestones."

**Relevance to Model Risk:** Citigroup's data governance failures are directly relevant to model risk management because data quality is foundational to model performance. A bank that cannot produce accurate, timely data for regulatory reporting cannot reliably validate models against actual outcomes, cannot detect data drift in model inputs, and cannot perform the outcome analysis that SR 11-7 requires.

**Global Model Risk Policy:** Citi operates a **Global Model Risk Policy** that applies across its worldwide operations, establishing minimum standards for model development, validation, approval, monitoring, and retirement. The Global Model Risk function operates within Citi's Independent Risk Management organization, reporting to the Chief Risk Officer.

**Responsible Technology Framework:** Citi's AI governance sits within a "Responsible Technology" framework that addresses AI fairness, transparency, accountability, and safety — principles that overlay the technical MRM framework for AI/ML models.

**Organizational Complexity:** Citigroup's model governance faces a particular cross-border governance challenge given its global footprint across more than 100 countries. A model used globally may be subject to simultaneously applicable requirements from the Federal Reserve, OCC, PRA, ECB/SSM, MAS, and various other national regulators — each with potentially different validation expectations, risk-tiering requirements, and documentation standards.

---

### 6.6 HSBC

**Overview:** HSBC operates model risk management at a uniquely complex scale, given its presence in more than 60 countries and its positioning as the primary international banking bridge between Western financial markets and Asian markets (particularly China and Hong Kong).

**MRM Structure:** HSBC's **model risk management and independent model review** team sits within Global Risk, providing oversight of modelling approaches used across the Group and ensuring model performance transparency. Critically, the MRM function is kept "separate from the risk analytics functions that are responsible for the development of models" — a structural independence requirement directly reflecting SS1/23 and SR 11-7 principles.

**Pillar 3 Disclosure:** HSBC's 2024 Pillar 3 disclosures confirm that "model risk remains a key area of focus given the regulatory scrutiny in this area, with local regulatory exams taking place in many jurisdictions and the PRA's supervisory statement 1/23 (SS1/23) coming into effect." This disclosure confirms the bank is actively managing compliance with the PRA's new model risk framework for its UK-regulated entities.

**AI Governance:** HSBC published its **Principles for the Ethical Use of Data and AI** in July 2024, setting out the firm's commitments to fairness, transparency, accountability, and human oversight in AI deployment. The principles address:
- Meaningful forums for challenging AI design or use
- Explainability requirements for consequential AI decisions
- Data privacy protections in AI applications
- Cross-border data governance considerations

**Organizational Restructuring:** In October 2024, HSBC announced a significant simplification of its organisational structure, creating four global businesses effective January 2025. This restructuring was designed to create clearer lines of accountability — directly relevant to model governance, where ambiguous ownership across complex matrix organisational structures has historically created gaps.

**Cross-Border Governance Challenge:** HSBC provides perhaps the clearest example of the cross-border governance challenge in global banking. A credit scoring model used in the UK must satisfy PRA SS1/23 requirements; the same model used in Hong Kong must satisfy HKMA guidelines; used in the United States, it must satisfy OCC requirements; used in Germany, ECB/SSM expectations apply. HSBC has invested in a global minimum standard that satisfies the most demanding regulatory jurisdiction, with local supplements for jurisdiction-specific requirements.

---

### 6.7 Deutsche Bank

**Overview:** Deutsche Bank's model risk programme has been significantly shaped by the ECB's Targeted Review of Internal Models (TRIM), the most extensive supervisory review of bank internal models in European history.

**TRIM Impact:** The TRIM project, conducted by ECB Banking Supervision between 2016 and 2021, covered 65 institutions directly supervised by the ECB (Single Supervisory Mechanism — SSM), accounting for more than 85% of total assets in the SSM. The review conducted approximately 200 on-site investigations and identified approximately 5,800 findings across all risk types, of which roughly 30% were classified as high severity. TRIM resulted in a 12% increase — approximately €275 billion — in risk-weighted assets for the investigated models, reflecting more stringent application of capital requirements.

For credit risk models specifically, TRIM found average deficiencies of 13 findings per bank for Loss-Given-Default (LGD) calculations and 7 findings per bank for Probability-of-Default (PD) parameters. Governance deficiencies were pervasive: banks showed lack of formal policies for model changes, failure to conduct annual back-tests, and inadequate independence between model developers and validators.

**Deutsche Bank's TRIM Remediation:** Deutsche Bank — one of the largest SSM-supervised institutions — undertook extensive remediation of TRIM findings, investing more than €1 billion annually in control improvements in 2023 and 2024. The bank's 2024 Annual Report stated that "remediation work on its most important regulatory programmes is now nearing completion," a sign that the post-TRIM governance rebuild was reaching maturity.

**Model Governance Restructuring:** In response to TRIM and related supervisory expectations, Deutsche Bank restructured its model governance framework to include:
- Strengthened internal validation independence
- Enhanced data governance for model inputs
- More rigorous change management controls for model updates
- Improved back-testing programmes with formal annual review requirements

**ECB Guide to Internal Models (February 2024):** The ECB published an updated Guide to Internal Models in February 2024, reinforcing supervisory expectations following TRIM and setting the framework for ongoing supervision of IRB, IMA, and CCR models under SSM banks. Deutsche Bank and other major SSM banks continue to operate under the ECB's detailed model supervision programme.

**Regulatory Environment:** Deutsche Bank is supervised by the ECB/SSM as its primary prudential regulator, with BaFin (Germany's national authority) acting as the national competent authority. The bank's global operations also subject it to PRA oversight (for its London branch), Federal Reserve and OCC oversight (for its U.S. operations), and various other national regulators.

---

### 6.8 UBS

**Overview:** UBS, following its acquisition of Credit Suisse in 2023, became the world's second-largest wealth manager and a systemically important institution at the global level. Its model risk management programme operates under both Swiss regulatory requirements (FINMA) and international requirements for its global operations.

**FINMA Regulatory Framework:** FINMA Circular 2017/1 assigns responsibility for developing and operating risk monitoring systems and applying principles for risk analysis and model validation to the bank's risk management function. FINMA approves and monitors the use of many models — particularly IRB credit risk models, VaR models for market risk, and internal model methods for counterparty credit risk — with all these models requiring independent model validation under FINMA's expectations.

**Credit Suisse Integration:** The integration of Credit Suisse's model inventory into UBS's governance infrastructure represents one of the most complex MRM integration challenges in banking history. Credit Suisse maintained its own model risk management function, with its own tiering framework, validation standards, and model inventory. Merging these two large inventories — while simultaneously managing Credit Suisse's legacy risk management weaknesses that had contributed to its failure — required extensive model-by-model review and governance framework harmonisation.

**SSM Relevance:** While UBS itself is not directly supervised by the ECB/SSM (as a Swiss bank), its EU subsidiaries are subject to SSM supervision and therefore must comply with the ECB's internal model requirements. UBS thus navigates a dual regulatory framework — FINMA for the group as a whole, ECB/SSM for its EU entities.

**Key Focus Areas:** FINMA's 2024 Risk Monitor identified model risk (alongside cybersecurity and operational resilience) as a priority supervisory focus area for Swiss banks, reflecting the global trend toward heightened regulatory scrutiny of bank model governance.

---

### 6.9 Barclays

**Overview:** Barclays is one of the UK's two largest banks by total assets and among the most significant subjects of PRA model risk supervision. The bank's implementation of SS1/23 — the PRA's Model Risk Management Principles that took effect May 17, 2024 — represents the UK benchmark for how major banks are adapting their MRM frameworks to the new UK regulatory standard.

**SS1/23 Implementation:** SS1/23 applies to banks, building societies, and PRA-designated investment firms with approval to use internal models for regulatory capital purposes. Barclays, with internal model approvals for credit risk (IRB), market risk (IMA), and counterparty credit risk (IMM), falls squarely within scope.

Following publication of SS1/23 in May 2023 and its enforcement from May 2024, Barclays (like other in-scope firms) completed a **self-assessment against the five principles** at a granular, line-by-line level, and developed a multi-year remediation plan mapped to identified gaps. Key remediation themes across the industry include:
- **DQM (Deterministic Quantitative Methods)** identification and governance: Many institutions had not previously brought spreadsheet-based and deterministic models into formal governance
- **Model governance uplift**: Policy and standards enhancements to reflect the SS1/23 principles
- **Enhanced model risk tiering**: More nuanced tiering dimensions across all model families
- **Improved model inventories**: Comprehensive documentation systems capturing all models within scope

**Barclays Pillar 3 Disclosure:** Barclays publishes a Pillar 3 Report annually that includes model risk disclosures. The 2024 report provides information about the bank's internal model approvals, risk-weighted assets computed under internal models, and regulatory capital impacts.

**PRA Supervision:** The PRA has indicated that it will conduct Section 166 (s166) skilled person reviews of SS1/23 implementation at a number of firms. These independent reviews, commissioned by the PRA at the bank's expense, represent a significant supervisory tool for assessing the quality and completeness of MRM remediation.

---

### 6.10 BNP Paribas

**Overview:** BNP Paribas is Europe's largest bank by assets and a leader in European AI governance, operating at the intersection of the EU AI Act's requirements and traditional banking model risk frameworks.

**AI Governance:** BNP Paribas has implemented a **hybrid AI governance model** anchored by an internal AI factory and a large language model (LLM)-as-a-service platform, with federated governance by business and function. This structure reflects the bank's recognition that centralised control of AI model governance is insufficient at enterprise scale — individual business lines need meaningful governance capability, while the centre sets minimum standards and provides shared infrastructure.

**EU AI Act Compliance:** The bank's AI governance and infrastructure strategy has been built in direct anticipation of the EU AI Act, which establishes a risk-based approach imposing strict obligations on entities developing or deploying high-risk AI systems within the EU. BNP Paribas's risk management of AI emphasises explainability, lifecycle risk management, and compliance with evolving European requirements.

**RISK AIR:** BNP Paribas's model risk function operates through a dedicated AI and model risk team (RISK AIR) within its Group Risk function. RISK AIR was involved in drafting a white paper on "Controlling the Risks of Artificial Intelligence Systems" with Hub France IA, demonstrating the bank's engagement with the broader AI governance ecosystem.

**European Regulatory Context:** BNP Paribas is supervised by the ECB/SSM as its primary prudential regulator, with the Autorité de contrôle prudentiel et de résolution (ACPR) as the French national competent authority. As a major SSM bank, BNP Paribas's internal models are subject to the same post-TRIM supervisory framework as Deutsche Bank and other SSM institutions.

---

### 6.11 Morgan Stanley

**Overview:** Morgan Stanley presents a distinctive model risk profile among the major banks, reflecting its positioning as primarily a capital markets, wealth management, and investment management firm. Unlike universal banks with large consumer lending books, Morgan Stanley's model inventory is weighted toward:

- **Quantitative trading models** (electronic trading, market-making, derivatives pricing)
- **Risk models** (VaR, Expected Shortfall, credit exposure models for trading book)
- **Investment models** (portfolio construction, factor models for investment management)
- **Wealth management models** (financial planning, goal-based investment models, suitability assessment)
- **Credit risk models** for its lending activities (institutional lending, wealth management credit)

**Model Risk Framework:** Morgan Stanley's model risk disclosures in its 2024 10-K note that "credit exposures may be concentrated by counterparty, product, sector, or geographic region, and although our models and estimates account for correlations among related types of exposures, a change in the market or economic environment may result in credit losses in excess of amounts forecast." This framing captures the fundamental challenge of market risk and credit risk models: they are calibrated to historical data and historical correlations that may not hold in tail scenarios.

**Risk Committee Governance:** Morgan Stanley's Board-level Risk Committee oversees the firm's model risk programme, with the Risk Committee Charter published publicly. The committee oversees "the firm's policies with respect to risk assessment and risk management" including model risk.

**Portfolio Risk Platform:** Morgan Stanley's Portfolio Risk Platform, which received an industry award for innovation, reflects the firm's investment in technology-enabled risk management infrastructure — a foundation for modern model governance.

**E*TRADE and Institutional Integration:** Morgan Stanley's 2020 acquisition of E*TRADE brought a large consumer-facing digital platform with its own model infrastructure (credit scoring, fraud detection, customer analytics) into the firm's model governance perimeter. Integrating E*TRADE's models into the Morgan Stanley MRM framework was a significant undertaking that illustrates the model governance challenges inherent in bank M&A.

---

## 7. Bank-by-Bank Summary Table

| Bank | Headquarters | Primary Regulator(s) | MVU Structure | Known AI Governance Program | Key Public Disclosure |
|---|---|---|---|---|---|
| JPMorgan Chase | New York, USA | Federal Reserve, OCC | Firmwide Model Risk (FMR) group, reports to CRO | AI Model Risk Framework (2024), aligned to EU AI Act and NIST AI RMF; CDAO oversight | 10-K "Estimations and Model Risk" section; AI Governance page |
| Goldman Sachs | New York, USA | Federal Reserve, OCC | Model Risk Management group (global, multidisciplinary); Technology Risk Subcommittee (TRiS) at Board level | Board-level TRiS subcommittee (est. June 2024) | Proxy Statement; Risk Committee Charter |
| Wells Fargo | San Francisco, USA | Federal Reserve, OCC | Rebuilt MRM function post-2018; model governance technology platform implemented | Post-consent-order governance rebuild; ongoing under Fed asset cap | OCC Consent Orders (2018, 2024); Federal Reserve enforcement order |
| Bank of America | Charlotte, USA | Federal Reserve, OCC | Enterprise Model Risk, reports within Global Risk | 270 AI models; AI governance framework: human oversight, transparency, accountability | 10-K "Model Risk" section; Responsible Growth framework |
| Citigroup | New York, USA | Federal Reserve, OCC | Global Model Risk within Independent Risk Management | Responsible Technology framework; data quality transformation under consent orders | OCC/Fed Consent Orders (2020, 2024); 10-K |
| HSBC | London, UK | PRA (UK); ECB/SSM (EU); Fed/OCC (US) | Global MRM team within Global Risk, independent of risk analytics | Principles for Ethical Use of Data and AI (July 2024) | Pillar 3 Disclosures (annual); AI Ethics Principles document |
| Deutsche Bank | Frankfurt, Germany | ECB/SSM (primary); BaFin; PRA (UK); Fed (US) | Internal Validation function within risk management; post-TRIM rebuilding | Ongoing post-TRIM remediation; AI governance within Group Risk | Pillar 3 Report; Annual Report; ECB TRIM outcomes |
| UBS | Zurich, Switzerland | FINMA (group); ECB/SSM (EU subsidiaries) | Group model risk management under FINMA Circular 2017/1 | Credit Suisse integration; group-wide model governance harmonization | Annual Report; Pillar 3 disclosures; FINMA reports |
| Barclays | London, UK | PRA (primary); ECB/SSM (EU); Fed (US) | Independent model validation within Group Risk; SS1/23 compliance programme | SS1/23 multi-year remediation plan; DQM governance uplift | Pillar 3 Report; SS1/23 self-assessment |
| BNP Paribas | Paris, France | ECB/SSM (primary); ACPR; PRA (UK); Fed (US) | RISK AIR (AI and model risk); federated model governance by business | Hybrid AI governance model; LLM-as-a-service platform; EU AI Act compliance | Annual Report; AI governance white paper |
| Morgan Stanley | New York, USA | Federal Reserve, OCC; SEC | Model risk management within Risk Management; Board Risk Committee oversight | Portfolio Risk Platform; E*TRADE model integration | 10-K; Risk Committee Charter; Pillar 3 disclosures |

---

## 8. The Consent Order as MRM Governance Catalyst

### 8.1 The Wells Fargo Template

The Wells Fargo regulatory saga illustrates what regulators can do — and what they expect — when bank governance fails comprehensively. The Federal Reserve's unprecedented asset cap, imposed in February 2018, was not a fine payable in a fixed amount; it was a structural constraint on the bank's ability to grow, maintained until the bank could demonstrate that its risk management infrastructure was adequate. This reflects a regulatory philosophy that chronic governance failures require structural remediation, not just financial penalties.

For model risk specifically, the Federal Reserve's Enterprise Risk Management Consent Order requirement was explicit: Wells Fargo was required to submit a plan demonstrating comprehensive improvements to its risk management governance, with model risk as a component of that broader infrastructure.

### 8.2 The Citigroup Data-Model Nexus

Citigroup's enforcement history illustrates a different but equally important point: **data quality failures are model risk failures**. A model is only as good as its inputs. When Citigroup's data governance was found to produce inaccurate regulatory reporting, this reflected systemic failures in the data infrastructure that underlies model-based risk computations.

The OCC's 2020 consent order identified failures in data quality management and data governance — deficiencies that directly compromised the bank's ability to validate models effectively, detect model performance degradation, and compute regulatory capital accurately. The $135.6 million in additional penalties in 2024 for insufficient progress underscored the regulatory expectation that data governance and model risk are inseparable.

### 8.3 The ECB TRIM as Collective Enforcement

The ECB's TRIM project (2016–2021) represents a form of collective enforcement action — not a single bank's failures, but a systemic examination of how European banks implement their internal models. The 5,800 findings across 65 banks, and the €275 billion increase in risk-weighted assets, reflected the ECB's conclusion that banks had systematically under-estimated their model risks and over-optimised their capital computations.

TRIM's governance findings were particularly instructive: banks showed inadequate independence between model developers and validators, insufficient back-testing discipline, and weak model change management. These are structural governance failures, not technical ones, and they illustrate why the Three Lines of Defense model is not a compliance formality but a genuine risk control.

---

## 9. Scale, Complexity, and the Model Proliferation Problem

### 9.1 The Scale Reality

Large banks now manage model inventories of extraordinary scale. Survey data from Moody's Analytics indicates that approximately one-fifth of commercial banks report more than 1,000 models in use, with model inventories at the largest G-SIBs believed to range from 3,000 to more than 10,000 models depending on what is counted. Growth has been rapid: 16% of commercial banks and 17% of investment banks reported inventory increases exceeding 50% over just two years.

This scale creates fundamental governance challenges:
- **Validation backlogs**: MVUs cannot keep pace with the volume of models requiring validation if headcount grows linearly with model count
- **Tiering quality**: With thousands of models, the tiering process itself must be reliable and defensible
- **Monitoring automation**: Manual monitoring is not feasible at scale; automated monitoring tools become essential
- **Inventory accuracy**: Maintaining an accurate, complete inventory of thousands of models requires both continuous discovery processes and robust change management

### 9.2 The Shadow Model Problem

Perhaps the most persistent operational challenge in bank MRM is the existence of **shadow models** — models operating outside the formal governance process that are unknown to the MVU and absent from the official inventory.

Shadow models arise from several sources:
- **Spreadsheet models**: Excel-based analytical tools developed by business analysts or finance teams, used to support business decisions but never registered in the model inventory
- **Python notebooks**: Data science experiments that became operational decision tools without passing through the formal model governance pipeline (particularly acute with the proliferation of Jupyter notebooks in bank analytics teams)
- **Third-party tools**: Vendor analytical tools or consulting firm outputs used in business decisions without being registered as models
- **Ad-hoc models**: One-off analytical exercises that became recurring operational tools

**Detection Approaches:**
Banks use several methods to surface shadow models:
- **IT change management integration**: Requiring IT teams to flag any new analytical application deployed in a business environment
- **Data lineage tools**: Using data governance platforms (Collibra, Alation, Informatica) to identify data flows that originate from unregistered analytical processes
- **Business process reviews (RCSA integration)**: Embedding model discovery questions into the bank's Risk and Control Self-Assessment process, asking business units to identify any quantitative tool that produces outputs used in decision-making
- **Annual attestations**: Requiring business unit heads to certify annually that all models under their supervision are registered in the inventory

The shadow model problem is particularly acute for AI/ML models, where Python notebooks can transition from exploration to production use without the formal handoffs that traditional software development processes would require.

### 9.3 Cross-Border Model Governance Challenges

Global banks face a unique challenge when the same model is deployed across multiple regulatory jurisdictions, each with potentially different governance requirements:

- A **credit scoring model** used in the UK must satisfy PRA SS1/23; in the U.S., SR 11-7; in Germany, ECB internal model requirements and the ECB Guide to Internal Models; in Singapore, MAS TRM guidelines; in Hong Kong, HKMA risk management guidelines.
- A **GenAI model** used in the EU falls under the EU AI Act's high-risk AI system requirements; in the U.S., it is subject to emerging interagency guidance; in the UK, the FCA's AI strategy applies.
- A **market risk VaR model** used for regulatory capital across multiple booking locations must satisfy the specific IMA requirements of each relevant jurisdiction.

Banks manage this complexity through **global minimum standards** — a baseline governance requirement that satisfies the most demanding jurisdiction — supplemented by **local supplements** that address jurisdiction-specific requirements.

### 9.4 Legacy Model Remediation

Every large bank carries a portfolio of **legacy models** — models built under older governance standards, often with limited documentation, using data sources that may no longer be available, and potentially running on deprecated technology platforms. These models present particular validation challenges:

- Historical development documentation may be incomplete or missing
- The original model developers may have left the bank
- The code may be in legacy languages (FORTRAN, SAS, early C++) that current validators cannot readily review
- The model's behaviour may not be well understood by current users

Remediating legacy models — either by bringing them into full compliance with current standards or replacing them — is a multi-year programme for most large banks and a significant driver of MVU resource consumption.

---

## 10. Regulatory Evolution: From SR 11-7 to the 2026 Interagency Guidance

### 10.1 The Revised U.S. Interagency Guidance (April 2026)

On April 17, 2026, the Federal Reserve, FDIC, and OCC jointly replaced the 2011 SR 11-7 / OCC 2011-12 guidance with a "more risk-based, principles-driven framework." The revised guidance reflects fifteen years of evolution in how banks use models — from the relatively narrow world of statistical credit risk models to the sprawling landscape of AI, machine learning, and generative AI.

Five core shifts in the revised guidance:
1. **Risk-based tiering**: Models categorized by materiality with proportionate controls, rather than a one-size-fits-all approach
2. **Lifecycle governance**: Continuous linkage required across development, validation, deployment, monitoring, and retirement
3. **Effective challenge**: Reproducible challenger models, benchmarking, and sensitivity testing treated as first-class governance artefacts
4. **Continuous monitoring**: Real-time performance and data drift tracking with materiality-tied thresholds
5. **AI inclusion**: Generative AI and agentic systems now explicitly inherit MRM principles

The guidance demands that "evidence must be produced as a byproduct of how models are built, not reconstructed after the fact" — a statement that directly challenges the documentation-after-the-fact culture that has plagued bank MRM for years.

### 10.2 PRA SS1/23 (UK)

The PRA's five principles under SS1/23 — Model Identification and Risk Classification, Governance, Model Development/Implementation/Use, Independent Model Validation, and Model Risk Mitigants — provide a comprehensive framework that is broadly consistent with SR 11-7 in its intent but more explicitly articulated in its requirements.

SS1/23's explicit extension to **DQMs (Deterministic Quantitative Methods)** — including material complex spreadsheet tools — is particularly noteworthy, as it captures a class of models that has historically been excluded from formal MRM governance at many banks.

### 10.3 ECB Internal Model Supervision (Post-TRIM)

Following TRIM, the ECB has maintained active internal model supervision through its ongoing supervisory programme. The February 2024 updated Guide to Internal Models provides detailed ECB expectations for IRB, IMA, and CCR models. Banks supervised under the SSM continue to undergo specific model-focused supervisory reviews (IMI — Internal Model Investigations) as part of the annual supervisory examination cycle.

---

## 11. Emerging Challenges: AI, GenAI, and the MRM Frontier

The arrival of large language models and generative AI in banking operations has created a new category of model governance challenges that existing MRM frameworks were not designed to address. These challenges — and the evolving regulatory and industry responses — are detailed in File 7 (GenAI Governance in Banking). Key themes include:

- **Non-determinism**: LLMs do not produce the same output from the same input, breaking fundamental assumptions of deterministic model validation
- **Hallucination**: LLMs can produce plausible but factually incorrect outputs, creating new categories of operational and customer harm risk
- **Explainability**: Standard model explainability tools (SHAP, LIME) do not cleanly apply to transformer-based models
- **Scope creep**: GenAI tools deployed for productivity applications (code generation, document summarisation) can be repurposed for consequential decisions if governance boundaries are not maintained
- **Vendor opacity**: Foundation models from major AI providers (OpenAI GPT series, Anthropic Claude, Google Gemini) are not transparent in their training data, model weights, or internal mechanisms — creating fundamental validation challenges for banks using these models

Banks are responding with **AI governance frameworks** that sit alongside (and progressively integrate with) traditional MRM frameworks. JPMorgan's alignment with the NIST AI RMF, HSBC's Principles for Ethical Use of Data and AI, BNP Paribas's hybrid AI governance model, and Goldman Sachs's Technology Risk Subcommittee all represent early institutional responses to the AI governance challenge.

---

## Cross-References

- [02_sr11_7_deep_dive.md](02_sr11_7_deep_dive.md) — Detailed analysis of SR 11-7 requirements and interpretation
- [05_model_validation_methodology.md](05_model_validation_methodology.md) — Technical craft of model validation: conceptual soundness, back-testing, challenger models
- [06_model_inventory_and_governance_ops.md](06_model_inventory_and_governance_ops.md) — Operational machinery: model inventories, tiering frameworks, MRM tooling
- [07_genai_governance_banking.md](07_genai_governance_banking.md) — Generative AI and LLM governance challenges in banking
- [12_explainability_fairness_bias.md](12_explainability_fairness_bias.md) — Explainability, fairness, and bias requirements for AI models in banking
- [13_model_drift_monitoring_mlops.md](13_model_drift_monitoring_mlops.md) — Model monitoring, drift detection, and MLOps integration with MRM

---

*Sources consulted: JPMorgan Chase 2024 Form 10-K (SEC EDGAR); Goldman Sachs 2024 Proxy Statement (SEC EDGAR); Wells Fargo OCC Consent Order EA2018-025; HSBC Pillar 3 Disclosures at 31 December 2024; HSBC Principles for the Ethical Use of Data and AI (July 2024); Citigroup OCC Consent Order (October 2020); ECB TRIM Project Report (April 2021); ECB Newsletter "The targeted review of internal models — the good, the bad and the future" (May 2019); ECB Guide to Internal Models (February 2024); Bank of England Supervisory Statement SS1/23 (May 2023, in force May 2024); KPMG PRA Model Risk Management Principles analysis; Moody's Analytics "The Evolving Model Risk Management Landscape in Banking"; Databricks "Model Risk Management in 2026: A Banker's Guide" (April 2026); Federal Reserve Enterprise Risk Management Consent Order Requirements (Wells Fargo); OCC AML Consent Order against Wells Fargo (September 2024); Yields.io "The Three Lines of Defence in Model Risk Management"; Solytics Partners "Three Lines of Defense Framework for Prudent Model Risk Management"; BNP Paribas AI governance disclosures; Bank of America CIO Dive "Bank of America runs 270 AI models across operations" (2025).*
