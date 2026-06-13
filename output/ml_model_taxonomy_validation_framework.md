# ML Model Taxonomy and Validation Framework
## Traditional Machine Learning Models in Financial Services

**Document Status:** Working Reference  
**Scope:** Traditional ML models used in financial services — excludes Generative AI, LLMs, and Agentic AI  
**Regulatory Alignment:** SR 11-7, SR 26-2, PRA SS1/23, EU AI Act (Annex III), ECOA/Regulation B, CFPB Circular 2022-03  
**Last Updated:** June 2026  
**Related KB Files:** `05_model_validation_methodology.md`, `06_model_inventory_and_governance_ops.md`, `12_explainability_fairness_bias.md`

---

## 1. Purpose and Scope

This document provides:

1. A **taxonomy of ML model categories** used in financial services, with algorithms, use cases, and governance tier
2. A **validation framework** covering all dimensions required by SR 11-7, PRA SS1/23, and the EU AI Act — performance, calibration, conceptual soundness, stability, bias/fairness, explainability, data quality, implementation, robustness, and monitoring
3. A **model-type × validation dimension matrix** showing which metrics apply where
4. A **non-ML reference table** (statistical and mathematical models) for context — these are governed under the same MRM framework but require different validation techniques not covered here

**What this document covers:**  
ML models — those using learning algorithms (logistic regression, tree ensembles, neural networks, SVMs, clustering) trained on data to produce predictions or scores for business decision-making.

**What this document explicitly excludes:**  
- Generative AI / LLMs (ChatGPT-type models, RAG systems, foundation models)
- Agentic AI systems
- Pure mathematical models (Black-Scholes, stochastic differential equations)
- Pure econometric models (VAR, ECM, ARIMA used for macro stress testing)
- IRB/FRTB regulatory capital models (governed under separate Basel III/IV frameworks)

---

## 2. Regulatory Context Summary

All ML models in financial services are subject to model risk governance. The following frameworks are most relevant.

### SR 11-7 / SR 26-2 (US Federal Reserve / OCC)
- Requires **complete model inventory**, risk-based **tiering**, independent **validation**, and ongoing **monitoring**
- Validation must assess: conceptual soundness, data quality, implementation integrity, back-testing, and outcomes analysis
- SR 26-2 (April 2026) adds: evidence as byproduct of development, challenger models as governance artefacts, explicit AI/ML inclusion

### PRA SS1/23 (UK Prudential Regulation Authority)
Five principles every firm must meet:
1. **Governance** — defined roles, three-lines-of-defence, Board-level oversight
2. **Model identification and risk classification** — complete inventory, risk tiering
3. **Model development, implementation and use** — documented methodology, fit-for-purpose data, controlled deployment
4. **Independent model validation** — structural independence, conceptual soundness, performance testing
5. **Model risk mitigants** — compensating controls, limitations register, use-with-exception process

### EU AI Act (Annex III — High-Risk AI)
Applies to ML models used in:
- Credit scoring and creditworthiness assessment → **High-Risk** (Annex III §5b)
- Insurance risk pricing → **High-Risk** (Annex III §5c)
- Employment decisions (where applicable) → High-Risk

EU AI Act obligations for High-Risk systems (enforceable from December 2027):
- **Article 9**: Risk management system throughout lifecycle
- **Article 10**: Data governance — training data quality, representativeness, bias-free
- **Article 13**: Transparency and logging obligations
- **Article 14**: Human oversight measures
- **Article 15**: Accuracy, robustness and cybersecurity requirements
- **Article 72**: Conformity assessment and EU database registration

### ECOA / Regulation B + CFPB Circular 2022-03 (US)
- Adverse action notices required for credit decisions — must state **specific, principal reasons**
- CFPB 2022-03: Complex ML models are not exempt from adverse action reason obligations
- Models must be able to produce human-readable, feature-level reasons for individual decisions

---

## 3. ML Model Categories

> **Boundary note:** The dividing line between "statistical model" and "ML model" is often algorithmic intent and complexity. This taxonomy uses a practical governance lens: ML models are those where a learning algorithm is trained on historical data to optimise a prediction or scoring objective, and where traditional parameter-level interpretability is not directly available without post-hoc explainability tools.

---

### Category 1: Propensity / Selection Models

| Attribute | Detail |
|-----------|--------|
| **What it does** | Scores the probability that a customer will take a desired action — respond to an offer, purchase a product, accept a campaign |
| **Business use** | Campaign targeting, cross-sell / up-sell selection, Next Best Offer (NBO), Next Best Action (NBA), customer segmentation for outreach |
| **Typical algorithms** | Logistic Regression, Gradient Boosted Trees (XGBoost, LightGBM), Random Forest, Neural Networks (shallow MLP) |
| **Output type** | Probability score [0,1] or rank/decile |
| **Decision made** | Who receives an offer / communication; which product to present |
| **Typical governance tier** | Tier 3 (medium) — Tier 2 if population >100K and customer-facing financial decisions |
| **Customer-facing flag** | Yes — directly influences which customers receive which financial product offers |
| **EU AI Act risk level** | Depends on use — credit-related propensity → High Risk |

---

### Category 2: Application / Origination Scorecard Models (ML-based)

| Attribute | Detail |
|-----------|--------|
| **What it does** | Scores creditworthiness of a new applicant at the point of application to support approve/decline and limit decisions |
| **Business use** | Retail loans, credit cards, mortgages, overdrafts, SME lending — point of origination |
| **Typical algorithms** | Gradient Boosted Trees (XGBoost, LightGBM), Random Forest, Logistic Regression with engineered features, Neural Networks |
| **Output type** | Credit score / probability of default [0,1] |
| **Decision made** | Approve / Decline / Refer; credit limit; interest rate band |
| **Typical governance tier** | Tier 1–2 — automatically Tier 2 if >100K customers/year; Tier 1 if regulatory capital feed |
| **Customer-facing flag** | Yes — direct adverse financial impact on customers |
| **EU AI Act risk level** | High Risk (Annex III §5b — creditworthiness assessment) |

