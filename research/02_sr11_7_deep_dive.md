# SR 11-7 Deep Dive: The Foundational US Model Risk Management Framework

## File Metadata
- **Scope:** Deep analysis of SR 11-7 (Federal Reserve) and OCC 2011-12 as the foundational US model risk management regulatory framework, including the April 2026 replacement by SR 26-2
- **Cluster:** A — Regulatory Foundations
- **Reading order:** 2/14
- **Related files:** [01_regulatory_landscape_overview.md](01_regulatory_landscape_overview.md), [04_bank_mrm_frameworks.md](04_bank_mrm_frameworks.md), [06_model_inventory_and_governance_ops.md](06_model_inventory_and_governance_ops.md), [07_genai_governance_banking.md](07_genai_governance_banking.md)
- **Regulators/bodies covered:** Federal Reserve, OCC, CFPB
- **Tags:** SR-11-7, OCC-2011-12, model-definition, model-validation, model-governance, three-lines-of-defense, model-risk, US-regulation, examiner-expectations, SR-26-2

---

SR 11-7, "Supervisory Guidance on Model Risk Management," issued by the Federal Reserve on April 4, 2011, and its companion OCC Bulletin 2011-12, stand as the most cited, most studied, and most consequential regulatory documents in US bank model risk management. In the fifteen years between issuance and the April 2026 revision that superseded them, SR 11-7 became the global reference standard against which MRM programs were benchmarked — adopted in spirit by UK, EU, Singapore, and Australian regulators, and incorporated directly into the curricula of risk management certifications worldwide. This document provides a comprehensive analysis of SR 11-7's full substance: its genesis, its definitions, its three-tier governance framework, its validation requirements, its governance architecture, its application to machine learning, and its enforcement consequences — as well as a detailed analysis of where SR 26-2 (April 2026) departs from the 2011 framework.

---

## 1. Background and Genesis

### 1.1 The Post-2008 Crisis Context

SR 11-7 was not issued in a vacuum. It was a direct regulatory response to the catastrophic model failures that contributed to the 2007–2009 global financial crisis. Multiple categories of quantitative models failed simultaneously and spectacularly: mortgage credit scoring models failed to anticipate the correlation of default risk in a nationwide housing price decline; value-at-risk (VaR) models used by trading desks across Wall Street dramatically underestimated tail risk; collateralized debt obligation (CDO) pricing models embedded assumptions about default correlation that were empirically unfounded; and liquidity models failed to account for simultaneous market-wide stress.

The pattern that emerged from post-crisis reviews was deeply concerning to supervisors. At institution after institution, the same failures appeared: models had been developed without rigorous documentation of assumptions; validation had been superficial or non-existent; model users did not understand the limitations of the outputs they were relying upon; governance was fragmented across business lines; and senior management and boards had limited visibility into the aggregate model risk their institutions were carrying. Basel II's model-heavy capital framework had inadvertently incentivized model proliferation without a commensurate governance framework to manage the risks.

### 1.2 The OCC's and Fed's Response

The OCC had previously issued guidance on credit scoring models (OCC Bulletin 1997-24) and had incorporated model risk concepts into its examination guidance. But there was no comprehensive, unified framework for managing all model risk. Beginning in 2009, the Fed and OCC engaged jointly to develop comprehensive model risk management guidance that would address the full breadth of the problem — not just credit risk models, not just trading models, but any quantitative tool that a bank relies upon to drive material decisions.

The resulting guidance, issued April 4, 2011, reflected extensive industry consultation and drew on academic literature on model risk, supervisory experience from the crisis, and evolving industry best practices. The Fed issued the guidance as Supervisory Letter SR 11-7; the OCC simultaneously issued OCC Bulletin 2011-12 with substantively identical content, creating a uniform framework applicable to all nationally chartered banks and Federal Reserve-supervised institutions.

---

## 2. The SR 11-7 Definition of "Model"

### 2.1 The Full Verbatim Definition

The definition of "model" is the foundational provision of SR 11-7. It reads, in full:

> **"The term 'model' refers to a quantitative method, system, or approach that applies statistical, economic, financial, or mathematical theories, techniques, and assumptions to process input data into quantitative estimates. A model consists of three components: an information input component, which delivers assumptions and data to the model; a processing component, which transforms inputs into estimates; and a reporting component, which translates the estimates into useful business information. The term 'model' also refers to quantitative approaches whose inputs are partially or wholly qualitative or based on expert judgment, provided that the output is quantitative in nature."**

This definition is notable for several characteristics. It is **technology-neutral**: it captures any quantitative method, system, or approach regardless of the programming language, platform, or technology used to implement it. It is **discipline-neutral**: statistical, economic, financial, and mathematical theories all fall within scope, meaning econometric models, actuarial models, risk models, pricing models, and optimization algorithms are all covered. And it is **output-focused**: the critical test is whether the output is quantitative in nature, even if the inputs involve qualitative judgment or expert opinion.

### 2.2 The Three Components Annotated

