# Model Inventory and Governance Operations: The Operational Machinery of MRM

## File Metadata
- **Scope:** Operational MRM — model inventories, tiering, risk appetite, Model Risk Committees, shadow models, vendor models, and governance tooling
- **Cluster:** B — Bank Practice: Traditional ML MRM
- **Reading order:** 6/14
- **Related files:** [04_bank_mrm_frameworks.md](04_bank_mrm_frameworks.md), [05_model_validation_methodology.md](05_model_validation_methodology.md), [07_genai_governance_banking.md](07_genai_governance_banking.md), [13_model_drift_monitoring_mlops.md](13_model_drift_monitoring_mlops.md)
- **Regulators/bodies covered:** Federal Reserve (SR 11-7/SR 26-2), OCC, Basel Committee (IRB/FRTB), IFRS/FASB (IFRS 9/CECL)
- **Tags:** model-inventory, model-tiering, model-risk-appetite, model-risk-committee, shadow-models, vendor-models, MRM-platform, IBM-OpenPages, MLOps, regulatory-capital, IFRS-9, CECL, IRB

---

## 1. Model Inventory Fundamentals

### 1.1 What a Model Inventory Is and Why It Exists

The **model inventory** — also called the model registry, model catalogue, or model register — is the central repository of record for all models an institution develops, acquires, or uses. It is the operational backbone of the entire MRM programme: without an accurate, complete inventory, the bank cannot know what it needs to govern, cannot allocate validation resources intelligently, cannot report its aggregate model risk to the Board, and cannot demonstrate to regulators that it has control over its model landscape.

SR 11-7 is explicit: "banks should maintain a complete model inventory." The 2026 revised interagency guidance (SR 26-2) reinforces this, describing the inventory as the foundation from which all lifecycle governance activity flows. PRA SS1/23 requires firms to maintain "a robust and auditable triage process" to identify models within scope — which presupposes a complete inventory.

The inventory is not merely a list. It is a living database that records the current status of every model across all dimensions of governance relevance: who owns it, when it was last validated, what its current performance status is, what findings are open against it, what regulatory uses it has, and when it is next scheduled for review. At large banks, this database may contain tens of thousands of records and must be maintained with discipline to remain useful.

### 1.2 Standard Model Record Fields (SR 11-7 and Best Practice)

A well-constructed model record contains the following categories of information:

**Identification Fields:**
- **Model ID**: Unique, persistent identifier assigned at registration and never reassigned
- **Model Name**: Descriptive name (e.g., "Retail Mortgage PD Model v3.2")
- **Model Version**: Current version number, with version history linked
- **Model Type**: Classification by function (credit risk, market risk, operational risk, fraud detection, AML, pricing, stress testing, customer behaviour, etc.)
- **Business Line / Use Case**: The business unit(s) using the model and the specific decision or process it supports
- **Model Classification**: A further classification within the model type (e.g., within "credit risk": origination scorecard, account management scorecard, IFRS 9 PD model, stress PD model)

**Ownership and Accountability Fields:**
- **Model Owner (First Line)**: Named individual accountable for the model's performance, documentation, and compliance; typically a senior business professional
- **Model Developer / Development Team**: The team or individual that built the model
- **Model Risk Manager (Second Line)**: The named MVU staff member assigned as the model's second-line point of contact
- **Business Line Sponsor**: Senior business executive who sponsors the model's continued use
- **Data Owner(s)**: Individual(s) responsible for the data inputs the model relies on

**Risk and Governance Classification Fields:**
- **Materiality Tier**: The model's assigned risk tier (Critical / High / Medium / Low, or Tier 1/2/3/4)
- **Regulatory Capital Use Flag**: Boolean indicating whether the model is used in the computation of regulatory capital (IRB, FRTB, SA-CCR, etc.)
- **CCAR/DFAST Flag**: Boolean indicating whether the model is used in stress testing for regulatory capital adequacy
- **Customer-Facing Flag**: Boolean indicating whether model outputs directly affect customers (credit decisions, pricing, product eligibility, communications)
- **External Model / Vendor Model Flag**: Boolean indicating whether this is a third-party or vendor model
- **Data Sensitivity Classification**: Classification of the sensitivity of data processed by the model (personal data, confidential financial data, public data)
- **Operational Dependency Level**: Assessment of how severely operations would be disrupted if the model became unavailable (Critical / High / Medium / Low)

**Lifecycle Status Fields:**
- **Development Date**: Date when the model was first developed or initially approved
- **Current Approval Status**: Approved / Approved with Conditions / Expired / Use-with-Exception / Retired
- **Approval Authority**: The individual or committee that issued the current approval
- **Last Validation Date**: Date of most recent validation or annual review
- **Last Validation Opinion**: The opinion issued at the last validation (Approved / Approved with Conditions / Not Approved)
- **Next Scheduled Review Date**: The date by which the next periodic review must be completed
- **Revalidation Type Due**: Full revalidation / Annual monitoring review / Event-triggered review
- **Days Until Review**: Automatically calculated field flagging models approaching or past their review date

**Performance and Findings Fields:**
- **Current Model Risk Rating**: Overall model risk rating from the most recent validation (numerical or colour-coded)
- **Open Findings Count**: Number of unresolved findings from all validation events
- **Open Critical Findings**: Boolean and count — any open critical finding is a key risk indicator requiring immediate attention
- **Open Major Findings**: Count of unresolved major findings with their target remediation dates
- **Known Limitations**: Summary of documented, ongoing model limitations and the compensating controls in place
- **Monitoring Status**: Assessment of current monitoring performance (Normal / Watch / Escalated)
- **Last Monitoring Review Date**: Date of most recent formal monitoring assessment

**Regulatory and Cross-Reference Fields:**
- **Regulatory References**: List of regulations, guidance, or supervisory requirements to which this model must comply
- **Downstream Model Dependencies**: Other models that use this model's output as an input
- **Upstream Model Dependencies**: Models whose output is consumed by this model
- **Validation History**: Links to all historical validation reports
- **Related Policies**: Links to applicable model risk policies and standards

### 1.3 SR 11-7 and SR 26-2 Inventory Requirements

SR 11-7 (2011) required banks to maintain a model inventory that captures "purpose and products for which the model is designed, actual or expected usage, and any restrictions on use." The 2026 SR 26-2 guidance strengthened this expectation significantly, requiring inventories to support:

- **Risk-based tiering** with documented criteria and governance over the tiering process
- **Lifecycle linkage**: The inventory record must connect across the full lifecycle, from development through retirement
- **Continuous model discovery**: Not just a static registry but an active process for identifying new models and changes to existing models
- **Proportionality evidence**: The inventory must demonstrate that governance is calibrated to model risk, not applied uniformly

The OCC's Model Risk Management Comptroller's Handbook (2021) similarly requires that inventories record each model's "purpose, products, inputs, outputs, status, risk tier, validation status, and known limitations."

---

## 2. Model Tiering Frameworks

### 2.1 The Purpose of Tiering

Model tiering is the mechanism through which the proportionality principle — applying greater governance intensity to higher-risk models — is operationalised. Without tiering, banks face an impossible choice: apply rigorous, resource-intensive validation to every model (which is not economically feasible at the scale of thousands of models), or apply lighter governance uniformly (which fails to adequately control the most material models). Tiering allows banks to be rigorous where it matters most and proportionate everywhere else.

The Journal of Risk Model Validation's research on industry tiering practices confirms that "nearly all firms assign models to several risk tiers rather than seeking to rank them individually from high to low," and that most institutions implement three to four risk tiers.

### 2.2 Tiering Criteria

Industry practice has converged on two primary dimensions of risk that determine tier assignment:

**1. Probability of Model Failure:**
- Model complexity (more complex models have more ways to fail)
- Firm's experience with this type of model (novelty increases failure risk)
- Implementation platform (bespoke code vs. well-tested commercial software)
- Data quality and stability of inputs
- Degree of human oversight in applying outputs

**2. Impact of Model Failure:**
- Financial materiality: portfolio size, P&L sensitivity, capital impact
- Regulatory use: models used in regulatory capital calculations, regulatory reporting, or regulatory stress tests attract the highest impact ratings
- Customer impact: models that directly affect customer financial outcomes (credit decisions, pricing) carry elevated impact ratings
- Reputational risk: models whose failures could be publicly visible or could attract regulatory attention
- Operational dependency: how severely the bank's operations would be disrupted

**Tiering Tool Implementation:** Most banks use a **scorecard approach** — assigning numerical scores across each dimension, applying weights, and computing a total score that maps to a tier. Decision trees (sequential binary questions) are used by some institutions but are generally considered less nuanced than scorecards for multi-dimensional risk assessment.

### 2.3 Tier Definitions: A Standard Framework

The following represents a representative four-tier framework used by major banks (exact definitions and thresholds vary by institution):

| Tier | Label | Typical Characteristics | Validation Frequency | Approval Authority |
|---|---|---|---|---|
| **Tier 1** | Critical | Regulatory capital models (IRB, FRTB, SA-CCR); CCAR/DFAST stress models; models with potential P&L or capital impact >$500M; models with direct Board-level regulatory exposure | Annual full revalidation | Model Risk Committee + Board ratification |
| **Tier 2** | High | Material credit risk models; flagship customer-facing models (major scoring engines); key AML/fraud detection models; IFRS 9 ECL models; financial reporting models | Annual full revalidation or intensive monitoring review | Chief Model Risk Officer / senior MRC sub-committee |
| **Tier 3** | Medium | Significant business-line risk or pricing models; operational models with material downstream impact; selected customer analytics models | Every 2–3 years | Head of Model Risk Management |
| **Tier 4** | Low | Internal management reporting models; low-volume or low-impact analytical tools; decision-support models with limited financial consequences | Every 3–5 years, or lighter-touch monitoring | Senior Validator / Validation Team Lead |

**Proportionality guidance from industry research:** The optimal tier distribution avoids either extreme. A tier that contains fewer than approximately 10% of total models is too narrow (over-segmented), while a single tier containing more than 30–40% of models is too broad (under-segmented). This implies that for a bank with 3,000 models, Tier 1 (Critical) might contain 150–300 models, Tier 2 (High) might contain 300–600 models, and the remaining models are distributed across Tiers 3 and 4.

### 2.4 Automatic Overrides and Governance Constraints

Industry practice includes **automatic overrides** for specific model uses that bypass the scorecard outcome:
- Any model used in regulatory stress testing (CCAR, DFAST, ILAAP) is automatically Tier 1, regardless of scorecard score
- Any model used to compute regulatory capital under an approved internal model approach (IRB, IMA) is automatically Tier 1
- Any customer-facing credit decision model used for populations exceeding a defined threshold (e.g., 100,000 customers annually) is automatically Tier 2 or above

Governance of the tiering tool itself is important: the tiering scorecard is a decision-making tool and should itself be subject to validation and periodic review. Industry standards are "an evolving process with rising standards," with leading practice requiring that tiering scorecards be maintained in the model inventory, owned by the MVU, and reviewed annually.

### 2.5 Annual Tiering Review Process

Every model in the inventory must be reassessed at least annually to confirm its tier assignment remains appropriate. Triggers for mid-cycle tier reassignment include:
- Material change in the model's use or business context
- Significant increase in the model's financial exposure
- Addition of a regulatory capital use
- Material change in the model's complexity (e.g., replacement of a logistic regression with an ML model)
- Internal audit finding or regulatory examination finding regarding the appropriateness of the current tier

The model owner typically initiates tier change requests, but the head of the MRM function holds final authority over tier assignment. Some banks allow model owners to request a lower tier assignment for their models but not to self-assign a lower tier without MVU concurrence.

---

## 3. Model Risk Appetite

### 3.1 What Model Risk Appetite Means

Model risk appetite is the bank's formally stated tolerance for the risk arising from model use — the amount of model risk the institution is willing to accept in pursuit of its business objectives. It sits within the bank's overall risk appetite framework, alongside credit risk appetite, market risk appetite, operational risk appetite, and other risk categories.

A model risk appetite statement is more than a general statement of prudence; it must be specific enough to be measurable and actionable. Key attributes of a well-designed model risk appetite statement:
- **Quantifiable**: Expressed in terms of metrics that can be measured and reported
- **Linked to consequences**: Breaches must trigger defined escalation actions
- **Calibrated to business risk**: Appetite must reflect the actual risks the bank faces, not a generic industry standard
- **Board-approved**: The Board Risk Committee (or equivalent) must formally approve the model risk appetite as part of the overall risk appetite framework

### 3.2 What a Model Risk Appetite Statement Looks Like

A representative model risk appetite statement for a large bank:

*"The Bank maintains a Low appetite for model risk. The Bank does not tolerate the use of models that have not received appropriate validation approval, except in defined use-with-exception circumstances subject to compensating controls and time-limited approval. The Bank does not tolerate persistent use of models that have exceeded their scheduled revalidation date without a documented action plan. The Bank maintains a Medium appetite for model-related losses from model parameter estimation error and model limitations, subject to appropriate monitoring and compensating controls.*

*Key risk metrics include: (i) percentage of Tier 1 models with open critical findings < 0%; (ii) percentage of models past their scheduled revalidation date < 5%; (iii) number of Tier 1/2 models on use-with-exception status < 3 at any time; (iv) percentage of models with monitoring results flagged 'Escalated' that have been presented to the MRC within 30 days > 95%."*

### 3.3 Metrics Used in Model Risk Appetite

The most commonly used model risk appetite metrics:

| Metric | Description | Typical Tolerance |
|---|---|---|
| **% Models with Open Critical Findings** | Proportion of approved models carrying unresolved critical findings | Zero tolerance (0%) |
| **% Models Past Scheduled Revalidation** | Models that have exceeded their scheduled review date without a completed review or documented exception | < 5% of total inventory; < 0% for Tier 1 |
| **# Tier 1/2 Models on UWE** | Count of high-materiality models approved only with use-with-exception status | Hard cap (e.g., < 5) |
| **Validation Backlog** | # of models awaiting initial validation beyond policy timelines | Expressed as a count with escalation trigger |
| **Open Findings Aging** | # of major findings open beyond their target remediation date | Escalation trigger at 90 days past due |
| **% Models with Active Monitoring** | Proportion of Tier 1/2 models with active, up-to-date monitoring results | > 95% |
| **Model Failure Events** | Documented instances of model error leading to financial loss, customer harm, or regulatory issue | Zero tolerance for material events |

### 3.4 Escalation Triggers and Breach Reporting

When model risk appetite metrics breach defined thresholds, escalation procedures are activated:
- **Amber breach**: Metrics approaching tolerance limits; notification to Chief Model Risk Officer; action plan required within 30 days
- **Red breach**: Metrics at or beyond tolerance limits; immediate notification to CRO and MRC; escalation to Board Risk Committee at next scheduled meeting; mandatory remediation plan with defined milestones

Model risk appetite breaches must be disclosed in regular model risk reporting and tracked to resolution.

---

## 4. Model Risk Committee Operations

### 4.1 Charter Template Elements

The Model Risk Committee (MRC) charter documents the committee's purpose, authority, and operating procedures. Key elements:

**Purpose and Authority:**
The MRC provides management-level oversight of the enterprise model risk profile, approves high-tier models, monitors model risk appetite, and provides governance oversight for the firmwide model risk programme. The MRC has authority to approve or reject models at Tier 1/2 level, to override first-line model decisions where model risk concerns warrant it, and to escalate matters to the Board Risk Committee.

**Scope:**
All models within the enterprise model inventory. May include specific provisions for regulatory capital models, AI/ML models, and vendor models.

**Composition and Membership:**
Standard standing membership (voting):
- Chief Risk Officer (Chair)
- Chief Financial Officer or delegate
- Chief Technology Officer / Chief Data Officer
- Chief Model Risk Officer / Head of Model Validation (Secretary and primary presenter)
- Head of Credit Risk
- Head of Market Risk
- Head of Operational Risk
- Business line heads for major model-using businesses (typically 2–4 representatives)

Non-voting standing attendees:
- Chief Compliance Officer
- Head of Internal Audit (observer — maintains independence)
- Legal/Regulatory Affairs representative

**Quorum:** Typically requires CRO (or designated deputy) plus majority of standing voting members. Decisions cannot be made without quorum.

**Voting Requirements:** Majority of voting members present. Some banks require CRO affirmative vote for Tier 1 model approvals.

**Conflicts of Interest:** Members with a material interest in a specific model outcome (e.g., the head of the business unit that owns the model) may be required to recuse from the vote on that model.

### 4.2 Meeting Cadence and Agenda

**Standard Meeting Cadence:**
- **Monthly standing meeting**: Reviews model approvals, findings updates, use-with-exception status, escalations, and regulatory developments
- **Quarterly model risk appetite review**: Full review of all MRA metrics, comparison against thresholds, assessment of trends
- **Ad hoc meetings**: Called within 48–72 hours for material model failures, regulatory enforcement actions related to model risk, or sudden deterioration in multiple model risk metrics

**Standard Monthly Agenda:**
1. Approval of previous minutes and action items update (10 minutes)
2. Chief Model Risk Officer's model risk update — headline metrics dashboard (10 minutes)
3. Model approval presentations — Tier 1/2 models completed since last meeting (30–60 minutes depending on volume)
4. Use-with-exception status review — current UWE models, expiry dates, compensating controls (15 minutes)
5. Open findings aging review — critical and major findings past target dates (15 minutes)
6. Regulatory and supervisory update — relevant regulatory developments, examination findings (10 minutes)
7. Emerging model risk issues — new model types, new data sources, AI governance concerns (15 minutes)
8. Any other business (10 minutes)

### 4.3 Sub-Committee Structure

Large banks typically operate specialist sub-committees:

**Regulatory Capital Model Sub-Committee:**
- Specialised oversight for IRB, FRTB, SA-CCR, IFRS 9 ECL, and CECL models
- Typically chaired by CRO or CFO
- Includes model development team heads, finance function representatives, and regulatory affairs
- Meets monthly or quarterly; outputs feed to the main MRC

**AI/GenAI Governance Forum (AI Model Oversight Group):**
- Dedicated oversight for generative AI, large language models, and advanced ML models
- Typically co-chaired by CTO/CDO and CRO
- Includes legal, compliance, data ethics, and business representation
- Reviews all new AI/GenAI model submissions before they enter the main MRC pipeline

**Stress Testing Model Oversight Committee (STMOC):**
- Oversees models used in CCAR, DFAST, ICAAP, and ILAAP stress tests
- Heavy CFO function involvement due to capital implications
- Typically convened quarterly with annual deep-dive reviews before regulatory submission

### 4.4 Board-Level Reporting

The Board Risk Committee receives regular model risk reporting:

**Quarterly Dashboard:**
- Tier distribution of model inventory (% by tier)
- Validation activity: completions, new submissions, backlog
- Model risk appetite metrics: current values vs. tolerance thresholds
- Open critical findings: count and aging
- Use-with-exception status: current count, oldest outstanding
- Regulatory and supervisory model risk developments
- Material model incidents (failures, errors, regulatory citations)

**Annual Firmwide Model Risk Report:**
- Year-in-review: validation activity, major validations completed, key findings
- Model inventory trends: growth, changes in tier distribution, retirements
- Model risk appetite performance: full year history of metrics
- Regulatory examination summary: any model risk-related examination findings or citations
- Emerging risks: new model types, new regulatory expectations, AI governance
- Forward plan: anticipated model launches, planned validations, resource outlook

---

## 5. Shadow Models and Undiscovered Model Proliferation

### 5.1 The Shadow Model Problem

**Shadow models** are quantitative tools that are used in business decision-making but are not registered in the official model inventory and have not been subject to formal MRM governance. They represent uncontrolled model risk — the bank may be unknowingly dependent on tools whose theoretical basis is unsound, whose code has not been reviewed for errors, and whose performance has never been formally assessed.

Shadow models arise from several common sources:

**Spreadsheet Models:**
Excel and Google Sheets workbooks are the most common source of shadow models. Business analysts build sophisticated models in spreadsheet software — IFRS 9 staging logic in a complex Excel workbook, credit limit adjustment formulas embedded in a multi-tab spreadsheet, valuation models for products that haven't yet been migrated to the bank's official pricing systems. These spreadsheets often become critical operational tools without anyone recognising they meet the regulatory definition of a model.

**Python and Jupyter Notebooks:**
The explosion of data science activity within banks has created a new generation of shadow models. A data scientist on a trading desk builds an exploratory Python notebook to analyse customer behaviour patterns; the analysis proves useful; colleagues start referencing it; it gets incorporated into a weekly reporting process; a year later, it is effectively a production model that has never been validated. Jupyter notebooks are particularly problematic because they blur the distinction between exploration and production.

**Third-Party and Consulting Firm Outputs:**
Banks frequently receive analytical outputs from consultants (McKinsey, Deloitte, Oliver Wyman) or industry data providers (MSCI, Bloomberg, CoreLogic) that are used in business decisions. These vendor outputs often contain embedded models, but their governance status is ambiguous — they may not have been registered as vendor models in the inventory.

**Legacy System Embeds:**
Older operational systems often contain embedded analytical logic — credit scoring rules embedded in origination systems, pricing formulae embedded in core banking platforms — that was implemented years or decades ago and has never been registered in a formal model inventory.

### 5.2 Why the Problem is Especially Acute for AI/ML

The traditional model governance pipeline — register, document, submit for validation, receive approval, deploy — was designed for a world where models were built by specialist quants using structured processes and deployed through controlled IT change management. The AI/ML era has disrupted all of these assumptions:

- **Model development is democratised**: Any business analyst with Python skills can build a predictive model in hours
- **Experimentation-to-production pipelines are compressed**: In MLOps environments, a model trained in a notebook can be deployed to production rapidly, potentially bypassing governance checkpoints
- **Model boundaries are blurred**: A data scientist's analytical tool, a model developer's experiment, and a production decision system can all look identical in a Jupyter notebook
- **Change management is continuous**: ML models may be retrained continuously (streaming learning), making the discrete "model update" event less meaningful

The governance challenge is not that ML models are inherently ungovernable; it is that the governance infrastructure was not designed for the pace and scale at which ML development occurs. Banks are addressing this by requiring that **all ML model development occurs within governed notebook environments** where tracking, lineage, and feature registration are automatic — making governance a byproduct of development rather than an afterthought.

### 5.3 Detection Approaches

**IT Change Management Integration:**
Requiring that any new analytical application be registered in the IT change management system before deployment. IT change management teams are trained to identify requests that indicate new model development (requests for new data feeds, new compute environments, new database connections) and to flag them to the MRM function.

**Data Lineage Analysis:**
Data governance platforms (Collibra, Alation, Informatica) can be used to identify data flows that originate from unregistered analytical processes. If a database query is producing output that feeds into a business report but has no corresponding model record in the inventory, it may indicate a shadow model.

**RCSA Integration:**
Risk and Control Self-Assessments (RCSA) are operational risk management exercises in which business units identify and assess their key risks and controls. Banks increasingly incorporate model discovery questions into RCSAs: business unit managers are asked to identify any quantitative tool used in their area that produces outputs used in decision-making, reporting, or risk measurement — and to confirm that each such tool is registered in the model inventory.

**Annual Attestation Process:**
Model owners and business unit heads are required to attest annually that all models under their supervision are registered in the inventory and that the inventory records are accurate. These attestations are documented and reviewed by Internal Audit.

**Validation Discovery Reviews:**
When a validator encounters evidence of model use in the course of a validation — for example, discovering that the model being validated takes inputs from another analytical tool — the validator is required to investigate whether that analytical tool is registered.

### 5.4 Remediation: Bringing Shadow Models into Governance

When a shadow model is discovered, the bank must determine:
1. **Is it a model?** Does it meet the regulatory definition of a model (inputs + quantitative methodology + outputs used in decision-making)?
2. **What is its risk tier?** Apply the tiering framework to determine the appropriate governance level
3. **What is its current validation status?** Has it ever been validated? By whom?
4. **What is its current use?** Is it actively used in production decisions, and if so, for what?

Remediation options:
- **Register and validate**: Register the shadow model and submit it for validation as a priority item, with interim use-with-exception approval if the business need is urgent
- **Decommission**: If the model is not genuinely needed or can be replaced by an already-validated model, decommission it
- **Documentation catch-up**: For lower-tier models, a streamlined retrospective documentation and validation process may be appropriate

---

## 6. Vendor and Third-Party Models

### 6.1 The Non-Delegable Responsibility

SR 11-7 established a principle that is now embedded in all major MRM regulatory frameworks: **"A bank's use of a vendor model does not diminish its responsibility for model risk management."** This means that a bank that deploys a vendor's credit scoring model, a Bloomberg valuation model, or an AI fraud detection tool from a third-party provider is still fully responsible for ensuring that model meets the bank's governance standards.

This principle creates a significant operational challenge. Vendor models — by definition — come with limited or no access to source code, training data, or model architecture details. The bank is being asked to validate a model it cannot fully inspect.

### 6.2 The Challenge of Validating Opaque Models