---

### Category 3: Behavioural / Account Management Scorecard Models (ML-based)

| Attribute | Detail |
|-----------|--------|
| **What it does** | Scores existing customers on an ongoing basis — probability of default, credit limit eligibility, account risk level |
| **Business use** | Credit limit increases/decreases, account closure triggers, overdraft management, pre-delinquency warning |
| **Typical algorithms** | Gradient Boosted Trees, Random Forest, Logistic Regression, LSTM / sequence models (for temporal transaction features) |
| **Output type** | Probability of default / risk band |
| **Decision made** | Limit change, account action, collections referral |
| **Typical governance tier** | Tier 2 for large retail portfolios |
| **Customer-facing flag** | Yes |
| **EU AI Act risk level** | High Risk (Annex III §5b) |

---

### Category 4: Fraud Detection Models

| Attribute | Detail |
|-----------|--------|
| **What it does** | Detects potentially fraudulent transactions, account activity, or application submissions in real or near-real time |
| **Business use** | Card transaction fraud, CNP (card not present) fraud, wire fraud, application fraud, account takeover |
| **Typical algorithms** | Gradient Boosted Trees (XGBoost), Random Forest, Isolation Forest (unsupervised anomaly), Autoencoder (unsupervised), Graph Neural Networks (GNN), LSTM (sequence models), SVM |
| **Output type** | Binary flag (fraud / not-fraud) or fraud probability score |
| **Decision made** | Block / allow transaction; flag for investigation; step-up authentication |
| **Typical governance tier** | Tier 2 — high volume + customer impact + reputational exposure |
| **Customer-facing flag** | Yes — false positives block legitimate transactions causing customer harm |
| **EU AI Act risk level** | Context-dependent; typically not Annex III unless used for creditworthiness |

---

### Category 5: AML / Financial Crime Models

| Attribute | Detail |
|-----------|--------|
| **What it does** | Detects suspicious patterns of transactions or customer behaviour indicative of money laundering, terrorist financing, or sanctions evasion |
| **Business use** | Transaction monitoring, SAR (Suspicious Activity Report) prioritisation, customer risk rating (KYC), network analysis for crime rings |
| **Typical algorithms** | Unsupervised clustering (k-means, DBSCAN), Graph Neural Networks, Autoencoder (anomaly detection), Random Forest (for SAR prediction), Isolation Forest |
| **Output type** | Alert flag, risk score, network cluster membership |
| **Decision made** | Alert for investigation, SAR filing, account restriction, enhanced due diligence trigger |
| **Typical governance tier** | Tier 2 — regulatory compliance model; AML failures carry severe regulatory consequence |
| **Customer-facing flag** | Indirect — account restrictions affect customers |
| **EU AI Act risk level** | Generally out of Annex III scope but subject to national AML regulation |

---

### Category 6: Customer Churn / Retention Models

| Attribute | Detail |
|-----------|--------|
| **What it does** | Predicts the probability that a customer will close their account, reduce balances, or switch to a competitor within a defined time horizon |
| **Business use** | Retention campaign targeting, relationship manager workload prioritisation, proactive outreach for at-risk customers |
| **Typical algorithms** | Gradient Boosted Trees, Logistic Regression, Random Forest, Survival Analysis (Cox PH with ML features), Neural Networks |
| **Output type** | Churn probability score [0,1]; time-to-churn estimate |
| **Decision made** | Intervention trigger; offer selection for retention |
| **Typical governance tier** | Tier 3–4 (medium to low) |
| **Customer-facing flag** | Indirect |
| **EU AI Act risk level** | Not high-risk under current Annex III |

---

### Category 7: Customer Lifetime Value (CLV) Models

| Attribute | Detail |
|-----------|--------|
| **What it does** | Estimates the total expected revenue or profit contribution of a customer relationship over a defined future horizon |
| **Business use** | Customer acquisition spend optimisation, portfolio segmentation, relationship pricing strategy, resource allocation |
| **Typical algorithms** | Gradient Boosted Trees, Random Forest, Neural Networks, BG/NBD models (probabilistic), Pareto/NBD |
| **Output type** | Continuous value estimate ($) |
| **Decision made** | Acquisition spend threshold; relationship tier assignment; pricing concessions |
| **Typical governance tier** | Tier 3–4 |
| **Customer-facing flag** | Indirect |
| **EU AI Act risk level** | Not high-risk under current Annex III |

---

### Category 8: Collections / Recovery Prioritisation Models

| Attribute | Detail |
|-----------|--------|
| **What it does** | Scores delinquent accounts to prioritise collections effort — who to contact, through which channel, with what offer |
| **Business use** | Delinquency management, settlement offer targeting, write-off timing, recovery rate optimisation |
| **Typical algorithms** | Gradient Boosted Trees, Logistic Regression, Random Forest, Survival Analysis (time to cure) |
| **Output type** | Collections score / probability of cure; settlement acceptance probability |
| **Decision made** | Collections channel, contact frequency, settlement offer, write-off timing |
| **Typical governance tier** | Tier 3 (medium) |
| **Customer-facing flag** | Yes — collections decisions have direct customer impact |
| **EU AI Act risk level** | High Risk if used in debt recovery decisions affecting individuals (Annex III §5b context) |

---

### Category 9: Risk-Based Pricing Models (ML-enhanced)