SR 11-7 decomposes every model into three structural components:

**Component 1: Information Input.** The information input component delivers assumptions and data to the model. This encompasses raw data (market prices, customer behavioral data, macroeconomic indicators), processed data (engineered features, derived variables), and explicit assumptions about relationships, distributions, or future states. The quality and appropriateness of inputs are the first line of model risk exposure — a technically sophisticated processing component cannot compensate for garbage inputs. SR 11-7 requires that input data be documented, validated for quality and completeness, and assessed for representativeness of the conditions under which the model will be used.

**Component 2: Processing.** The processing component transforms inputs into estimates using the chosen statistical, economic, financial, or mathematical methodology. This is where the model's conceptual logic lives — the calibration of parameters, the estimation of coefficients, the application of the underlying theoretical framework. SR 11-7's emphasis on conceptual soundness is primarily directed at the processing component: examiners assess whether the theory and logic underlying the processing are sound, well-documented, and appropriate for the model's intended use.

**Component 3: Reporting.** The reporting component translates quantitative estimates into actionable business information. A model does not fulfill its purpose by generating a number in isolation — that number must be communicated to model users in a form that supports sound decision-making. The reporting component determines what information is displayed, how uncertainty is communicated, what caveats and limitations are surfaced to users, and how outputs are integrated into business processes. SR 11-7 makes clear that model risk is not confined to the processing component — poor reporting that obscures model uncertainty or presents outputs as more precise than they are constitutes a form of model risk.

### 2.3 Why the Definition Matters

The breadth of the SR 11-7 model definition proved consequential. In the years following issuance, banks inventoried their tools and discovered that SR 11-7's definition captured far more than they had anticipated: spreadsheet-based valuations, end-user computing tools, vendor software using undisclosed algorithms, simple regression-based scorecards, and even some deterministic rule-based systems with statistical parameters were arguable models under the definition. Model inventories at large banks grew to thousands of entries. This created both a compliance challenge (validating thousands of models) and an organizational challenge (finding qualified validators and establishing proportionate governance).

The SR 26-2 revision in April 2026 directly addressed this scope creep by excluding "simple arithmetic calculations, such as those found within spreadsheets, as well as deterministic rule-based processes and software." This narrowing reflects fifteen years of industry feedback and examiner experience showing that SR 11-7's model definition, while appropriately broad in principle, had generated disproportionate compliance burden for low-risk tools.

---

## 3. What Is NOT a Model Under SR 11-7

SR 11-7 acknowledged that not every quantitative tool is a model requiring formal MRM governance. The guidance identified several categories of tools that, while quantitative, do not rise to the level of "model":

**Simple lookups and fixed schedules.** A table that converts a credit score to a risk category using a fixed, deterministic mapping established by policy (not statistical estimation) is not a model. The key distinction is that a lookup table implements a policy decision; a model generates an estimate.

**Pure rule-based systems without statistical estimation.** A system that applies logical rules (if condition A and condition B, then action C) without any statistical parameter estimation or empirical calibration is generally not a model under SR 11-7. However, the boundary is contested: if the rules themselves were derived from or calibrated to statistical analysis, the system may be characterized as implementing a model.

**Human judgment processes.** Purely qualitative assessments relying on expert judgment — a credit officer's narrative assessment of a borrower's management quality, for example — are not models. However, when human judgment is codified into a scoring rubric with quantitative outputs, the resulting system may qualify as a model.

**Simple financial calculations.** Calculations implementing well-established mathematical formulas (such as compound interest, present value of a fixed cash flow, or standard amortization schedules) without estimation components are generally not models. These are implementations of deterministic mathematics, not model outputs.

**Practical boundary challenges.** In practice, the boundary between a model and a non-model tool is rarely sharp. Many systems used in banking blend model components with rule-based logic, human overrides, and deterministic calculations. SR 11-7 required institutions to make reasonable, documented judgments about what falls within scope. Examination findings have included cases where institutions excluded a tool from the model inventory without adequate documentation of the exclusion rationale — a practice examiners view as a governance gap even if the ultimate classification was correct.

SR 26-2 (2026) explicitly codifies the exclusion of simple arithmetic calculations, deterministic tools, and basic spreadsheets, providing regulatory clarity that SR 11-7 lacked. However, this narrowing does not resolve the fundamental challenge of classifying hybrid systems.

---

## 4. Model Risk Taxonomy

SR 11-7 identifies three primary sources of model risk, which together constitute the model risk taxonomy that has become standard across the industry:

### 4.1 Fundamental Model Error

Fundamental model error (sometimes called "conceptual error") arises when the model itself is wrong — when the underlying theory, logic, or methodology is flawed, incorrectly specified, or based on invalid assumptions. This is the most serious form of model risk because it is embedded in the model's design and cannot be fully mitigated by improved implementation or careful use.

Examples of fundamental model error include: a credit scoring model that uses features with spurious correlations to creditworthiness rather than causal drivers; a VaR model that assumes normally distributed returns in a market where returns exhibit fat tails; a prepayment model that embeds assumptions about borrower behavior derived from a period of rising rates when rates are now falling; and a stress-testing model whose macroeconomic scenarios do not adequately capture non-linear tail dynamics.