For many vendor models, the bank receives:
- A score or output
- A user guide describing inputs and intended use
- Summary documentation of the model's development approach (often high-level and non-specific)
- Validation reports produced by the vendor (potentially reviewed by the vendor's own team, not independent of the vendor)

What the bank typically does not receive:
- Source code
- Training data
- Detailed parameter values
- Full methodology documentation
- Independent third-party validation

The regulatory guidance acknowledges this challenge. The OCC's Model Risk Management Handbook notes that when model components are proprietary, banks may need to "use other means to evaluate vendor models, including the following: evaluate the vendor's development and testing processes; independently backtest the model's outputs against their own data; benchmark results against alternative approaches."

### 6.3 Contractual Requirements for Vendor Model Documentation

Best-practice vendor model governance includes contractual requirements in vendor agreements:
- **Documentation access**: Vendor must provide sufficient methodology documentation for the bank to perform a meaningful conceptual soundness review
- **Right to audit**: Bank reserves the right to commission an independent assessment of the vendor's model development processes
- **Material change notification**: Vendor must notify the bank of any material change to the model within a defined timeframe (e.g., 30 days)
- **Performance data**: Vendor must provide ongoing model performance data to support the bank's monitoring programme
- **Regulatory cooperation**: Vendor must cooperate with any regulatory examination or inquiry that involves their model

Large banks often have sufficient market power to negotiate these terms. Smaller banks may have less leverage with major vendors but should still seek documentation rights as a minimum.

### 6.4 Benchmarking Approaches for Black-Box Vendor Models

When source code access is unavailable, validators rely on **empirical validation** approaches:
- **Independent back-testing**: Test the vendor model's outputs against the bank's own historical outcomes data; compare predicted default rates against actual default rates, or predicted fraud scores against confirmed fraud cases
- **Benchmarking**: Compare vendor model outputs against an internally-developed challenger model or an alternative vendor model for the same purpose
- **Sensitivity testing**: Feed systematic variations of model inputs to the vendor model and assess whether outputs respond in the expected direction and magnitude
- **Outcomes analysis**: Compare vendor model predictions against actual outcomes in the bank's own portfolio — particularly important if the bank's portfolio differs materially from the vendor's model development population
- **Vendor validation report review**: Obtain and critically review any independent validation report produced for the vendor model, assessing the independence and rigour of the review

CRISIL's guidance on vendor model validation notes that the key principle is demonstrating that "the model performs adequately for the bank's specific use case and portfolio" — not that the vendor's model development meets all standards, but that its outputs are reliable in the bank's context.

### 6.5 Vendor Management Integration with MRM

Vendor models should be integrated into the bank's vendor management framework:
- **Annual vendor risk review**: Assess vendor model performance as part of the broader vendor relationship management process
- **Model-specific vendor due diligence**: Beyond standard vendor due diligence, include model-specific assessment of the vendor's development quality, validation practices, and change management disciplines
- **Vendor model inventory**: Maintain a sub-register of all vendor models within the broader model inventory, with vendor name, contract terms, and access rights documented
- **Regulatory change management**: Monitor regulatory changes that may affect vendor model adequacy (e.g., new regulatory requirements for credit scoring fairness that the vendor's model may need to address)

---

## 7. Model Lifecycle Management Tooling

### 7.1 The Case for Purpose-Built MRM Platforms

Managing a model inventory of thousands of models, with complex lifecycle workflows, multi-tier approval processes, and regulatory reporting requirements, is not feasible with general-purpose project management tools or spreadsheets. Purpose-built MRM platforms (and GRC platforms with MRM modules) provide:
- **Centralised model records** with version control and history
- **Workflow automation** that guides models through lifecycle stages with appropriate approval gates
- **Automated scheduling** of revalidation dates with escalation alerts
- **Findings management** with tracking, aging reports, and remediation workflows
- **Reporting capabilities** for the Board, MRC, regulators, and business units
- **Integration with development and MLOps environments** for automated model discovery

### 7.2 Major MRM Platform Vendors

**IBM OpenPages Model Risk Governance:**
IBM OpenPages is the most widely deployed enterprise GRC platform in large financial institutions. Its Model Risk Governance module provides:
- Centralised model inventory with configurable fields
- Automated workflow for model lifecycle stages (registration, development, validation, approval, monitoring, retirement)
- Integration with IBM Watson OpenScale for AI model monitoring (bias and drift detection)
- Regulatory content integration: Wolters Kluwer provides custom fields for regulatory content in OpenPages, enabling banks to map model governance requirements to specific regulatory frameworks
- Board and management reporting dashboards

IBM OpenPages 9.1.1 (2025 release) introduced AI agent capabilities and automation features designed to reduce manual documentation burden while maintaining governance rigour. Major financial institutions with the most complex, multi-entity risk environments are the primary target market.

**SAS Model Risk Management:**
SAS provides a purpose-built MRM platform that combines model governance with the firm's deep analytics heritage. Key features:
- End-to-end model lifecycle management
- Built-in analytics for model performance monitoring and outcome analysis
- Validation workflow tools with statistical testing capabilities integrated directly into the platform
- Risk appetite and KRI reporting
- Strong integration with SAS's broader risk management suite (credit risk, market risk, stress testing)

SAS MRM is particularly strong in environments where the bank also uses SAS for model development, as it provides a common governance and analytics infrastructure.

**Wolters Kluwer OneSumX:**
OneSumX provides integrated finance, risk, and regulatory reporting capabilities. Its risk management module encompasses model governance as part of a broader enterprise risk management suite. Key differentiators:
- Strong regulatory content library, updated for regulatory changes across jurisdictions
- Integration between model governance and regulatory reporting (connecting model risk to FINREP, COREP, and other regulatory reporting requirements)
- Achieved top-ten ranking in Chartis RiskTech 100 (2025)

**ValidMind:**
ValidMind is a newer, AI-native MRM platform specifically designed for the ML model governance challenge. Key features:
- Python SDK that integrates directly into model development workflows, generating governance documentation as a byproduct of development
- Automated test generation and execution for ML models
- LLM-specific validation support
- Integration with MLflow, Databricks, and other MLOps platforms
- Particularly well-suited for banks modernising their data science governance rather than managing legacy statistical model inventories

Oliver Wyman has partnered with ValidMind for its MRM practice, a signal of growing enterprise credibility.

**MetricStream and Archer (SAP):**
Both MetricStream and Archer (SAP) are broad GRC platforms with MRM modules. They are typically deployed in institutions that want a single GRC platform to manage operational risk, compliance, audit, and model risk — sacrificing some MRM-specific depth for the benefit of a unified risk and control framework.

**Moody's Analytics Model Registry:**
Moody's Analytics offers a model registry solution that integrates with its broader suite of credit risk analytics (RiskCalc, CreditEdge). It provides model inventory management with deep integration to Moody's credit risk models and analytics — particularly relevant for banks that use Moody's models as challengers or benchmarks.

### 7.3 GRC Platform Integrations

MRM platforms commonly integrate with:
- **ServiceNow**: For change management, IT ticket integration, and risk register
- **Jira / Azure DevOps**: For model development project tracking and code change management
- **Confluence / SharePoint**: For documentation storage and version control
- **LDAP / Active Directory**: For user access management and role-based permissions

### 7.4 Git/MLOps Integration with Model Registry

The integration between MLOps platforms and MRM governance tools is one of the most active areas of MRM technology development. Banks operate complex data science and model deployment pipelines:
- **Databricks / Spark**: For large-scale ML model development and training
- **MLflow**: For experiment tracking, model versioning, and deployment
- **Kubeflow / Metaflow**: For ML pipeline orchestration
- **Seldon / BentoML**: For model serving and deployment
- **GitHub / GitLab**: For code version control

The governance challenge is connecting these technical artefacts to the MRM governance framework:
- A model trained in MLflow should automatically create or update a record in the MRM system
- A model deployed through Seldon should trigger a governance checkpoint before reaching production
- Feature importance outputs from model training should automatically populate the model's validation documentation
- Performance metrics tracked in the MLOps platform should feed the MRM system's monitoring dashboards

**Platform connections being implemented by leading banks:**
- Collibra integrates with MLflow and Microsoft Azure AI Foundry to track AI models as governed assets, enabling complete and immutable audit trails linking model versions to specific training datasets
- IBM OpenPages offers direct connectors to ML development environments
- ValidMind's Python SDK generates governance documentation directly from model development notebooks

The 2026 U.S. interagency guidance's requirement that "evidence must be produced as a byproduct of how models are built, not reconstructed after the fact" is a direct regulatory endorsement of this integration approach.

### 7.5 Data Lineage Tools

Data lineage tools are essential for model governance at scale because they answer a fundamental question: what data sources does each model depend on, and how does that data flow from source to model input?

**Collibra:**
Market leader in enterprise data governance for financial services. Collibra Data Lineage documents the full lifecycle of data, tracking how data moves through the organisation. Collibra dominates in financial services where data lineage documentation is a regulatory requirement. Integration with MLflow enables AI models to be tracked as governed assets with full training data lineage.

**Alation:**
Alation provides a data catalogue and data governance platform with strong lineage capabilities. Scores well for automated column-level lineage tracing.

**Informatica:**
Informatica's Intelligent Data Management Cloud provides comprehensive data lineage and governance capabilities, with particular strength in managing complex, multi-system data integration environments.

For model governance, data lineage tools enable:
- **Model input traceability**: Confirm that every data input to a model is documented and governed
- **Shadow model detection**: Identify unregistered data flows that may indicate shadow models
- **Impact analysis**: When a data source changes, identify all models that depend on that data and require reassessment
- **Regulatory audit trail**: Demonstrate to regulators that model input data is managed under appropriate governance

---

## 8. Regulatory Capital Models: Special Governance Requirements

### 8.1 The Elevated Stakes of Regulatory Capital Models

Models used to compute regulatory capital requirements occupy a special category in bank MRM governance. Errors or weaknesses in these models can:
- Lead to incorrect capital computation, resulting in capital inadequacy without the bank's awareness
- Trigger regulatory enforcement actions if capital computation errors are identified in supervisory examinations
- Create competitive distortions if a bank's capital requirements are systematically lower than justified by actual risk (as the TRIM exercise found across European banks)
- Expose the bank to material financial loss if capital is insufficient during a stress event

For these reasons, regulatory capital models receive the highest tier classification, the most intensive validation requirements, and are subject to additional supervisory oversight beyond standard MRM governance.

### 8.2 IRB (Internal Ratings-Based) Model Governance Requirements

Under Basel III (and continuing under Basel IV/CRR3), banks using the IRB approach to credit risk must obtain supervisory approval for their internal PD, LGD, and EAD models. Key governance requirements:

**Supervisory Approval:** Initial IRB model implementation requires formal approval from the prudential supervisor (Federal Reserve/OCC in the U.S.; ECB/SSM in Europe; PRA in the UK; FINMA in Switzerland). This approval process is intensive — regulators conduct their own review of model methodology, data quality, validation standards, and governance.

**Annual Reporting:** IRB banks must report to their supervisor regularly on the performance of approved models, including back-testing results comparing predicted PD/LGD against actual outcomes.

**Materiality of Changes:** Even after initial approval, material changes to IRB models require advance notification to (and potentially approval from) the supervisor before implementation. Non-material changes may be implemented and reported on an annual basis.

**Capital Comparison (Regulatory EL vs. Accounting Provisions):** IRB banks must compare the total accounting provisions against the regulatory expected loss (EL). Any shortfall between provisions and regulatory EL is deducted from Common Equity Tier 1 capital.

**Post-TRIM Standard (ECB Banks):** Following TRIM, the ECB's revised Guide to Internal Models (February 2024) sets detailed expectations for credit risk, market risk, and counterparty credit risk internal models at SSM-supervised banks. Banks must demonstrate ongoing compliance with these standards through their internal validation processes.

### 8.3 IFRS 9 Expected Credit Loss Model Governance

IFRS 9 requires banks to estimate and recognise expected credit losses over a forward-looking horizon, using probability-weighted forecasts that incorporate current and forward-looking economic information. This creates significant model governance challenges:

**Three-Stage Classification:** IFRS 9 requires classification of financial instruments into three stages based on changes in credit quality since origination:
- Stage 1: 12-month ECL (performing)
- Stage 2: Lifetime ECL (significant increase in credit risk — SICR)
- Stage 3: Lifetime ECL (credit-impaired)

The models that determine SICR and the PD/LGD/EAD estimates for each stage are IFRS 9 ECL models — all high-tier models in the MRM framework.

**Governance Expectations:** Regulatory expectations (from EBA, PRA, and national supervisors) for IFRS 9 model governance include:
- Board and senior management oversight of staging decisions, model assumptions, and judgmental inputs
- Independent validation of ECL model methodology, including the forward-looking scenarios and their probability weights
- Audit committee oversight of the financial reporting implications
- Documentation of expert judgment overlays applied to model outputs

**Interaction with Regulatory Capital:** Under Basel rules, accounting provisions can partially offset regulatory expected loss, reducing the CET1 deduction for the provision shortfall. Banks must carefully manage the interaction between their IFRS 9 ECL models and their IRB regulatory EL models — inconsistencies between them attract regulatory scrutiny.

### 8.4 CECL Model Governance (U.S. GAAP)

The Current Expected Credit Loss (CECL) standard (ASC 326), which replaced the incurred loss model for U.S. banks under GAAP, requires recognition of lifetime expected credit losses from origination. Key differences from IFRS 9:
- CECL requires lifetime losses for all financial instruments at origination (no three-stage structure)
- CECL therefore demands more complex models for instruments with long contractual lives (mortgages, student loans)

The model governance requirements for CECL are broadly similar to IFRS 9: Board oversight, independent validation, and auditor review of model assumptions and methodology. The CECL implementation wave (2019–2023) generated significant investment in model governance infrastructure at U.S. banks.

**Joint MRM + Finance Governance:** Because CECL reserves directly affect financial reporting (balance sheet and income statement), CECL model governance necessarily involves both the Risk function (MRM) and the Finance/Accounting function. The interface between model risk governance and financial reporting governance is one of the most complex cross-functional coordination challenges in bank MRM.

### 8.5 FRTB (Fundamental Review of the Trading Book)

FRTB (Basel III final reforms, being phased in through 2025–2028) introduces new requirements for market risk capital computation:
- The **Internal Model Approach (IMA)** requires banks to use Expected Shortfall (replacing VaR) computed over a stressed period and with liquidity-adjusted holding periods
- IMA approval is now desk-level (not firm-level), requiring each trading desk to demonstrate it meets the P&L Attribution Test and the Back-Testing requirements
- Models are subject to the Non-Modellable Risk Factor (NMRF) regime, which requires capital add-ons for risk factors that are not modellable

The FRTB model governance requirements are among the most technically demanding in banking:
- Each IMA desk requires its own regulatory approval
- P&L Attribution must be monitored daily
- Back-testing against both trading desk P&L and risk-theoretical P&L
- Comprehensive documentation of risk factor modellability determinations

FRTB models are automatically Tier 1 in any bank's tiering framework.

---

## 9. Model Risk Reporting

### 9.1 What Gets Reported to Whom

Effective model risk reporting provides the right information to the right governance body at the right level of detail:

| Recipient | Reporting Frequency | Key Content |
|---|---|---|
| **Board Risk Committee** | Quarterly + Annual report | Model risk appetite metrics vs. tolerance; material model incidents; regulatory developments; inventory overview |
| **CRO / CMRO** | Monthly | Full model risk dashboard; validation pipeline; MRC decisions; emerging issues |
| **Model Risk Committee** | Monthly | Detailed validation findings; use-with-exceptions; open findings aging; regulatory updates |
| **Business Unit Heads** | Quarterly | Models under their ownership: validation status, open findings, monitoring results |
| **Internal Audit** | As needed + planned audits | Model risk programme effectiveness assessment; specific model governance reviews |
| **Regulators** | Per regulatory submission schedule | DFAST stress testing model documentation; IRB/IMA annual performance reports; SS1/23 self-assessment; Pillar 3 disclosures |

### 9.2 Model Risk Dashboard Metrics

A comprehensive model risk dashboard typically displays:

**Inventory Overview:**
- Total model count by tier (Tier 1/2/3/4)
- New models added in the period
- Models retired in the period
- Models on use-with-exception (count and tier breakdown)

**Validation Pipeline:**
- Models pending initial validation
- Models pending revalidation (by days overdue)
- Validations completed in the period (with validation opinion breakdown)
- Validation backlog (models past scheduled review date)
- Estimated backlog resolution timeline

**Model Risk Quality:**
- Open critical findings (count, aging, business unit)
- Open major findings (count, aging, remediation status)
- Models with monitoring status "Escalated"
- PSI breaches (models where population stability has deteriorated)

**Appetite Metrics:**
- All MRA KRI values vs. tolerance thresholds (traffic light: green/amber/red)
- Trend charts showing metric trajectory over prior 12 months

**Regulatory Highlights:**
- Regulatory examination findings related to model risk (since last period)
- Upcoming regulatory submission deadlines (DFAST, IRB annual reporting)
- Notable regulatory developments (new guidance, enforcement actions at peers)

### 9.3 Regulatory Reporting on Model Risk

Several regulatory reporting requirements specifically address model risk:

**DFAST/CCAR (U.S.):** Banks subject to DFAST and CCAR must submit comprehensive model documentation as part of their stress testing submissions. The Federal Reserve and OCC review model documentation as part of the supervisory examination of stress testing practices.

**EBA Pillar 3 Disclosures (EU/UK):** EBA regulatory reporting frameworks require banks to disclose information about their use of internal models in regulatory capital computation, including quantitative disclosures about risk-weighted assets computed under internal model approaches.

**FINREP/COREP (EU):** The EBA's FINREP (financial reporting) and COREP (capital adequacy reporting) frameworks require banks to report detailed information that is model-dependent — including IFRS 9 ECL amounts, IRB capital requirements, and market risk capital.

**SS1/23 Self-Assessment (UK PRA):** Banks subject to SS1/23 conducted formal self-assessments of their compliance with the five principles and submitted these to the PRA. The self-assessment process itself becomes a governance document — a public accountability mechanism.

### 9.4 MRM Key Risk Indicators (KRIs) and Key Performance Indicators (KPIs)

**Key Risk Indicators (leading):**
- % of models approaching their scheduled review date (next 30/60/90 days)
- # of models with PSI > 0.15 in the current monitoring period
- # of new model registrations without a scheduled validation date
- # of IT change requests that may indicate shadow model development activity

**Key Performance Indicators (lagging):**
- % of models validated within scheduled timeframe (in period)
- Average time from validation request to validation completion
- % of findings closed within target remediation timeline
- # of model incidents resulting in financial loss or customer harm (target: zero)

---

## 10. Model Decommissioning

### 10.1 When to Decommission a Model

Models should be considered for decommissioning when:
- A superior replacement model has been developed and approved
- The business use for which the model was developed has been discontinued
- The model has persistent, unresolvable performance issues (repeated failed revalidations; persistent PSI breaches; calibration failures)
- The regulatory framework for which the model was developed has changed in a way that renders the model non-compliant
- The data inputs on which the model depends are no longer available
- The model has not been used for a defined period (e.g., 18–24 months) with no active use anticipated

Decommissioning is not the same as retaining a model in inactive status. An officially decommissioned model is removed from the active inventory, its data feeds are disconnected, and its governance record is moved to the archived inventory.

### 10.2 Decommissioning Documentation Requirements

The decommissioning process must be documented:
1. **Decommissioning request**: Business owner's statement of intent to decommission, with rationale and effective date
2. **MVU concurrence**: Second-line acknowledgment that the model can be decommissioned (confirming no ongoing dependencies)
3. **Transition risk assessment**: Assessment of any risks arising from the model's retirement — particularly for regulatory capital models, where a transition period may be required
4. **Data disconnection plan**: Documentation of how model input data feeds will be disconnected
5. **Archive notification**: Confirmation that all model artefacts (code, documentation, validation reports, data) have been archived per the bank's record retention policy
6. **Inventory update**: Model status changed to "Retired" with effective date

### 10.3 Transition Risk During Model Replacement

When a model is being replaced by a successor model, there is an inevitable transition period during which:
- The new model has been approved but the old model is still in production
- Users are migrating decisions from the old model's outputs to the new model's outputs
- The new model's population stability has not been established (it has been validated but not observed in production)

Best practice is to run the new model in parallel with the old model for a defined period (typically 3–6 months for material models), monitoring whether the new model produces materially different outputs and whether those differences are expected and understood. Parallel running documentation should be captured in both models' inventory records.

### 10.4 Archiving Requirements

Regulatory retention requirements in the U.S. require bank records to be maintained for at least 7 years under most applicable requirements. Model governance artefacts — including validation reports, development documentation, approval records, and monitoring history — should be archived for this period in an immutable, retrievable format. Archives should be:
- **Governed**: Access-controlled and managed under the bank's records management policy
- **Immutable**: Records cannot be modified after archiving (ensuring integrity of the governance record)
- **Retrievable**: Can be produced in response to a regulatory examination or legal discovery request within a defined timeframe

The ECB guide to internal models specifically notes that banks must maintain documentation of all retired models for a period consistent with regulatory expectations.

---

## 11. Emerging Developments: AI-Native Governance Operations

The shift from traditional statistical model governance to AI/ML model governance is not merely a change in model type — it requires a fundamental rethinking of how governance operations work.

**From Periodic to Continuous:** Traditional MRM operates on periodic cycles (annual validation, quarterly monitoring reviews). AI/ML models in production can shift in ways that traditional monitoring does not detect quickly enough. Leading banks are moving toward continuous monitoring with automated alerting — tracking model performance, data drift, and population stability in near-real time.

**From Documentation to Evidence Generation:** The traditional governance paradigm requires validators to produce documentation after reviewing a model. The ML governance paradigm increasingly requires that governance evidence is generated automatically as part of model development — training logs, feature importance outputs, performance metrics, and lineage information captured in real-time rather than reconstructed retrospectively.

**From Single Models to Model Systems:** Modern AI applications often involve systems of models working together — a document ingestion pipeline that uses one ML model for text extraction, another for classification, and an LLM for synthesis. Governing individual models in isolation may miss systemic risks that emerge from model interactions. MRM programmes are beginning to develop frameworks for governing **model systems** as well as individual models.

**The 2026 Interagency Guidance Implication:** The April 2026 revised U.S. interagency guidance is explicitly designed to accommodate these shifts. Its emphasis on platform-enforced governance, evidence-as-byproduct, and AI inclusion reflects a regulatory recognition that governance operations must evolve to remain relevant as model technology advances.

---

## Cross-References

- [04_bank_mrm_frameworks.md](04_bank_mrm_frameworks.md) — Bank-by-bank MRM governance structures and the three-lines-of-defense framework
- [05_model_validation_methodology.md](05_model_validation_methodology.md) — Technical validation methodology: what happens during the validation process
- [07_genai_governance_banking.md](07_genai_governance_banking.md) — Governance of generative AI and LLM models: special challenges beyond traditional MRM
- [13_model_drift_monitoring_mlops.md](13_model_drift_monitoring_mlops.md) — PSI/CSI monitoring, data drift detection, and MLOps integration with MRM governance

---

*Sources consulted: Federal Reserve SR 11-7 "Guidance on Model Risk Management" (April 2011); Federal Reserve / FDIC / OCC SR 26-2 revised interagency guidance (April 2026) via Databricks Blog; OCC Model Risk Management Comptroller's Handbook (2021); Journal of Risk Model Validation "Model Risk Tiering: An Exploration of Industry Practices and Principles" (Risk.net); PRA Supervisory Statement SS1/23 (May 2023); KPMG "PRA Model Risk Management Principles" analysis; Lumenova.ai "SR 26-2: Actionable Guide to Model Risk Management"; Moody's Analytics "The Evolving Model Risk Management Landscape in Banking"; CRISIL "Validate Third-Party Vendor Models for US Financial Institution"; Proofpoint "Banking Organizations and Validation of Vendor and Other Third-Party Products Under SR Letter 11-7"; IBM OpenPages product documentation (2025); Wolters Kluwer OneSumX product documentation; ValidMind "SR 11-7 Model Risk Management Compliance" blog; Collibra "Data Lineage for Financial Services"; Databricks "Model Risk Management in 2026: A Banker's Guide"; ECB Guide to Internal Models (February 2024); Risk.net "The New Impairment Model: Governance and Validation" (IFRS 9/CECL); Deloitte Canada "Guideline E-23 is Here" (OSFI E-23); FDIC Model Risk Management Examination Core Analysis; Chartis Research "Model Risk Management Solutions 2024 Quadrant Update"; Baker Tilly "Mastering Model Governance"; Elliott Davis "Building the Foundation: Key Steps for Launching Model Risk Management"; SME Finance Forum "Principles for Model Risk Management" v1.0 (August 2025); OSFI Guideline E-23 – Model Risk Management (2027); Citigroup 2020 OCC Consent Order; Wells Fargo Federal Reserve enforcement requirements.*