| Attribute | Detail |
|-----------|--------|
| **What it does** | Determines the interest rate, premium, or fee to offer a specific customer based on their predicted risk and price sensitivity |
| **Business use** | Mortgage rate offers, personal loan pricing, insurance premium calculation, deposit rate optimisation |
| **Typical algorithms** | Gradient Boosted Trees (for risk component), Price Elasticity models (logistic / neural for acceptance probability), Two-stage ML models (risk × acceptance) |
| **Output type** | Recommended rate / price |
| **Decision made** | Price offered to customer |
| **Typical governance tier** | Tier 2 — direct customer financial impact + fair lending / disparate impact exposure |
| **Customer-facing flag** | Yes |
| **EU AI Act risk level** | High Risk (Annex III §5c for insurance; §5b for credit) |

---

### Category 10: NLP / Text Classification Models (Traditional ML — Not LLMs)

| Attribute | Detail |
|-----------|--------|
| **What it does** | Classifies, extracts, or scores text-based inputs — customer communications, regulatory filings, credit memos, complaint analysis |
| **Business use** | Complaint classification and routing, document type classification, credit memo analysis, sentiment scoring of customer communications |
| **Typical algorithms** | TF-IDF + Logistic Regression / SVM, BERT-based fine-tuned classifiers (not GPT-class), fastText, traditional CNNs for text |
| **Output type** | Class label, sentiment score, entity extraction |
| **Decision made** | Routing, triage, flagging for review |
| **Typical governance tier** | Tier 3 (medium) unless driving customer credit decisions |
| **Customer-facing flag** | Depends on use |
| **EU AI Act risk level** | Depends on use — complaint triage: limited; credit decision feed: High Risk |

---

### Category 11: Anomaly Detection / Internal Monitoring Models

| Attribute | Detail |
|-----------|--------|
| **What it does** | Identifies unusual patterns in operational data — trading activity, employee behaviour, system access, model output anomalies |
| **Business use** | Internal fraud, rogue trading detection, operational risk monitoring, model output surveillance |
| **Typical algorithms** | Isolation Forest, Autoencoder, One-Class SVM, DBSCAN, LOF (Local Outlier Factor) |
| **Output type** | Anomaly score; binary flag |
| **Decision made** | Escalate for investigation; flag for human review |
| **Typical governance tier** | Tier 3–4 — not customer-facing |
| **Customer-facing flag** | No |
| **EU AI Act risk level** | Generally not Annex III |

---

## 4. Validation Dimensions Framework

This section defines what must be tested for each validation dimension, the metrics and methods used, the regulatory basis, and applicable thresholds.

---

### 4.1 Discriminatory Power (Performance)

**Regulatory basis:** SR 11-7 §4 "Back-testing and Benchmarking"; SS1/23 Principle 4; EU AI Act Article 15 (accuracy)

**What it measures:** How well the model distinguishes between positive and negative outcomes (defaulters vs. non-defaulters, fraudsters vs. legitimate, churners vs. stayers).

#### Metrics and Thresholds

| Metric | Formula / Method | Thresholds | Best Used For |
|--------|-----------------|------------|---------------|
| **AUC-ROC** | Area under receiver operating characteristic curve | <0.60 Poor · 0.60–0.70 Acceptable · 0.70–0.80 Good · >0.80 Excellent | Binary classification: credit, churn, propensity |
| **Gini Coefficient** | 2 × AUC − 1 | <0.20 Poor · 0.20–0.40 Acceptable · >0.40 Good · >0.60 Excellent | Same as AUC-ROC (linear transformation) |
| **KS Statistic** | Max separation between CDF of positives and negatives | <20% Poor · 20–40% Acceptable · 40–60% Good · >60% Excellent | Credit scorecards; collection models |
| **Lift / Gain** | Actual response rate in decile ÷ overall response rate | Lift >2.0 in top decile (rule of thumb for propensity) | Propensity, marketing selection, collections |
| **Cumulative Gain Chart** | % of positives captured by top N% of population | Top 20% should capture ≥ 40–50% of positives (model-specific) | Campaign planning, collections |
| **Precision** | TP ÷ (TP + FP) | Model and use-case specific | Fraud detection, AML — cost of false positives |
| **Recall (Sensitivity)** | TP ÷ (TP + FN) | Fraud: typically target >80% recall at operational threshold | Fraud detection, AML — cost of false negatives |
| **F1 Score** | 2 × (Precision × Recall) ÷ (Precision + Recall) | Balanced metric when both precision and recall matter | Fraud, AML, NLP classification |
| **Precision@K** | Precision in top K predictions | Benchmark against prior model or business target | Propensity, NBO models |
| **RMSE / MAE / MAPE** | Root mean squared error / Mean absolute error / Mean absolute percentage error | Benchmark-relative (compare to challenger or baseline) | CLV, pricing, regression outputs |

#### Testing Approach
- Evaluate on **out-of-time holdout sample** (not in-sample)
- Use **time-ordered train/test split** — never random split for temporal data
- Assess performance **by segment** (product, geography, vintage, demographic)
- Compare against **challenger model** performance
- Run **k-fold or walk-forward cross-validation** to confirm stability of performance estimates

---

### 4.2 Calibration / Correctness

**Regulatory basis:** SR 11-7 §4 "quantitative comparison of model outputs against actual outcomes"; SS1/23 Principle 4; EU AI Act Article 15

**What it measures:** Whether predicted probabilities accurately reflect true event rates — a model with AUC of 0.80 may still systematically over/under-predict, which matters for capital provisioning, pricing, and downstream model inputs.

#### Metrics and Methods