SR 11-7 requires that **conceptual soundness** be the primary focus of model validation — assessing whether the theory and logic are sound is more important than verifying that the code is correctly implemented. A model that produces correct outputs for the wrong reasons fails the conceptual soundness test even if its back-tests look good.

### 4.2 Model Misuse

Model misuse occurs when a valid, well-designed model is applied in contexts, to populations, or for purposes beyond those for which it was developed and validated. The model itself is not flawed, but its deployment is inappropriate.

Classic examples include: using a credit scoring model developed on prime borrowers to assess subprime applicants; using a short-term VaR model to inform long-horizon strategic decisions; applying a domestic pricing model to assets in foreign markets with different characteristics; and using a model calibrated in low-volatility environments during periods of extreme market stress.

SR 11-7 emphasizes that model users bear as much responsibility for model risk as model developers. The guidance requires that model use be documented, that deviations from intended use be approved and documented, and that ongoing monitoring include assessment of whether models are being used appropriately relative to their validated scope.

### 4.3 Implementation Error

Implementation error arises when a correctly designed model is incorrectly translated into code, a system, or an operational process. The theory may be sound, the intended use may be appropriate, but errors in the implementation mean that the model does not function as designed.

Implementation errors can take many forms: programming errors that cause a model to compute an incorrect result; data mapping errors that feed wrong inputs into the model; parameter calibration errors; spreadsheet formula errors in end-user computing tools; and system integration errors that cause model outputs to be misapplied downstream. Implementation errors are particularly insidious because they may produce plausible-looking outputs that pass naive review.

SR 11-7 requires **process verification** — a component of model validation dedicated to testing whether the model's implementation correctly instantiates the intended methodology. This includes code review, reconciliation of outputs against independent implementations, and systematic testing of edge cases and boundary conditions.

---

## 5. The Three-Tier Governance Framework

SR 11-7 organizes its substantive requirements around three interconnected domains that collectively constitute the MRM framework. While the guidance does not use the explicit language of "three tiers," industry practice has organized SR 11-7 expectations into the following structure:

### Tier 1: Model Development and Implementation

The first tier addresses expectations for how models are built and deployed. SR 11-7 requires:

**Purpose and scope documentation.** Development documentation must clearly articulate the model's purpose, intended use cases, and scope of application. This documentation serves two functions: it constrains model use (preventing misuse) and it provides the foundation for validation.

**Theoretical and methodological rigor.** Developers must document the theoretical basis for the model, the methodological choices made, and why those choices are appropriate for the intended use. Documentation must explore alternative approaches considered and explain why the chosen methodology is preferred. SR 11-7 specifically notes that documentation "should be sufficiently detailed so that parties unfamiliar with a model can understand how the model operates, what it is designed to do, and its limitations."

**Data quality and governance.** The inputs to a model are as important as its processing logic. SR 11-7 requires assessment of data quality, completeness, and relevance; documentation of data transformations and preprocessing; and consideration of whether the data used for model development is representative of the data that will be fed to the model in production. Data lineage — understanding where data originated, how it was processed, and how it arrived at the model — is a SR 11-7 requirement even though the guidance predates the formalization of data lineage as a discipline.

**Testing prior to implementation.** Models must be tested before deployment. SR 11-7 requires testing to include both **developmental testing** (verifying the model performs as intended in the development environment using historical data) and **out-of-sample testing** (assessing performance on data not used in model development). The guidance also expects sensitivity analysis — assessing how model outputs change in response to changes in key inputs and assumptions.

**Documentation for handoff.** Model development documentation must be sufficient to allow validation teams, auditors, and examiners to understand the model without requiring access to the original developers. This is a practical safeguard against key-person dependency and a quality control requirement.

---

### Tier 2: Model Validation

Model validation is the most extensively treated topic in SR 11-7 and the area that received the most examination scrutiny over the guidance's fifteen-year life. The guidance defines validation as "the set of processes and activities intended to verify that models are performing as expected, in line with their design objectives and business uses."

**The core validation framework.** SR 11-7 organizes validation expectations around three activities:

1. **Evaluation of conceptual soundness.** This involves assessing the quality of the model's design, theoretical framework, and empirical evidence supporting the methodology. Validators must evaluate the model's assumptions, assess whether the underlying theory is well-established or empirically validated, and assess whether the chosen methodology is appropriate for the model's intended use. Conceptual soundness review should include examination of developmental evidence — the testing, comparison, and analysis that developers conducted in building the model.

2. **Process verification.** This involves confirming that the model's components function correctly, that data flows into the model appropriately, that calculations produce results consistent with the intended methodology, and that outputs are correctly transmitted to downstream users and systems. Process verification includes testing for implementation errors, validating that model code correctly instantiates the theoretical framework, and checking data quality and completeness.