| Metric | Method | Interpretation | Used For |
|--------|--------|---------------|----------|
| **Hosmer-Lemeshow Test** | Chi-square test comparing observed vs. expected event rates in decile groups | p > 0.05 indicates adequate calibration; p < 0.05 indicates miscalibration | Credit risk, propensity, churn |
| **Binomial Z-test (by grade)** | z = (observed defaults − expected defaults) ÷ σ | \|z\| < 1.96 within 95% CI; \|z\| > 1.96 triggers investigation | IRB-style PD models, IFRS 9 |
| **Brier Score** | Mean squared error of probabilistic predictions | Lower = better; compare against null model (always predict base rate) | All probability-output models |
| **Reliability Diagram** | Plot mean predicted probability vs. observed event rate per bin | Points close to 45° diagonal = well calibrated | All probability-output models |
| **Expected Calibration Error (ECE)** | Weighted average of calibration error per bin | ECE < 0.05 typically considered good | ML models with probability outputs |
| **Log-Loss (Cross-Entropy)** | −[y·log(p) + (1−y)·log(1−p)] | Lower = better; compare against benchmark and challenger | All classification models |
| **Vintage Back-test** | Compare default rates by origination cohort against model predictions | Systematic cohort-level bias indicates drift or recalibration need | Credit, collections |

#### Calibration Correction Methods (if miscalibrated)
- **Platt Scaling** — logistic regression on raw model scores to recalibrate
- **Isotonic Regression** — non-parametric monotone recalibration
- **Beta Calibration** — for binary classifiers
- These are model adjustments, not validation fixes — recalibration must itself be validated

---

### 4.3 Conceptual Soundness

**Regulatory basis:** SR 11-7 §3 "conceptual soundness, including documentation review"; SS1/23 Principle 3 and Principle 4; EU AI Act Article 9 (risk management), Article 13 (transparency)

**What it measures:** Whether the model's design, theoretical foundation, assumptions, and feature selection are grounded in sound theory and business logic — not just statistical signal.

#### Assessment Dimensions

| Dimension | What to Assess | Evidence Required |
|-----------|---------------|-------------------|
| **Theoretical foundation** | Is the model type appropriate for the problem? (e.g., is survival analysis justified for time-to-churn over binary classification?) | Literature review, methodology justification document |
| **Feature economic rationale** | Does each input variable have a plausible economic/business reason to predict the target? | Feature rationale document; SHAP global importance alignment |
| **Direction / monotonicity** | Do features move outputs in the expected direction? (higher debt-to-income → higher PD; not reversed) | SHAP dependence plots; PDP; coefficient sign review |
| **Feature interactions** | Are interaction terms economically meaningful, or spurious statistical artefacts? | SHAP interaction values; domain expert review |
| **Functional form** | Is the relationship between inputs and output modelled at appropriate complexity for the data-generating process? | ALE plots; residual analysis |
| **Scope appropriateness** | Was the model developed on a population comparable to its intended production population? | Population comparison analysis; out-of-scope segment performance |
| **Algorithm choice justification** | Why was XGBoost chosen over logistic regression (or vice versa)? What is the interpretability vs. accuracy trade-off? | Model selection document; champion-challenger comparison |
| **Assumption documentation** | Are all model assumptions explicitly stated and tested? | Assumption register in model documentation |
| **Proxy variable check** | Do any features serve as illegal proxies for protected characteristics (postcode as proxy for race)? | Proxy variable analysis; correlation with protected attributes |
| **Regulatory alignment** | Does the methodology comply with regulatory guidance for this model type? | Regulatory mapping; compliance sign-off |

#### SHAP as a Conceptual Soundness Tool
SHAP global importance and dependence plots are now standard tools for assessing conceptual soundness in ML models:
- **SHAP summary plot** — confirms most important features make business sense
- **SHAP dependence plot** — confirms directionality of feature effects (monotonic where expected)
- **SHAP interaction plot** — identifies feature interactions for reasonableness review
- Unexpected SHAP patterns (a feature pulling in the wrong direction) are a conceptual soundness finding

---

### 4.4 Stability

**Regulatory basis:** SR 11-7 §4 "outcomes analysis including back-testing"; SS1/23 Principle 4 and 5; EU AI Act Article 15 (robustness)

**What it measures:** Whether the model's population, inputs, and performance remain stable over time — detecting data drift, concept drift, and model decay before they cause harm.

#### Stability Metrics

| Metric | Formula | Thresholds | Frequency |
|--------|---------|------------|-----------|
| **PSI (Population Stability Index)** | Σ [(Actual_i − Expected_i) × ln(Actual_i / Expected_i)] | <0.10 Stable · 0.10–0.25 Minor shift, investigate · >0.25 Significant shift, escalate / event-triggered review | Monthly |
| **CSI (Characteristic Stability Index)** | Same as PSI applied to each input variable | Same thresholds as PSI | Monthly |
| **Feature Importance Stability** | SHAP value rank correlation across monitoring periods vs. development | Spearman ρ > 0.80 indicates stable feature importance structure | Quarterly |
| **Rank Order Stability** | Spearman rank correlation of score distribution across time periods | ρ > 0.90 stable; ρ < 0.70 significant re-ranking concern | Monthly |
| **Score Distribution Shift** | KL Divergence or Wasserstein distance between reference and monitoring score distribution | Benchmark-relative; calibrate threshold from historical monitoring | Monthly |
| **Vintage Analysis** | Default / event rates by origination cohort against model-predicted rates | Systematic cohort deviation >20% relative = escalation trigger | Quarterly |
| **Roll Rate Stability** | % of accounts rolling from DPD30 → DPD60 → DPD90 vs. historical pattern | Institution-specific thresholds; 30% relative change = review | Monthly |

#### Types of Drift (MUST distinguish)

| Drift Type | Definition | Detection Method | Response |
|-----------|-----------|-----------------|----------|
| **Covariate / Data Drift** | Input feature distributions change; underlying relationship stable | CSI on individual features | Recalibration may suffice |
| **Concept Drift** | Underlying relationship between inputs and target changes (e.g., income became less predictive post-COVID) | Performance metric deterioration despite stable inputs | Model redevelopment required |
| **Label Drift** | Target variable definition or measurement changes | Outcome rate analysis; label distribution monitoring | Root cause investigation |
| **Prediction Drift** | Score distribution shifts without corresponding outcome shift | PSI + outcome lag analysis | Investigate data pipeline first |

---