3. **Outcomes analysis.** This involves comparing model outputs against actual outcomes to assess whether the model predicts or estimates what it claims to predict or estimate. For credit models, this means comparing predicted default rates against observed defaults. For market risk models, this means comparing VaR estimates against observed losses. For pricing models, this means comparing model prices against observed transaction prices. Outcomes analysis includes backtesting (using historical data to assess model performance), benchmarking (comparing the model's outputs against those of alternative models), and sensitivity testing (assessing whether model outputs respond appropriately to changes in inputs).

**Validation independence.** SR 11-7's requirement for **independent** validation is one of its most operationally significant provisions. The guidance requires that validators be "separated from model development functions — whether that separation is within a business line, across business lines, or between the banking organization and an external party." Independence means that validators cannot report to model owners or model development teams; they must have sufficient organizational standing, authority, and resources to raise concerns and escalate findings without facing undue pressure from model owners.

In practice, large banks typically satisfy this requirement through a dedicated Model Risk Management function (sometimes called a Model Validation Group or Independent Validation Unit) that reports to the Chief Risk Officer or directly to the Board Risk Committee, separate from the business lines that own and use models. Smaller banks may use external consultants or third-party validation providers, which satisfy the independence requirement but introduce third-party risk management considerations.

**Proportionality.** SR 11-7 is explicit that "the rigor and sophistication of validation should be commensurate with the bank's overall use of models, the complexity and materiality of its models, and the size and complexity of the bank's operations." This proportionality principle — the foundation of model tiering — means that a mission-critical CCAR stress test model warrants more rigorous and frequent validation than a low-exposure pricing model for a simple product.

**Third-party and vendor models.** SR 11-7 applies the same validation principles to vendor-supplied models as to internally developed models. Banks cannot outsource model risk by purchasing software from vendors. "A banking organization's use of models supplied by vendors or other third parties does not diminish the responsibility of the banking organization's management for the risks associated with those models." In practice, validating vendor models is challenging because vendors frequently provide limited access to source code, training data, and model architecture documentation — a tension that has intensified with the rise of AI platform providers.

---

### Tier 3: Governance, Policies, and Controls

The governance tier addresses the organizational, policy, and oversight framework within which model development and validation occur.

**Board and senior management accountability.** SR 11-7 places accountability for model risk management at the highest organizational levels. The Board of Directors must set and approve model risk appetite, ensure that model risk is adequately resourced, and receive regular reporting on significant model risk. Senior management (including the Chief Risk Officer) is responsible for implementing the Board's risk appetite through policies, procedures, and organizational structures.

**Model risk appetite.** SR 11-7 requires institutions to explicitly establish model risk appetite — a statement of the level and nature of model risk the institution is willing to accept in the pursuit of its business objectives. This concept was radical when introduced in 2011; most banks had credit risk appetite statements and market risk appetite statements but had not articulated model risk appetite. The risk appetite should drive decisions about model tiering, validation frequency, acceptable model limitations, and escalation thresholds.

**Model inventory.** SR 11-7 requires banks to "maintain a comprehensive set of information for models implemented for use, under development for implementation, or recently retired." The model inventory is the foundation of model risk governance — without a complete inventory, no organization can assess its aggregate model risk, allocate validation resources appropriately, or respond to examiner inquiries. SR 11-7 requires the inventory to capture each model's name and description, purpose and use, owner, approval status, known limitations, risk tier, validation history, and outstanding findings.

**Model tiering.** While SR 11-7 does not prescribe a specific tiering system, it requires that governance resources (validation frequency, documentation requirements, oversight intensity) be allocated proportionately to model risk. Industry practice has converged on three to five risk tiers (typically Low, Medium, High, and Critical or Mission-Critical), with tier determined by a combination of factors: the financial materiality of decisions driven by the model, the complexity of the model, the degree of management reliance, the quality of alternatives if the model fails, and the model's regulatory importance.

**Policies and procedures.** The governance framework must include documented policies and procedures covering model development standards, validation requirements, change management (including the threshold for triggering revalidation when a model is modified), model retirement, inventory maintenance, and escalation protocols. Policies must define what constitutes a model (using language consistent with the SR 11-7 definition), specify the organizational roles and responsibilities in model risk management, and establish the approval authority for new models and model changes.

**Model risk committees.** Many large banks have established dedicated Model Risk Committees (MRCs) that serve as the primary governance forum for model risk. Typically chaired by the Chief Risk Officer, an MRC reviews validation findings, approves new models and material model changes, sets model risk appetite parameters, monitors aggregate model risk, and escalates material issues to the Board Risk Committee. MRCs represent an operationalization of SR 11-7's governance requirements and have become a standard organizational feature at systemically important financial institutions (SIFIs).

---

## 6. Conceptual Soundness Requirements

Conceptual soundness is both the most important and the most technically demanding component of model validation under SR 11-7. An examiner assessing conceptual soundness asks the following questions:

**Is the theoretical foundation sound?** Does the model rest on a well-established theoretical framework, or does it rely on empirical correlations without theoretical justification? A credit scoring model that identifies statistically significant predictors of default but cannot articulate why those variables are causally related to creditworthiness may fail the conceptual soundness test. SR 11-7 was written before the widespread adoption of machine learning, but examiners have applied this principle to ML models by asking whether there is a coherent explanation for why the model's features are predictive.

**Are the assumptions reasonable?** Every model embeds assumptions — about the distribution of underlying variables, about the stationarity of relationships, about the behavior of rational actors. SR 11-7 requires that these assumptions be explicitly documented and their reasonableness assessed. Where assumptions are significant, sensitivity analysis should demonstrate how model outputs respond to assumption changes.

**Is the model appropriate for its intended use?** A model may be theoretically sound in general but inappropriate for the specific context in which it is being applied. A model developed on US consumer credit data may be theoretically sound but inappropriate for commercial real estate underwriting; a model calibrated to normal market conditions may be sound but inappropriate for stress-testing applications.

**Is the evidence adequate?** SR 11-7 requires evaluation of "developmental evidence" — the analysis, testing, and comparison that developers conducted in building the model. Validators must assess whether this evidence is sufficient to support the methodology chosen.

**Common examiner findings on conceptual soundness.** Examiners have cited numerous conceptual soundness deficiencies over SR 11-7's history, including: models embedding assumptions that had become stale without documentation of the limitation; regression models with multicollinearity among predictors that was not acknowledged as a limitation; models trained on periods unrepresentative of current conditions (particularly a concern for models trained on pre-crisis data); and discrimination-adjacent features embedded in credit models without adequate business justification.

---

## 7. Data Quality Requirements

SR 11-7 treats data quality as a foundational component of model risk management. Key requirements include:

**Data representativeness.** The data used to develop a model must be representative of the population to which the model will be applied and the conditions under which it will be used. A model developed on prime residential mortgages should not be applied to commercial loans; a model trained on data from 2010–2019 may not be appropriate for a post-pandemic credit environment without recalibration.

**Data completeness.** Missing data is a pervasive challenge in financial models. SR 11-7 requires documentation of how missing data is handled — whether through imputation, exclusion, or other approaches — and assessment of whether the chosen approach introduces bias.

**Data accuracy and integrity.** Input data must be verified for accuracy. The guidance requires procedures for identifying and correcting data errors and for assessing the impact of data errors on model outputs.

**Data lineage.** While SR 11-7 uses this concept rather than the modern terminology of "data lineage," the guidance requires documentation of data sources, transformations, and the process by which raw data arrives at the model. This lineage documentation enables validators and examiners to trace model outputs back to their data origins and assess whether the data is appropriate.

**Ongoing data monitoring.** Data quality obligations do not end at model deployment. SR 11-7 requires ongoing monitoring of data quality — tracking input data distributions over time, identifying data drift (changes in the statistical properties of inputs), and escalating concerns about data quality to model risk governance.

---

## 8. Model Validation Independence

SR 11-7's independence requirement for model validation is one of its most operationally significant and frequently debated provisions. The guidance states:

> **"An effective validation framework must include evaluation by a party that is independent of the model development process."**

**What independence means.** Independence requires that validators have no reporting relationship to the model developers or model owners. It means that validators' compensation and performance assessments are not determined by the business lines whose models they validate. It means validators can escalate concerns and issue negative findings without facing organizational pressure to reach favorable conclusions.

**What independence does not require.** Independence does not require that validators be external to the institution. An internal validation team that reports to the Chief Risk Officer (rather than to the business line or model development team) satisfies the independence requirement. It does not require that validators have no interaction with developers — on the contrary, effective validation typically requires extensive dialogue with developers to understand model design. Independence is about the organizational relationship and authority structure, not about physical or informational separation.

**Organizational structures.** Large banks typically implement independence through dedicated Model Risk Management functions that sit within the Risk division and report to the CRO or Board Risk Committee. These teams employ PhD-level quantitative analysts, statisticians, and domain experts (credit specialists, market risk specialists) who can provide genuine technical challenge to model developers.

**Validator qualifications.** SR 11-7 requires that validators have "expertise equal to or greater than that of the model developers." This creates a talent challenge: the best model developers are highly sought after and may be difficult to retain in a validation function. Banks have addressed this through competitive compensation for validation staff, structured career paths that rotate talent between development and validation, and use of external validators for complex models where internal expertise is limited.

**Challenge to independence in practice.** The most common examiner finding related to independence is not that the validation reporting line is wrong, but that validation teams lack the organizational standing and courage to issue negative findings. SR 11-7's concept of **effective challenge** goes beyond formal independence: it requires that validators actually challenge models rigorously and that their findings carry sufficient authority to drive model changes or usage restrictions. Cosmetic independence — a technically independent team that consistently issues favorable findings to avoid conflict with powerful model owners — violates the spirit of SR 11-7 even if it satisfies its formal requirements.

---

## 9. Ongoing Monitoring

SR 11-7's requirements for ongoing model monitoring address the reality that models are not static: they are deployed into environments that change over time, and a model that performed well at deployment may degrade as conditions evolve. Ongoing monitoring requirements include:

**Performance tracking.** Banks must track key performance metrics for each model on an ongoing basis. For a credit scoring model, this includes the Gini coefficient or AUROC; for a VaR model, exception rates; for a pricing model, bid-ask spreads relative to model prices. Performance tracking enables early detection of model degradation before it produces material business or financial harm.

**Backtesting.** Systematic comparison of model outputs against subsequent realized outcomes. For credit models, backtesting typically involves comparing predicted default probabilities against observed default rates cohort by cohort, over rolling time windows. For market risk models (VaR), backtesting involves counting the number of days actual P&L exceeded the estimated VaR. Backtesting results must be documented and deviations from expected performance investigated.

**Benchmarking.** Comparing a model's outputs against those of challenger models or industry benchmarks. Benchmarking provides a cross-sectional view of model performance and can identify whether a model is systematically biased relative to market consensus.

**Sensitivity testing.** Assessing how model outputs respond to changes in inputs and assumptions over time. As macroeconomic conditions change, it is important to verify that model sensitivities remain consistent with economic intuition.

**Revalidation triggers.** SR 11-7 identifies conditions that should trigger revalidation (a full or partial re-examination of a model even outside the regular validation cycle): significant changes to the model's inputs or methodology; significant changes in the environment in which the model operates (e.g., a regime change in interest rates, credit conditions, or market structure); evidence of material performance degradation; changes in the model's use that extend beyond its original validated scope; and discovery of errors in the model or its implementation.

**Periodic revalidation.** Beyond trigger-based revalidation, SR 11-7 requires that models be periodically reviewed even absent specific triggers. The frequency of periodic revalidation should reflect model materiality: high-risk models at systemically important institutions are typically validated annually; lower-risk models may follow 18-month or 24-month cycles supported by continuous performance monitoring.

---

## 10. Model Risk Governance — Board and Senior Management Roles

SR 11-7 places explicit obligations at the highest levels of bank governance. These obligations distinguish MRM from a purely technical discipline and embed it in the institution's risk culture.

**Board of Directors obligations.** The Board must: approve model risk appetite; ensure adequate resources are devoted to model risk management; receive regular reporting on aggregate model risk; and create a culture in which model limitations are acknowledged and managed rather than hidden. SR 11-7 notes that "the board and senior management play an important role in promoting an enterprise-wide model risk management culture."

**Senior management obligations.** Senior management must: implement Board-approved model risk appetite through policies and procedures; establish and maintain a model inventory; ensure validation is independent; promote effective challenge; and escalate significant model risk issues to the Board. The Chief Risk Officer typically holds primary senior management accountability for model risk.

**Model Risk Committee.** While SR 11-7 does not mandate a dedicated Model Risk Committee, the governance requirements effectively require some form of governance forum at which model risk is discussed, model approvals are considered, and aggregate model risk is monitored. Large banks have universally implemented Model Risk Committees; smaller banks may embed model risk governance within existing risk committees.

**Reporting to the Board.** SR 11-7 requires that senior management "regularly report to the board on significant model risk — both from individual models and from its model risk portfolio — and on the effectiveness of model risk management." Board reporting typically includes an aggregate model risk dashboard showing: number of models by tier; validation coverage and currency; outstanding high-severity findings; model risk appetite utilization; and significant changes in the model landscape (new models deployed, models retired, material model changes).

---

## 11. The Materiality Question and Model Tiering

SR 11-7's proportionality principle requires that governance intensity reflect model materiality, but the guidance does not specify how materiality should be assessed or what tier structure should be used. Over fifteen years, industry practice converged on a generally consistent approach.

**Materiality dimensions.** Banks typically assess model materiality along multiple dimensions:
- **Financial materiality:** The notional size of exposures or decisions driven by the model (e.g., total outstanding balance of loans scored by the model, VaR computed by the market risk model).
- **Decision criticality:** The degree to which business decisions depend on model output. A model whose outputs can be overridden by human judgment at low cost is less critical than a model embedded in an automated decision system.
- **Regulatory importance:** Models used in regulatory capital calculations, CCAR stress tests, or DFAST submissions are inherently high-tier regardless of financial exposure.
- **Model complexity:** More complex models (nonlinear, high-dimensional, using novel techniques) carry greater inherent conceptual error risk and warrant more intensive validation.
- **Data sensitivity:** Models trained on sensitive consumer data, proprietary trading data, or data with limited external validation benchmarks carry higher data risk.

**Typical tier structures.** Most large banks operate a four-tier system:
- **Tier 4 / Critical:** Regulatory capital models (IRB, CCAR), mission-critical pricing models, and other models with institution-wide financial impact. Annual validation required; board-level reporting.
- **Tier 3 / High:** Significant business line models with material financial exposure. Annual validation typical.
- **Tier 2 / Medium:** Models with moderate exposure or complexity. 18–24 month validation cycles.
- **Tier 1 / Low:** Low-exposure or simple models. 24–36 month validation cycles with continuous performance monitoring.

**The FDA analogy.** Regulatory practitioners have drawn an analogy between SR 11-7 model tiering and the FDA's device classification system (Class I, II, III based on risk to public health). The analogy is imperfect but useful: just as the FDA requires more rigorous pre-market review for higher-risk medical devices, SR 11-7 requires more rigorous validation for higher-risk models. And just as the FDA's classification determines the pathway to market clearance, SR 11-7's tiering determines the validation requirements for model deployment.

---

## 12. SR 26-2: The 2026 Revision and What Changed

On April 17, 2026, the Federal Reserve, OCC, and FDIC jointly rescinded SR 11-7 and replaced it with SR 26-2, "Revised Guidance on Model Risk Management." This revision was the most significant update to the US MRM regulatory framework since 2011.

**What SR 26-2 changed:**

| Aspect | SR 11-7 (2011–2026) | SR 26-2 (April 2026 onward) |
|---|---|---|
| Scope | Applied broadly to all supervised institutions | Most relevant to banks >$30bn assets |
| Model definition | Broad — captured spreadsheets and many rule-based tools | Narrower — explicitly excludes simple arithmetic, deterministic rule-based processes |
| Validation independence | Structural independence requirements (reporting lines) | Quality-focused — "rigor and effectiveness rather than organizational structure" |
| Validation frequency | Annual for high-risk models (in practice) | Materiality-based; no default annual requirement |
| GenAI/Agentic AI | Not addressed (emerged post-2011) | Explicitly excluded pending separate rulemaking |
| Compliance signal | Findings ("MRAs") issued for non-compliance | "Non-compliance with this guidance will not result in supervisory criticism" |
| Governance structure | Prescriptive policies and procedures expected | Outcome-based; proportionate to risk profile |
| Third-party models | Same standards as internal models | Same principle maintained; proportionality added |

**What remained constant.** SR 26-2 preserved the core intellectual architecture of SR 11-7: models remain central to bank decision-making and require risk governance; conceptual soundness, process verification, and outcomes analysis remain the three pillars of validation; independent effective challenge remains the gold standard; comprehensive documentation is non-negotiable; and board/senior management accountability for model risk is preserved.

**The GenAI gap.** The explicit exclusion of generative AI and agentic AI from SR 26-2's scope is significant. As large banks deploy LLMs for customer service, credit memo generation, transaction monitoring, and increasingly autonomous decision support, these systems fall outside SR 26-2's formal framework. The agencies have indicated they will issue separate guidance on GenAI governance, and in the interim, banks are applying SR 26-2 principles by analogy. Examiners are already asking about GenAI governance even before formal guidance exists.

---

## 13. SR 11-7 and Machine Learning Models

The arrival of machine learning models in banking operations created genuine tension with SR 11-7's conceptual framework. SR 11-7 was written in an era when "model" meant a statistical regression, a Monte Carlo simulation, or a risk engine — not a neural network with millions of parameters, a gradient boosting ensemble trained on behavioral data, or a natural language model. Key challenges include:

**Conceptual soundness for black boxes.** How can a validator assess the "theoretical and logical soundness" of a deep learning model that learns representations not interpretable in economic terms? Regulators and industry have reached an evolving consensus: conceptual soundness for ML means demonstrating that the features used are relevant and causally connected to the outcome of interest; that the training methodology is statistically sound; that the model has been tested for bias and distributional shift; and that model outputs can be interpreted sufficiently to understand the drivers of individual decisions.

**Explainability as a validation requirement.** SR 11-7's reporting component requirement implicitly demands some level of explainability: model outputs must be communicated to users in a way that supports sound decision-making. Examiners have interpreted this as requiring that model users understand, at a minimum, the key drivers of model outputs. Tools such as SHAP (Shapley Additive Explanations), LIME (Local Interpretable Model-agnostic Explanations), and partial dependence plots have become standard components of ML model validation.

**Ongoing monitoring and drift detection.** ML models are particularly vulnerable to concept drift — changes in the relationship between inputs and outputs as the world evolves — and data drift — changes in the statistical distribution of inputs. The 2021 OCC Handbook added specific expectations for monitoring data drift and model drift for ML models, and SR 26-2 preserves these expectations in its continuous monitoring requirements.

**Third-party ML platforms.** Many banks are using ML capabilities from major technology providers (Amazon SageMaker, Google Vertex AI, Microsoft Azure ML) or AI model providers (foundation model APIs). SR 11-7 and SR 26-2 both require that third-party models be subject to the same governance standards as internal models. Banks have responded by requiring contractual access to model documentation from vendors, conducting challenger model analyses against vendor models, and performing outcome-based monitoring even where they cannot access model internals.

---

## 14. Examiner Expectations and Common MRA/MRIA Findings

Federal Reserve and OCC examiners assessing model risk frameworks under SR 11-7 consistently focused on certain high-priority areas. Understanding examiner expectations is essential to understanding how SR 11-7 was operationalized in practice.

**Model inventory completeness.** Examiners regularly identified model inventories that were incomplete — models used in material business processes that had not been captured in the formal inventory. Particular problem areas included: models embedded in business line spreadsheets (EUC tools); models operated by technology teams without involvement of risk functions; vendor algorithms used in automated decisioning without formal vendor model governance; and "shadow" analytical tools developed by business lines and used informally in decisions.

**Validation documentation quality.** A common MRA was that validation documentation was insufficient to evidence effective challenge. Examiners expected documentation showing that validators had independently assessed conceptual soundness (not merely confirmed what developers said), conducted outcomes analysis with appropriate statistical rigor, and identified and escalated findings. Documentation that reproduced developer analysis without independent assessment was a finding.

**Validation independence deficiencies.** Even where reporting lines appeared independent, examiners found cases where validators were perceived to be reluctant to issue negative findings due to organizational dynamics, compensation structures, or cultural factors. This is the "cosmetic independence" problem — formal independence without effective challenge.

**Ongoing monitoring gaps.** Many banks established robust pre-deployment validation processes but had weak ongoing monitoring. Examiners found models with outdated validations, models whose performance had deteriorated without being re-examined, and models used beyond their originally validated scope without triggering revalidation.

**Third-party model governance.** As vendor models proliferated — particularly credit scoring models, compliance screening tools, and pricing models — examiners found that many banks had applied SR 11-7 governance only to internally developed models. Third-party models without documentation of the vendor's methodology, without independent validation of performance, and without formal approval processes were a common MRA.

**Formal MRA/MRIA designations.** In formal examination reports, model risk deficiencies can be designated as Matters Requiring Attention (MRAs — requiring correction within a defined timeframe) or Matters Requiring Immediate Attention (MRIAs — material weaknesses requiring urgent remediation). MRIAs for model risk have typically been issued when: a bank's model inventory is so incomplete that examiners cannot assess aggregate model risk; a model with critical regulatory capital or CCAR implications is found to have fundamental conceptual errors; or model governance is so weak that examiners have no confidence in the integrity of the bank's quantitative processes.

---

## 15. CFPB Extensions — SR 11-7 Concepts in Consumer Credit

While SR 11-7 is a Federal Reserve/OCC document applicable to bank model governance broadly, the CFPB extended its conceptual framework specifically to consumer credit models through two enforcement-relevant circulars.

**Consumer Financial Protection Circular 2022-03 (May 2022)** addressed adverse action notification requirements when AI/ML models are used in credit decisions. The Equal Credit Opportunity Act (ECOA) and Regulation B require creditors to provide applicants with specific, accurate reasons when credit is denied or terms are adverse. The CFPB stated unambiguously: the complexity of an algorithm does not exempt a creditor from providing specific reasons. A creditor that uses a black-box model and cannot explain its outputs to rejected applicants cannot use that model for consumer credit decisions — regardless of how accurate or sophisticated the model may be.

**Consumer Financial Protection Circular 2023-03 (September 2023)** reinforced these requirements with specific guidance on the proper use of Sample Forms under Regulation B when AI models drive credit decisions. The CFPB clarified that reasons derived from SHAP values, LIME, or similar post-hoc explanation methods are acceptable for adverse action purposes, provided they are accurate and specific enough to be meaningful to a consumer. Generic reasons (e.g., "insufficient credit history") that do not accurately reflect the model's actual decisioning logic are not sufficient.

The CFPB's approach represents a practical extension of SR 11-7's model reporting component requirements into the consumer protection context. Just as SR 11-7 requires that model outputs be communicated to model users in a form that supports sound business decision-making, CFPB's circulars require that model outputs be explainable to the consumers whose financial lives they affect. The CFPB has also emphasized fair lending testing as a model risk management obligation: banks must assess consumer credit AI models for discriminatory effects and document the business justification for all model features.

---

## Cross-References

- [01_regulatory_landscape_overview.md](01_regulatory_landscape_overview.md) — Global regulatory landscape mapping all major MRM regulatory frameworks; provides context for SR 11-7's place in global regulation
- [03_eu_ai_act_finance.md](03_eu_ai_act_finance.md) — EU AI Act obligations for financial services, including comparison of EU and US model governance expectations
- [04_bank_mrm_frameworks.md](04_bank_mrm_frameworks.md) — How major banks have implemented SR 11-7 requirements in practice, including governance structures and validation frameworks
- [06_model_inventory_and_governance_ops.md](06_model_inventory_and_governance_ops.md) — Operational details of model inventory management, tiering methodologies, and governance committee structures
- [07_genai_governance_banking.md](07_genai_governance_banking.md) — GenAI governance frameworks and how SR 26-2's exclusion of GenAI creates a governance gap for banks deploying LLMs
- [12_explainability_fairness_bias.md](12_explainability_fairness_bias.md) — SHAP, LIME, and other explainability tools in the context of SR 11-7 and CFPB adverse action requirements