### 4.5 Bias and Fairness

**Regulatory basis:** ECOA / Regulation B (US); FCA Fair Treatment of Customers (UK); EU AI Act Article 10 (data representativeness), Article 9 (risk management for bias); EU GDPR Article 22; SS1/23 Principle 3 (appropriate model use)

**What it measures:** Whether the model produces systematically different outcomes for legally protected groups (race, gender, age, national origin, disability, religion) or proxies thereof — creating disparate impact even if the model does not explicitly use protected attributes.

#### IBM AIF360 Metrics (Primary Bias Measurement Library)

| Metric | Formula | Threshold / Interpretation | Regulatory Basis |
|--------|---------|---------------------------|-----------------|
| **Statistical Parity Difference (SPD)** | P(Ŷ=1 \| A=unprivileged) − P(Ŷ=1 \| A=privileged) | SPD = 0 is perfectly fair; \|SPD\| < 0.05 typically acceptable; \|SPD\| > 0.10 requires investigation | ECOA; EU AI Act Art. 10 |
| **Disparate Impact Ratio (DIR)** | P(Ŷ=1 \| A=unprivileged) ÷ P(Ŷ=1 \| A=privileged) | 4/5 rule (EEOC / CFPB): DIR ≥ 0.80 required; DIR < 0.80 = evidence of disparate impact | ECOA Reg B; CFPB fair lending guidance |
| **Equal Opportunity Difference (EOD)** | TPR(unprivileged) − TPR(privileged) | \|EOD\| < 0.05 typically acceptable | Equal opportunity fairness definition |
| **Average Odds Difference (AOD)** | ½ × [(FPR(unpriv) − FPR(priv)) + (TPR(unpriv) − TPR(priv))] | \|AOD\| < 0.05 acceptable; captures both FPR and TPR disparity | Equalized odds fairness |
| **Theil Index** | Individual fairness measure; entropy-based decomposition | Lower = more fair; benchmark against pre-mitigation value | Individual fairness |
| **Between-Group Generalized Entropy Error (BGEE)** | Generalised entropy of prediction errors between groups | Lower = more equal error distribution across groups | Group fairness |

#### Fairness Testing Protocol

**Step 1 — Identify Protected Attributes and Proxies**
- Direct protected attributes (if available and legally permitted to test): race, gender, age, national origin
- **Proxy variables** (more common): postcode/zip code, surname, device type, browsing behaviour — test correlation with protected attributes
- Remove or control for proxies that serve as illegal discriminators

**Step 2 — Pre-Mitigation Analysis**
- Compute all AIF360 metrics on development and out-of-time samples
- Document baseline bias levels before any mitigation
- Identify which specific features drive disparate impact (SHAP disaggregated by group)

**Step 3 — Apply Mitigation If Required**

| Mitigation Stage | Method | When to Apply |
|-----------------|--------|--------------|
| **Pre-processing** | Reweighing (AIF360), Disparate Impact Remover, Learning Fair Representations | When training data itself is biased |
| **In-processing** | Adversarial debiasing, Prejudice Remover (Fairness-aware learning) | When bias is embedded in the learning process |
| **Post-processing** | Equalised Odds Post-processing, Reject Option Classification | When model is fixed but outputs need adjustment |

**Step 4 — Post-Mitigation Validation**
- Re-run all AIF360 metrics; confirm improvement
- Confirm acceptable performance trade-off (fairness-accuracy trade-off must be explicitly documented and justified)
- Perform **intersectional analysis** (age × gender; race × postcode) not just single-axis

**Step 5 — Adverse Action Compliance (Credit Models)**
- For any adverse credit decision, model must produce **principal reasons** per CFPB Circular 2022-03
- SHAP values should be mapped to consumer-readable reason codes
- Validate reason code stability: the same score should produce consistent reasons across similar profiles

---

### 4.6 Explainability (XAI)

**Regulatory basis:** CFPB Circular 2022-03 (adverse action reasons); EU AI Act Article 13 (transparency); SS1/23 Principle 4; FCA Consumer Duty (UK); SR 11-7 (conceptual soundness requires ability to explain)

**What it measures:** Whether model decisions can be explained at both global level (how the model works overall) and local level (why a specific decision was made for a specific customer).

#### Explainability Methods

| Method | Type | What It Provides | Limitations |
|--------|------|-----------------|-------------|
| **SHAP (Shapley Additive Explanations)** | Post-hoc, model-agnostic | Additive decomposition of each prediction into feature contributions; global + local | Computationally intensive; approximate for large models; can be unstable |
| **LIME (Local Interpretable Model-agnostic Explanations)** | Post-hoc, local only | Fits simple interpretable model locally around prediction | Local approximation only; unstable across similar instances |
| **Partial Dependence Plots (PDP)** | Global, marginal effect | Shows how model prediction changes as one feature varies, holding others constant | Assumes feature independence; misleading under strong correlations |
| **Accumulated Local Effects (ALE)** | Global, marginal effect | Better than PDP under feature correlation; computes local derivatives | Less intuitive to communicate |
| **Permutation Feature Importance** | Global | Measures drop in performance when feature values are randomly permuted | Does not show direction; affected by correlated features |
| **Decision Tree Surrogate** | Global, post-hoc | Fits simple decision tree to model outputs for approximate global explanation | Surrogate ≠ actual model; complexity vs. accuracy trade-off |
| **Integrated Gradients** | Post-hoc (neural nets) | Gradient-based attribution for deep learning models | Neural network-specific |

#### Validation Requirements for Explainability

| Test | Method | Pass Criteria |
|------|--------|--------------|
| **SHAP stability** | Run SHAP across multiple holdout samples; compute rank correlation of feature importances | Spearman ρ > 0.85 across samples indicates stable explanations |
| **SHAP sign consistency** | Check that SHAP direction aligns with expected business logic for all top features | No material sign contradictions for top 5 features |
| **Local explanation consistency** | Run LIME/SHAP for the same individual across multiple runs | Same top 3 features with consistent direction |
| **Adverse action reason mapping** | Map SHAP values to consumer-readable reason codes | Each adverse decision must produce ≥ 4 principal reasons (US ECOA standard) |
| **Explainability audit trail** | Log SHAP values per decision for sample of production decisions | 12-month retention; reproducible on regulatory request |

---

### 4.7 Data Quality

**Regulatory basis:** SR 11-7 §4 "sound data practices and data quality"; SS1/23 Principle 3; EU AI Act Article 10 (training data governance)

**Framework: DQICAR**

| Dimension | Metric / Test | Threshold |
|-----------|--------------|-----------|
| **Completeness** | Missing value rate per feature | <5% per feature for training data; document imputation method if >1% |
| **Accuracy** | Cross-validation against authoritative source (credit bureau, core banking) | <2% discrepancy rate on key fields |
| **Consistency** | Format and definition consistency across time periods and data sources | Zero tolerance for redefinition of target variable across time |
| **Relevance** | Information Value (IV) for binary classification features | IV < 0.02: Useless · 0.02–0.10: Weak · 0.10–0.30: Medium · >0.30: Strong |
| **Timeliness** | Data lag analysis — time between event and data availability in production | Confirm lag at training matches lag in production (no lag leakage) |

#### Additional ML-Specific Data Tests

| Test | What It Detects |
|------|----------------|
| **Data Leakage Test** | Features that would not be available at the time of prediction (look-ahead bias). Test: AUC collapses significantly when time-ordering is enforced → leakage likely |
| **Training Set Representativeness** | Whether training data represents the current and expected future production population. Use PSI between training data and recent production population |
| **Class Imbalance Assessment** | Severe imbalance (e.g., 0.1% fraud rate) affects model calibration. Document SMOTE, ADASYN, or class weighting mitigation |
| **Feature Correlation Analysis** | High pairwise correlation (ρ > 0.85) indicates redundancy and potential instability. VIF > 10 indicates problematic multicollinearity |
| **Outlier Assessment** | Univariate: IQR method, z-score. Multivariate: Isolation Forest, Mahalanobis Distance. Document treatment |
| **Data Lineage Documentation** | Source → transformation → model input. Required by EU AI Act Article 10 and SR 26-2 |

---

### 4.8 Implementation Soundness

**Regulatory basis:** SR 11-7 §3 "validation should encompass all components of a model including implementation"; SS1/23 Principle 3

**What it measures:** Whether the model as coded accurately reflects the model as designed, and whether it will operate correctly in the production environment.

#### Implementation Review Checklist

| Review Area | What to Check | Method |
|-------------|--------------|--------|
| **Code vs. specification** | Implementation accurately reflects methodology documentation | Line-by-line code walkthrough against mathematical spec |
| **Reproducibility** | Same inputs produce same outputs across runs | Fixed random seeds; locked dependency versions; containerised environment |
| **Data leakage in code** | No future data in training pipeline; feature engineering uses only past information | Review pipeline code; test AUC drop on temporally-ordered data |
| **Edge case handling** | Nulls, zeros, negatives, extreme values handled correctly without crashing | Unit test with boundary inputs |
| **Transformation consistency** | Same transformations (scaling, encoding, imputation) applied identically in training and production | Compare training pipeline code vs. production scoring code |
| **Version control** | Code and training data version documented and reproducible | Git commit hash; MLflow run ID; data version tag |
| **Environment parity** | Development, testing, and production environments are identical in material respects | Environment manifest; Docker image hash |
| **Library version locking** | Dependencies (scikit-learn, XGBoost, etc.) pinned to specific versions | requirements.txt / conda environment file version-pinned |
| **Unit test coverage** | Key functions have unit tests | Minimum 80% coverage for Tier 1/2 models |
| **Performance in production** | Model meets latency and throughput requirements | Load test results; p99 latency benchmark |

---

### 4.9 Robustness and Stress Testing

**Regulatory basis:** SR 11-7 §4 "sensitivity analysis"; SS1/23 Principle 4; EU AI Act Article 15 (robustness and cybersecurity)

**What it measures:** Model performance under adverse or unexpected conditions — distributional shift, adversarial inputs, extreme scenarios, and sub-population edge cases.

#### Robustness Tests

| Test | Method | What It Reveals | Pass Criteria |
|------|--------|----------------|--------------|
| **Input perturbation sensitivity** | Systematically vary each input ±10%, ±20%, ±50%; measure output change | Whether model is excessively sensitive to minor input variations | No >20% output change for ±10% input change in key features |
| **Feature removal test** | Retrain / re-score without each top-5 feature in turn | Feature dependency concentration risk | Top-1 feature should not account for >40% of predictive power |
| **Adversarial input testing** | Feed deliberately manipulated inputs designed to fool the model | Model vulnerability to gaming / manipulation | Flag where small deliberate changes produce large score jumps |
| **Out-of-distribution testing** | Apply model to population outside its development scope | Performance degradation at population edges | Document performance and apply scope restriction |
| **Stress period performance** | Back-test on historical stress periods (GFC 2008, COVID 2020) | Performance during economic stress | Assess direction of performance change; update monitoring thresholds |
| **Sub-population analysis** | Disaggregate performance by key segments (product, geography, vintage, income band) | Segments where model underperforms | Segment-level AUC/KS must exceed model-wide minimum |
| **SHAP stability under perturbation** | Perturb training data; re-run SHAP; compare feature importance ranks | Explanation stability | Spearman ρ > 0.80 on top-10 feature rankings |

---

### 4.10 Ongoing Monitoring Requirements

**Regulatory basis:** SR 11-7 §4 "ongoing monitoring"; SS1/23 Principle 5; EU AI Act Article 9 (lifecycle risk management); SR 26-2 (continuous evidence generation)

**What it monitors:** Model performance in production after approval — detecting deterioration before it causes harm.

#### Monitoring Framework

| Metric Category | Metric | Frequency | Escalation Trigger |
|----------------|--------|-----------|-------------------|
| **Score distribution** | PSI on output scores | Monthly | PSI > 0.25 → event-triggered review |
| **Input stability** | CSI on each input feature | Monthly | CSI > 0.25 on any feature → investigate |
| **Performance** | AUC-ROC / Gini / KS (where outcomes available) | Quarterly | Gini drops >5 percentage points → investigation; >10pp → mandatory revalidation |
| **Calibration** | Observed event rate vs. predicted (by score band) | Quarterly | >20% relative miscalibration → recalibration required |
| **Fairness** | Disparate Impact Ratio by protected group | Quarterly | DIR drops below 0.80 → immediate escalation to compliance |
| **Business KPIs** | Approval rate, bad rate, response rate (by product) | Monthly | >15% relative change from baseline → investigate |
| **Feature importance** | SHAP feature rank correlation vs. development | Quarterly | Spearman ρ < 0.80 → conceptual soundness review |
| **Volume** | Scoring volume vs. approved scope | Monthly | Volume <50% or >200% of approved scope → tier and use review |

#### Event-Triggered Revalidation Criteria

Any of the following requires a mandatory revalidation outside the scheduled cycle:
- PSI > 0.25 sustained over two consecutive monitoring periods
- Gini / AUC-ROC drops >10 percentage points from validation benchmark
- Disparate Impact Ratio falls below 0.80
- Material change in model use, population, or business context
- Significant change in regulatory requirements applicable to this model type
- Discovery of data quality failure affecting model inputs
- Material model incident (production error, customer harm, regulatory citation)

---

## 5. Model-Type × Validation Dimension Matrix

The following matrix shows which validation dimensions are **Primary (P)**, **Secondary (S)**, or **Not Applicable (—)** for each model category. Primary dimensions must be fully executed for every validation of that model type. Secondary dimensions should be executed unless justified scope limitation is documented.

| Validation Dimension | Propensity | App Scorecard | Behav Scorecard | Fraud | AML | Churn | CLV | Collections | Pricing | NLP/Text | Anomaly |
|---------------------|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Discriminatory Power** (AUC/Gini/KS) | P | P | P | P | P | P | S | P | S | P | S |
| **Lift / Gain** | P | P | P | P | S | P | — | P | S | — | — |
| **Precision / Recall / F1** | S | S | S | P | P | S | — | S | — | P | P |
| **RMSE / MAE** | — | — | — | — | — | S | P | — | P | — | — |
| **Calibration (HL / Brier)** | P | P | P | S | — | P | — | P | S | — | — |
| **Reliability Diagram / ECE** | S | P | P | S | — | S | — | S | S | — | — |
| **Conceptual Soundness** | P | P | P | P | P | P | P | P | P | P | P |
| **PSI (Score Stability)** | P | P | P | P | P | P | S | P | P | S | S |
| **CSI (Feature Stability)** | P | P | P | P | P | S | S | P | P | S | — |
| **Vintage / Roll Rate Analysis** | — | P | P | — | — | — | — | P | — | — | — |
| **Bias — Disparate Impact (DIR)** | P | P | P | S | S | — | — | P | P | — | — |
| **Bias — IBM AIF360 Metrics** | S | P | P | S | S | — | — | S | P | — | — |
| **Adverse Action Reason Codes** | — | P | P | — | — | — | — | S | S | — | — |
| **SHAP (Global)** | P | P | P | P | S | P | P | P | P | S | — |
| **SHAP (Local / per-decision)** | S | P | P | P | — | S | — | S | P | — | — |
| **LIME** | S | S | S | S | — | S | S | S | S | S | — |
| **PDP / ALE Plots** | S | P | P | S | — | S | S | S | P | — | — |
| **Data Quality (DQICAR)** | P | P | P | P | P | P | P | P | P | P | P |
| **Leakage / Look-ahead Test** | P | P | P | P | P | P | P | P | P | P | P |
| **Implementation Review** | P | P | P | P | P | S | S | S | P | S | S |
| **Reproducibility** | P | P | P | P | P | P | P | P | P | P | S |
| **Input Perturbation** | S | P | P | P | S | S | — | S | P | — | S |
| **Adversarial Testing** | — | S | S | P | P | — | — | — | — | S | S |
| **Sub-population Robustness** | P | P | P | P | P | S | S | S | P | S | — |
| **Stress Period Back-test** | S | P | P | S | — | S | S | S | S | — | — |
| **Ongoing Monitoring (PSI/CSI)** | P | P | P | P | P | P | S | P | P | S | P |
| **Challenger Model** | S | P | P | P | S | S | — | S | P | S | — |

**P** = Primary — must be executed; **S** = Secondary — execute unless scope justified; **—** = Not Applicable

---

## 6. Findings Classification

All validation findings must be classified per the following taxonomy (consistent with SR 11-7 and SS1/23 Principle 4):

| Severity | Definition | Model Status | Examples |
|----------|-----------|--------------|---------|
| **Critical** | Fundamental deficiency preventing safe model use | Not Approved — model cannot be deployed | Data leakage; material conceptual flaw; regulatory non-compliance; discriminatory output exceeding legal threshold |
| **Major** | Significant deficiency materially affecting reliability | Approved with Conditions — compensating controls required | Calibration bias (known, controllable); performance weakness in specific segment; missing challenger documentation; DIR between 0.70–0.80 |
| **Minor** | Non-material deficiency in documentation or practice | Approved — remediation plan required | Incomplete assumption documentation; CSI borderline (0.10–0.15); monitoring frequency below policy minimum |

**Critical finding examples specific to ML models:**
- Data leakage confirmed (AUC collapses >15pp when look-ahead removed)
- DIR < 0.70 for a protected class in a credit decision model — exceeds legal threshold
- Model producing negative SHAP values for features that should positively predict outcome, with no business explanation
- Training data confirmed to exclude a material demographic segment that the model is deployed on

---

## 7. Non-ML Statistical and Mathematical Models — Reference Table

> **Purpose:** For context and completeness only. These model types are governed under the same MRM framework (SR 11-7, SS1/23) but require different validation techniques primarily drawn from classical statistics, econometrics, and mathematical finance. They are not covered in depth in this document.

| Model Type | Primary Algorithms | Validation Approach | Tier |
|-----------|-------------------|--------------------|----|
| **IRB PD Models** | Logistic Regression, Probit, Cox Proportional Hazards | Binomial back-test, HL test, grade-level calibration, Spearman rank, traffic light | **Tier 1** (automatic) |
| **IRB LGD Models** | Beta Regression, Tobit Regression, Two-stage Heckman | Back-test of realised LGD vs. predicted; downturn analysis; facility-type segmentation | **Tier 1** (automatic) |
| **IRB EAD Models** | OLS, Tobit, CCF Regression | Back-test CCF; exposure profile analysis | **Tier 1** (automatic) |
| **IFRS 9 / CECL ECL** | Logistic regression (PiT PD) + macro overlay | Stage migration accuracy; provision back-test; scenario coherence; macro sensitivity | **Tier 1–2** |
| **CCAR / DFAST Stress** | OLS Panel Regression, VAR, ARIMAX | Historical stress period back-test; scenario coherence; sensitivity to macro variables | **Tier 1** (automatic) |
| **Market Risk VaR / ES** | Historical Simulation, Parametric, Monte Carlo | Kupiec back-test; traffic light (Basel); P&L Attribution Test (FRTB) | **Tier 1** (automatic) |
| **Option Pricing** | Black-Scholes, Binomial Tree, Heston | Market price comparison; Greek stability; day-1 P&L | **Tier 1** |
| **Interest Rate Models** | Hull-White, Vasicek, LMM (SOFR) | Calibration to market instruments; scenario analysis; historical period comparison | **Tier 1** |
| **Operational Risk Capital** | Loss Distribution Approach (LDA), EVT | EVT parameter stability; external data blending; scenario analysis | **Tier 1** |

**Further reading:** `05_model_validation_methodology.md` Sections 7–8 cover traditional back-testing in detail. `02_sr11_7_deep_dive.md` covers the regulatory capital model governance requirements.

---

## 8. Quick Reference — Threshold Summary

| Metric | Poor | Acceptable | Good | Excellent |
|--------|------|-----------|------|-----------|
| AUC-ROC | < 0.60 | 0.60–0.70 | 0.70–0.80 | > 0.80 |
| Gini Coefficient | < 0.20 | 0.20–0.40 | 0.40–0.60 | > 0.60 |
| KS Statistic | < 20% | 20–40% | 40–60% | > 60% |
| PSI (stability) | > 0.25 (action) | 0.10–0.25 (monitor) | < 0.10 (stable) | — |
| Disparate Impact Ratio | < 0.70 (critical) | 0.70–0.80 (major finding) | > 0.80 (compliant) | > 0.90 (no issue) |
| Statistical Parity Diff | > ±0.15 | ±0.10–0.15 | ±0.05–0.10 | < ±0.05 |
| Information Value (IV) | < 0.02 (useless) | 0.02–0.10 (weak) | 0.10–0.30 (medium) | > 0.30 (strong) |
| VIF (multicollinearity) | > 10 (high) | 5–10 (moderate) | < 5 (acceptable) | < 2 (ideal) |
| SHAP rank correlation | < 0.70 (unstable) | 0.70–0.80 (borderline) | 0.80–0.90 (stable) | > 0.90 (very stable) |
| F1 Score | Benchmark-relative — compare against challenger and baseline; no universal threshold | | | |
| Brier Score | Benchmark-relative — compare against null model (always predict base rate) | | | |

---

## 9. Regulatory Mapping — Which Regulation Requires What

| Validation Dimension | SR 11-7 | SR 26-2 | SS1/23 | EU AI Act | ECOA/Reg B |
|---------------------|---------|---------|--------|-----------|-----------|
| Conceptual Soundness | §3 | §3 | Principle 4 | Art. 9, 13 | — |
| Data Quality | §3 | §3 | Principle 3 | Art. 10 | — |
| Implementation Review | §3 | §3 | Principle 3 | Art. 15 | — |
| Back-testing / Performance | §4 | §4 | Principle 4 | Art. 15 | — |
| Challenger Model | §4 | §4 (mandatory artefact) | Principle 4 | — | — |
| Ongoing Monitoring | §4 | §4 | Principle 5 | Art. 9 | — |
| Bias / Disparate Impact | — | Implied | Principle 3 | Art. 10 | Direct requirement |
| Adverse Action Reasons | — | — | — | Art. 13 | Direct requirement |
| Explainability (SHAP/LIME) | Implied (soundness) | Explicit | Principle 4 | Art. 13 | CFPB 2022-03 |
| Human Oversight | — | — | Principle 1 | Art. 14 | — |
| Risk Tiering | §3 | §3 | Principle 2 | Art. 9 | — |
| Documentation | §3 | §3 | All Principles | Art. 11 | — |

---

*Sources: Federal Reserve SR 11-7 (April 2011); SR 26-2 Revised Interagency Guidance (April 2026); PRA Supervisory Statement SS1/23 (May 2023); EU AI Act (Regulation 2024/1689, June 2024); CFPB Circular 2022-03; ECOA / Regulation B (12 CFR Part 202); IBM AIF360 documentation (v2.0, 2024); SHAP library documentation (Lundberg & Lee, 2017–2024); MRM KB files 05, 06, 12.*
