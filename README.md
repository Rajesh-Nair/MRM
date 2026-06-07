# Model Risk Management (MRM) Knowledge Base

## 1. Knowledge Base Declaration

This knowledge base covers **AI/ML Model Risk Management (MRM) and Governance** in financial services, with a particular focus on how major global banks operationalise MRM, the regulatory frameworks that govern it, and the specific challenges posed by Generative AI, LLMs, and autonomous agentic AI systems. It spans traditional statistical model governance (credit scorecards, VaR models, IFRS 9 ECL) and the frontier challenges of 2025–2027 (foundation model risk, agentic AI, synthetic data, federated learning). It does **not** cover general machine learning engineering, model training techniques, or non-financial-services AI applications except where they directly inform financial services governance.

**Last reviewed:** June 2026 | **Primary audience:** MRM practitioners, risk officers, AI governance teams, regulators, and researchers.

**AI Agent Note:** Use the File Registry (Section 3) and Cross-Index (Section 5) for fast topic lookup. Use Section 6 for abbreviation resolution. The Coverage Gaps Log (Section 7) identifies what is not present — do not confabulate content for listed gaps.

---

## 2. File Quicklook for Agents

> **Agents:** Scan the "Answers" column below to find the ONE file that addresses your question. Then read only that file. Do not open multiple files. For a full topic → file mapping, see the **Cross-Index of Key Topics** section below.

| File | Answers questions about… |
|------|--------------------------|
| [01](research/01_regulatory_landscape_overview.md) | Which countries regulate model risk, what each regulator requires, compliance timelines, binding vs. guidance, and open regulatory questions (SR 26-2, MAS, FCA, EBA, BCBS, HKMA, FINMA) |
| [02](research/02_sr11_7_deep_dive.md) | What SR 11-7 and its 2026 replacement SR 26-2 actually say: model definition (verbatim), what is/is not a model, three-tier governance framework, validation independence, model tiering, examiner expectations, MRA patterns |
| [03](research/03_eu_ai_act_finance.md) | EU AI Act obligations for banks and insurers: which financial AI systems are high-risk (Annex III), what Articles 9-15 require, GPAI rules, conformity assessment, DORA/GDPR interaction, Dec 2027 compliance deadline, penalties |
| [04](research/04_bank_mrm_frameworks.md) | How JPMorgan, Goldman Sachs, HSBC, Citi, Wells Fargo, Barclays, Deutsche Bank, UBS, BNP, Morgan Stanley structure MRM: three lines of defense, model lifecycle, approval tiering, Model Risk Committees, consent order case studies |
| [05](research/05_model_validation_methodology.md) | Model validation methods: conceptual soundness, back-testing, benchmarking, AUC/KS/PSI thresholds, ML black-box validation (SHAP/LIME in validation), LLM validation (red-teaming, hallucination testing), findings taxonomy (Critical/Major/Minor), challenger models |
| [06](research/06_model_inventory_and_governance_ops.md) | Model inventory field schema, materiality tiering criteria, risk appetite statements, Model Risk Committee charter, shadow model detection, vendor model governance, MRM platforms (IBM OpenPages, SAS, Wolters Kluwer, ValidMind), IRB/IFRS 9/CECL/FRTB governance |
| [07](research/07_genai_governance_banking.md) | Why SR 11-7 is insufficient for LLMs, how banks extend MRM for Gen AI, the "is a prompt a model?" debate, how JPMorgan/Goldman/HSBC/Morgan Stanley govern LLMs, five-tier Gen AI categorization, regulatory expectations for Gen AI, third-party LLM vendor risk |
| [08](research/08_llm_risk_taxonomy.md) | Complete LLM risk catalog: 33 risks across Model Risk (hallucination, prompt sensitivity, version drift), Data Risk (PII memorization, RAG poisoning), Operational Risk (API dependency, jailbreaking), Conduct Risk (discriminatory outputs, ECOA violation); heat map; OWASP LLM mapping |
| [09](research/09_agentic_ai_governance.md) | Governing autonomous AI agents: what distinguishes agents from LLMs, nine agentic risk types, when HITL is mandatory, kill switch design, agent identity/credentialing, audit trail logging requirements, SR 26-2 "agent as model?" question, Singapore's 2026 agentic framework |
| [10](research/10_industry_frameworks_nist_iso.md) | NIST AI RMF (all GOVERN/MAP/MEASURE/MANAGE subcategories), ISO 42001:2023 (clauses and Annex A controls), OECD AI Principles (2024 revision), G7 Hiroshima Code of Conduct, COBIT for AI, IEEE 7001/7010, SR 11-7 ↔ NIST mapping table, adoption by jurisdiction |
| [11](research/11_big_tech_mrm_guidance.md) | IBM (AIF360, UQ360, watsonx.governance, IBM breach report data), Google (Model Cards, Vertex AI explainability/monitoring), Microsoft (Responsible AI Standard, Fairlearn, Azure ML Monitor, Copilot governance), AWS (SageMaker Clarify bias metrics, Model Monitor, Bedrock Guardrails), Anthropic (Constitutional AI, Model Spec, RSP, agentic principles) |
| [12](research/12_explainability_fairness_bias.md) | ECOA adverse action compliance for ML, GDPR Art 22, LIME/SHAP/counterfactuals (technical), fairness impossibility theorems (Chouldechova, Kleinberg), disparate impact 4/5 rule, six bias types, de-biasing (pre/in/post-processing), Apple Card case study, CFPB enforcement |
| [13](research/13_model_drift_monitoring_mlops.md) | PSI/CSI/KL/Wasserstein metrics and thresholds, five drift types (covariate/concept/label/prediction/attribution), MLOps for regulated banks (audit trails, approval gates, rollback), champion-challenger patterns, LLM production monitoring, Evidently/WhyLabs/Arize tooling, model decommissioning |
| [14](research/14_mrm_maturity_and_emerging_topics.md) | 5-level MRM maturity model (Level 1 Ad Hoc → Level 5 Optimizing), convergence of MRM and AI governance programs, synthetic data governance, LoRA fine-tuning risk, federated learning governance, systemic AI risk (Flash Crash analog), adversarial attacks, regulatory horizon 2025-2028 |
| [S1](standards/owasp_top10_llm.md) | OWASP Top 10 for LLM Applications 2025: prompt injection, sensitive data disclosure, supply chain, data poisoning, improper output handling, excessive agency, system prompt leakage, vector weaknesses, misinformation, unbounded consumption |
| [S2](standards/owasp_top10_agentic.md) | OWASP Top 10 for Agentic AI 2026: agent goal hijack, tool misuse, identity/privilege abuse, agentic supply chain, unexpected code execution, memory/context poisoning, insecure inter-agent communication, cascading failure, human-agent trust exploitation, rogue agents |
| [S3](standards/ibm_cost_of_data_breach_2025.md) | IBM/Ponemon 2025 breach report: $5.56M avg cost in financial services, shadow AI $670K premium, 97% of AI breaches lacked access controls, 63% of organizations lack AI governance policies, 16% of breaches AI-driven |

---

## 3. Directory Map

```
MRM/
├── README.md                                   ← This file — navigation hub
│
├── research/                                   ← 14 deep-research topic files
│   ├── 01_regulatory_landscape_overview.md     ← Global MRM regulation across 10+ jurisdictions
│   ├── 02_sr11_7_deep_dive.md                  ← SR 11-7 / SR 26-2: foundational US MRM framework
│   ├── 03_eu_ai_act_finance.md                 ← EU AI Act obligations for financial services
│   ├── 04_bank_mrm_frameworks.md               ← How major banks structure MRM governance
│   ├── 05_model_validation_methodology.md      ← Model validation craft: traditional, ML, LLM
│   ├── 06_model_inventory_and_governance_ops.md← Model inventories, tiering, MRC operations
│   ├── 07_genai_governance_banking.md          ← Extending MRM for Gen AI / LLMs at banks
│   ├── 08_llm_risk_taxonomy.md                 ← 33-risk four-dimension LLM risk taxonomy
│   ├── 09_agentic_ai_governance.md             ← Autonomous agent governance framework
│   ├── 10_industry_frameworks_nist_iso.md      ← NIST AI RMF, ISO 42001, OECD AI Principles
│   ├── 11_big_tech_mrm_guidance.md             ← IBM, Google, Microsoft, AWS, Anthropic guidance
│   ├── 12_explainability_fairness_bias.md      ← XAI, fairness definitions, bias testing
│   ├── 13_model_drift_monitoring_mlops.md      ← Drift types, PSI/CSI, MLOps, decommissioning
│   └── 14_mrm_maturity_and_emerging_topics.md  ← Maturity model, convergence, emerging topics
│
├── standards/                                  ← Security and standards reference files
│   ├── owasp_top10_llm.md                      ← OWASP Top 10 for LLM Applications (2025)
│   ├── owasp_top10_agentic.md                  ← OWASP Top 10 for Agentic AI (2026)
│   └── ibm_cost_of_data_breach_2025.md         ← IBM/Ponemon Cost of Data Breach 2025 — full summary
│
└── downloads/
    └── cost-of-a-data-breach-2025-full-report.pdf  ← IBM Cost of Data Breach 2025 (source PDF)
```

---

## 4. File Registry

| # | File | Cluster | Primary Topic | Key Regulators/Bodies | Reading Order |
|---|------|---------|--------------|----------------------|---------------|
| 01 | [01_regulatory_landscape_overview.md](research/01_regulatory_landscape_overview.md) | A — Regulatory Foundations | Global MRM regulation map: US, EU, UK, APAC | Fed, OCC, EBA, FCA, PRA, MAS, FINMA, HKMA, BCBS | 1/14 |
| 02 | [02_sr11_7_deep_dive.md](research/02_sr11_7_deep_dive.md) | A — Regulatory Foundations | SR 11-7 and SR 26-2 deep analysis | Federal Reserve, OCC, CFPB | 2/14 |
| 03 | [03_eu_ai_act_finance.md](research/03_eu_ai_act_finance.md) | A — Regulatory Foundations | EU AI Act for financial services | EU Commission, EBA, ECB, EIOPA, EU AI Office | 3/14 |
| 04 | [04_bank_mrm_frameworks.md](research/04_bank_mrm_frameworks.md) | B — Bank Practice | MRM governance at major global banks | Fed, OCC, PRA, ECB/SSM, FINMA | 4/14 |
| 05 | [05_model_validation_methodology.md](research/05_model_validation_methodology.md) | B — Bank Practice | Validation methodology: statistical, ML, LLM | Federal Reserve (SR 11-7), OCC, BCBS | 5/14 |
| 06 | [06_model_inventory_and_governance_ops.md](research/06_model_inventory_and_governance_ops.md) | B — Bank Practice | Model inventories, tiering, MRC, shadow models | Fed (SR 11-7/SR 26-2), OCC, BCBS, IFRS/FASB | 6/14 |
| 07 | [07_genai_governance_banking.md](research/07_genai_governance_banking.md) | C — Gen AI & LLM Governance | Extending MRM for Gen AI at banks | Fed, OCC, FCA, ECB, MAS, BIS, FSB | 7/14 |
| 08 | [08_llm_risk_taxonomy.md](research/08_llm_risk_taxonomy.md) | C — Gen AI & LLM Governance | 33-risk LLM taxonomy (Model/Data/Ops/Conduct) | Fed, OCC, FCA, CFPB, BCBS, FSB, NIST | 8/14 |
| 09 | [09_agentic_ai_governance.md](research/09_agentic_ai_governance.md) | C — Gen AI & LLM Governance | Autonomous agent governance framework | Fed, OCC, MAS, FCA, PRA, EBA, ECB, NIST | 9/14 |
| 10 | [10_industry_frameworks_nist_iso.md](research/10_industry_frameworks_nist_iso.md) | D — Industry Frameworks | NIST AI RMF, ISO 42001, OECD, COBIT, IEEE | NIST, ISO, OECD, G7/G20, ISACA, IEEE | 10/14 |
| 11 | [11_big_tech_mrm_guidance.md](research/11_big_tech_mrm_guidance.md) | D — Industry Frameworks | IBM, Google, Microsoft, AWS, Anthropic guidance | NIST (via vendors), ISO, EU AI Act | 11/14 |
| 12 | [12_explainability_fairness_bias.md](research/12_explainability_fairness_bias.md) | E — Technical Risk Topics | XAI (LIME/SHAP), fairness definitions, bias testing | CFPB, Fed, OCC, FFIEC, FCA, EU Commission, HUD | 12/14 |
| 13 | [13_model_drift_monitoring_mlops.md](research/13_model_drift_monitoring_mlops.md) | E — Technical Risk Topics | Drift types, PSI/CSI, MLOps, LLM monitoring | Federal Reserve (SR 11-7/SR 26-2), OCC, BCBS | 13/14 |
| 14 | [14_mrm_maturity_and_emerging_topics.md](research/14_mrm_maturity_and_emerging_topics.md) | F — Synthesis | Maturity model, convergence, emerging topics | Fed, OCC, FSB, BCBS, SEC, CFTC, FCA, EU | 14/14 |

### Standards / Reference Files

| File | Contents |
|------|----------|
| [standards/owasp_top10_llm.md](standards/owasp_top10_llm.md) | OWASP Top 10 for LLM Applications 2025 — security risks with mitigations |
| [standards/owasp_top10_agentic.md](standards/owasp_top10_agentic.md) | OWASP Top 10 for Agentic AI 2026 — agent-specific security risks |
| [standards/ibm_cost_of_data_breach_2025.md](standards/ibm_cost_of_data_breach_2025.md) | IBM/Ponemon Cost of Data Breach Report 2025 — full structured summary with financial services data |

---

## 5. Persona-Based Reading Paths

### Path A: Regulatory Practitioner (Compliance Officer, MRM Officer, Regulator)

Goal: Understand the regulatory environment, your obligations, and how leading banks meet them.

1. **[01_regulatory_landscape_overview.md](research/01_regulatory_landscape_overview.md)** — Start here to map your jurisdiction's requirements
2. **[02_sr11_7_deep_dive.md](research/02_sr11_7_deep_dive.md)** — Deep-dive into the foundational US framework (and its 2026 replacement SR 26-2)
3. **[03_eu_ai_act_finance.md](research/03_eu_ai_act_finance.md)** — If operating in the EU, understand your AI Act obligations
4. **[04_bank_mrm_frameworks.md](research/04_bank_mrm_frameworks.md)** — See how industry peers implement MRM governance
5. **[06_model_inventory_and_governance_ops.md](research/06_model_inventory_and_governance_ops.md)** — Understand inventory, tiering, and committee mechanics
6. **[07_genai_governance_banking.md](research/07_genai_governance_banking.md)** — Apply traditional MRM to Gen AI
7. **[10_industry_frameworks_nist_iso.md](research/10_industry_frameworks_nist_iso.md)** — Voluntary frameworks that may satisfy or complement regulatory requirements
8. **[14_mrm_maturity_and_emerging_topics.md](research/14_mrm_maturity_and_emerging_topics.md)** — Where the regulatory horizon is heading

### Path B: Technical Practitioner (Model Validator, Data Scientist, ML Engineer)

Goal: Understand validation methodology, technical risk, and production operations.

1. **[05_model_validation_methodology.md](research/05_model_validation_methodology.md)** — Validation craft: the how-to
2. **[08_llm_risk_taxonomy.md](research/08_llm_risk_taxonomy.md)** — The 33-risk LLM risk catalog
3. **[12_explainability_fairness_bias.md](research/12_explainability_fairness_bias.md)** — LIME, SHAP, fairness metrics, bias testing
4. **[13_model_drift_monitoring_mlops.md](research/13_model_drift_monitoring_mlops.md)** — PSI/CSI, MLOps pipelines, LLM monitoring
5. **[09_agentic_ai_governance.md](research/09_agentic_ai_governance.md)** — Agent governance: HITL, kill switches, audit trails
6. **[11_big_tech_mrm_guidance.md](research/11_big_tech_mrm_guidance.md)** — IBM AIF360, SageMaker Clarify, Fairlearn, Vertex AI tooling
7. **[14_mrm_maturity_and_emerging_topics.md](research/14_mrm_maturity_and_emerging_topics.md)** — Emerging technical topics (synthetic data, federated learning, adversarial robustness)

### Path C: Executive / Strategic Reader (CRO, CAIO, Board Member)

Goal: Understand the landscape and strategic implications without deep technical detail.

1. **[01_regulatory_landscape_overview.md](research/01_regulatory_landscape_overview.md)** — Regulatory obligations at a glance
2. **[04_bank_mrm_frameworks.md](research/04_bank_mrm_frameworks.md)** — How peer banks are structured
3. **[07_genai_governance_banking.md](research/07_genai_governance_banking.md)** — The Gen AI governance challenge
4. **[09_agentic_ai_governance.md](research/09_agentic_ai_governance.md)** — The agentic AI risk frontier
5. **[10_industry_frameworks_nist_iso.md](research/10_industry_frameworks_nist_iso.md)** — Available frameworks to adopt
6. **[14_mrm_maturity_and_emerging_topics.md](research/14_mrm_maturity_and_emerging_topics.md)** — Maturity benchmarking and strategic horizon

### Path D: Security / Red Team Focus

Goal: Understand the security attack surface of financial AI systems.

1. **[08_llm_risk_taxonomy.md](research/08_llm_risk_taxonomy.md)** — LLM risk catalog including operational/adversarial risks
2. **[09_agentic_ai_governance.md](research/09_agentic_ai_governance.md)** — Agentic AI attack surface and controls
3. **[standards/owasp_top10_llm.md](standards/owasp_top10_llm.md)** — OWASP LLM Top 10 (prompt injection, supply chain, etc.)
4. **[standards/owasp_top10_agentic.md](standards/owasp_top10_agentic.md)** — OWASP Agentic Top 10 (goal hijacking, tool misuse, etc.)
5. **[11_big_tech_mrm_guidance.md](research/11_big_tech_mrm_guidance.md)** — Vendor security controls (Bedrock Guardrails, Azure AI Content Safety)
6. **[13_model_drift_monitoring_mlops.md](research/13_model_drift_monitoring_mlops.md)** — Adversarial monitoring and anomaly detection
7. **[standards/ibm_cost_of_data_breach_2025.md](standards/ibm_cost_of_data_breach_2025.md)** — Breach cost data and AI-specific attack vectors

---

## 6. Cross-Index of Key Topics

Use this index to find where a topic is covered. Format: **Topic** → primary file(s), with secondary files in parentheses.

| Topic | Primary File(s) | Also in |
|-------|----------------|---------|
| Adverse Action (ECOA) | [12](research/12_explainability_fairness_bias.md) | [08](research/08_llm_risk_taxonomy.md) |
| Agentic AI — governance | [09](research/09_agentic_ai_governance.md) | [07](research/07_genai_governance_banking.md), [14](research/14_mrm_maturity_and_emerging_topics.md) |
| Agentic AI — OWASP risks | [standards/owasp_top10_agentic.md](standards/owasp_top10_agentic.md) | [09](research/09_agentic_ai_governance.md) |
| AI Act (EU) | [03](research/03_eu_ai_act_finance.md) | [01](research/01_regulatory_landscape_overview.md), [07](research/07_genai_governance_banking.md) |
| AI Fairness 360 (IBM) | [11](research/11_big_tech_mrm_guidance.md) | [12](research/12_explainability_fairness_bias.md) |
| Anthropic / Claude | [11](research/11_big_tech_mrm_guidance.md) | [09](research/09_agentic_ai_governance.md) |
| Audit Trails (AI agents) | [09](research/09_agentic_ai_governance.md) | — |
| AWS SageMaker (Clarify / Monitor) | [11](research/11_big_tech_mrm_guidance.md) | [13](research/13_model_drift_monitoring_mlops.md) |
| Back-testing | [05](research/05_model_validation_methodology.md) | [13](research/13_model_drift_monitoring_mlops.md) |
| Bank of America | [04](research/04_bank_mrm_frameworks.md) | [07](research/07_genai_governance_banking.md) |
| Barclays | [04](research/04_bank_mrm_frameworks.md) | — |
| Basel / BCBS | [01](research/01_regulatory_landscape_overview.md) | [06](research/06_model_inventory_and_governance_ops.md) |
| Bias — types | [12](research/12_explainability_fairness_bias.md) | [08](research/08_llm_risk_taxonomy.md) |
| Bias — de-biasing techniques | [12](research/12_explainability_fairness_bias.md) | [11](research/11_big_tech_mrm_guidance.md) |
| Black-box validation | [05](research/05_model_validation_methodology.md) | [12](research/12_explainability_fairness_bias.md) |
| CCAR / DFAST | [06](research/06_model_inventory_and_governance_ops.md) | [14](research/14_mrm_maturity_and_emerging_topics.md) |
| CECL | [06](research/06_model_inventory_and_governance_ops.md) | — |
| Challenger Model | [05](research/05_model_validation_methodology.md) | [13](research/13_model_drift_monitoring_mlops.md) |
| Champion-Challenger | [13](research/13_model_drift_monitoring_mlops.md) | [05](research/05_model_validation_methodology.md) |
| Citigroup | [04](research/04_bank_mrm_frameworks.md) | [07](research/07_genai_governance_banking.md) |
| COBIT for AI | [10](research/10_industry_frameworks_nist_iso.md) | — |
| Concept Drift | [13](research/13_model_drift_monitoring_mlops.md) | — |
| Conformity Assessment (EU AI Act) | [03](research/03_eu_ai_act_finance.md) | — |
| Constitutional AI (Anthropic) | [11](research/11_big_tech_mrm_guidance.md) | [09](research/09_agentic_ai_governance.md) |
| Consent Orders (Wells Fargo, Citi) | [04](research/04_bank_mrm_frameworks.md) | [06](research/06_model_inventory_and_governance_ops.md) |
| Counterfactual Explanations | [12](research/12_explainability_fairness_bias.md) | — |
| Covariate Shift | [13](research/13_model_drift_monitoring_mlops.md) | — |
| Credit Scoring — AI Act classification | [03](research/03_eu_ai_act_finance.md) | [12](research/12_explainability_fairness_bias.md) |
| CSI (Characteristic Stability Index) | [13](research/13_model_drift_monitoring_mlops.md) | [05](research/05_model_validation_methodology.md) |
| Data Breach (IBM 2025 Report) | [standards/ibm_cost_of_data_breach_2025.md](standards/ibm_cost_of_data_breach_2025.md) | [11](research/11_big_tech_mrm_guidance.md) |
| Data Governance (for models) | [06](research/06_model_inventory_and_governance_ops.md) | [05](research/05_model_validation_methodology.md) |
| Decommissioning (model) | [13](research/13_model_drift_monitoring_mlops.md) | [06](research/06_model_inventory_and_governance_ops.md) |
| Demographic Parity | [12](research/12_explainability_fairness_bias.md) | — |
| Deutsche Bank / TRIM | [04](research/04_bank_mrm_frameworks.md) | [01](research/01_regulatory_landscape_overview.md) |
| Disparate Impact Testing | [12](research/12_explainability_fairness_bias.md) | [08](research/08_llm_risk_taxonomy.md) |
| DORA (EU) | [03](research/03_eu_ai_act_finance.md) | [01](research/01_regulatory_landscape_overview.md) |
| EBA (European Banking Authority) | [01](research/01_regulatory_landscape_overview.md) | [03](research/03_eu_ai_act_finance.md) |
| ECB / TRIM | [01](research/01_regulatory_landscape_overview.md) | [04](research/04_bank_mrm_frameworks.md) |
| ECOA / Regulation B | [12](research/12_explainability_fairness_bias.md) | [08](research/08_llm_risk_taxonomy.md) |
| Equalized Odds | [12](research/12_explainability_fairness_bias.md) | — |
| EU AI Act | [03](research/03_eu_ai_act_finance.md) | [01](research/01_regulatory_landscape_overview.md) |
| Evidently AI | [13](research/13_model_drift_monitoring_mlops.md) | — |
| Explainability (XAI) | [12](research/12_explainability_fairness_bias.md) | [05](research/05_model_validation_methodology.md), [11](research/11_big_tech_mrm_guidance.md) |
| Fairlearn (Microsoft) | [11](research/11_big_tech_mrm_guidance.md) | [12](research/12_explainability_fairness_bias.md) |
| FCA (UK) | [01](research/01_regulatory_landscape_overview.md) | [03](research/03_eu_ai_act_finance.md) |
| FEAT Principles (MAS) | [01](research/01_regulatory_landscape_overview.md) | — |
| Federated Learning | [14](research/14_mrm_maturity_and_emerging_topics.md) | — |
| Fine-tuning (LoRA/QLoRA) risk | [14](research/14_mrm_maturity_and_emerging_topics.md) | [08](research/08_llm_risk_taxonomy.md) |
| FINMA (Switzerland) | [01](research/01_regulatory_landscape_overview.md) | [04](research/04_bank_mrm_frameworks.md) |
| Foundation Model risk | [07](research/07_genai_governance_banking.md) | [08](research/08_llm_risk_taxonomy.md) |
| FRTB | [06](research/06_model_inventory_and_governance_ops.md) | — |
| GDPR Article 22 | [03](research/03_eu_ai_act_finance.md) | [12](research/12_explainability_fairness_bias.md) |
| Goldman Sachs | [04](research/04_bank_mrm_frameworks.md) | [07](research/07_genai_governance_banking.md) |
| Google — Model Cards / Vertex AI | [11](research/11_big_tech_mrm_guidance.md) | — |
| GPAI (General Purpose AI) | [03](research/03_eu_ai_act_finance.md) | [07](research/07_genai_governance_banking.md) |
| Hallucination | [07](research/07_genai_governance_banking.md) | [08](research/08_llm_risk_taxonomy.md) |
| HKMA (Hong Kong) | [01](research/01_regulatory_landscape_overview.md) | — |
| HSBC | [04](research/04_bank_mrm_frameworks.md) | [07](research/07_genai_governance_banking.md) |
| Human-in-the-Loop (HITL) | [09](research/09_agentic_ai_governance.md) | [07](research/07_genai_governance_banking.md) |
| IBM OpenPages / watsonx.governance | [11](research/11_big_tech_mrm_guidance.md) | [06](research/06_model_inventory_and_governance_ops.md) |
| IBM Cost of Data Breach 2025 | [standards/ibm_cost_of_data_breach_2025.md](standards/ibm_cost_of_data_breach_2025.md) | [11](research/11_big_tech_mrm_guidance.md) |
| IFRS 9 (ECL models) | [06](research/06_model_inventory_and_governance_ops.md) | — |
| Integrated Gradients | [12](research/12_explainability_fairness_bias.md) | [11](research/11_big_tech_mrm_guidance.md) |
| IRB (Internal Ratings-Based) models | [06](research/06_model_inventory_and_governance_ops.md) | [01](research/01_regulatory_landscape_overview.md) |
| ISO 42001 | [10](research/10_industry_frameworks_nist_iso.md) | — |
| JPMorgan Chase | [04](research/04_bank_mrm_frameworks.md) | [07](research/07_genai_governance_banking.md) |
| Kill Switch (agent) | [09](research/09_agentic_ai_governance.md) | — |
| KL Divergence | [13](research/13_model_drift_monitoring_mlops.md) | — |
| LLM risk taxonomy | [08](research/08_llm_risk_taxonomy.md) | [07](research/07_genai_governance_banking.md) |
| LLM validation | [05](research/05_model_validation_methodology.md) | [08](research/08_llm_risk_taxonomy.md) |
| LIME | [12](research/12_explainability_fairness_bias.md) | [05](research/05_model_validation_methodology.md) |
| MAS (Singapore) | [01](research/01_regulatory_landscape_overview.md) | [09](research/09_agentic_ai_governance.md) |
| Microsoft — Responsible AI / Fairlearn | [11](research/11_big_tech_mrm_guidance.md) | [12](research/12_explainability_fairness_bias.md) |
| MLflow | [13](research/13_model_drift_monitoring_mlops.md) | [06](research/06_model_inventory_and_governance_ops.md) |
| MLOps | [13](research/13_model_drift_monitoring_mlops.md) | [06](research/06_model_inventory_and_governance_ops.md) |
| Model Cards (Google) | [11](research/11_big_tech_mrm_guidance.md) | — |
| Model Definition (SR 11-7) | [02](research/02_sr11_7_deep_dive.md) | [07](research/07_genai_governance_banking.md) |
| Model Inventory | [06](research/06_model_inventory_and_governance_ops.md) | [04](research/04_bank_mrm_frameworks.md) |
| Model Materiality / Tiering | [06](research/06_model_inventory_and_governance_ops.md) | [04](research/04_bank_mrm_frameworks.md) |
| Model Risk Committee (MRC) | [06](research/06_model_inventory_and_governance_ops.md) | [04](research/04_bank_mrm_frameworks.md) |
| Morgan Stanley | [04](research/04_bank_mrm_frameworks.md) | [07](research/07_genai_governance_banking.md) |
| MRM Maturity Model | [14](research/14_mrm_maturity_and_emerging_topics.md) | — |
| Multi-agent orchestration | [09](research/09_agentic_ai_governance.md) | [08](research/08_llm_risk_taxonomy.md) |
| Multi-modal model risk | [14](research/14_mrm_maturity_and_emerging_topics.md) | — |
| NIST AI RMF | [10](research/10_industry_frameworks_nist_iso.md) | [11](research/11_big_tech_mrm_guidance.md) |
| NIST AI 600-1 (GenAI Profile) | [10](research/10_industry_frameworks_nist_iso.md) | — |
| OCC | [02](research/02_sr11_7_deep_dive.md) | [01](research/01_regulatory_landscape_overview.md) |
| OECD AI Principles | [10](research/10_industry_frameworks_nist_iso.md) | — |
| OWASP LLM Top 10 | [standards/owasp_top10_llm.md](standards/owasp_top10_llm.md) | [08](research/08_llm_risk_taxonomy.md) |
| OWASP Agentic Top 10 | [standards/owasp_top10_agentic.md](standards/owasp_top10_agentic.md) | [09](research/09_agentic_ai_governance.md) |
| PII Memorization (LLMs) | [08](research/08_llm_risk_taxonomy.md) | — |
| PRA SS1/23 (UK) | [01](research/01_regulatory_landscape_overview.md) | [04](research/04_bank_mrm_frameworks.md) |
| Prompt Injection | [08](research/08_llm_risk_taxonomy.md) | [standards/owasp_top10_llm.md](standards/owasp_top10_llm.md) |
| PSI (Population Stability Index) | [13](research/13_model_drift_monitoring_mlops.md) | [05](research/05_model_validation_methodology.md) |
| RAG (Retrieval-Augmented Generation) | [07](research/07_genai_governance_banking.md) | [08](research/08_llm_risk_taxonomy.md) |
| Responsible Scaling Policy (Anthropic) | [11](research/11_big_tech_mrm_guidance.md) | — |
| Shadow Models | [06](research/06_model_inventory_and_governance_ops.md) | [04](research/04_bank_mrm_frameworks.md) |
| SHAP | [12](research/12_explainability_fairness_bias.md) | [05](research/05_model_validation_methodology.md), [11](research/11_big_tech_mrm_guidance.md) |
| SR 11-7 | [02](research/02_sr11_7_deep_dive.md) | [01](research/01_regulatory_landscape_overview.md), [04](research/04_bank_mrm_frameworks.md), [06](research/06_model_inventory_and_governance_ops.md), [07](research/07_genai_governance_banking.md) |
| SR 26-2 (2026 revision) | [02](research/02_sr11_7_deep_dive.md) | [01](research/01_regulatory_landscape_overview.md), [07](research/07_genai_governance_banking.md) |
| Synthetic Data Governance | [14](research/14_mrm_maturity_and_emerging_topics.md) | — |
| Systemic AI Risk | [14](research/14_mrm_maturity_and_emerging_topics.md) | [08](research/08_llm_risk_taxonomy.md) |
| Three Lines of Defense | [04](research/04_bank_mrm_frameworks.md) | [02](research/02_sr11_7_deep_dive.md) |
| TRIM (ECB) | [01](research/01_regulatory_landscape_overview.md) | [04](research/04_bank_mrm_frameworks.md) |
| UBS | [04](research/04_bank_mrm_frameworks.md) | — |
| Vendor Models (third-party AI) | [06](research/06_model_inventory_and_governance_ops.md) | [07](research/07_genai_governance_banking.md) |
| Vertex AI (Google) | [11](research/11_big_tech_mrm_guidance.md) | — |
| VaR Models | [02](research/02_sr11_7_deep_dive.md) | [05](research/05_model_validation_methodology.md) |
| Wasserstein Distance | [13](research/13_model_drift_monitoring_mlops.md) | — |
| Wells Fargo (consent order) | [04](research/04_bank_mrm_frameworks.md) | [06](research/06_model_inventory_and_governance_ops.md) |
| WhyLabs | [13](research/13_model_drift_monitoring_mlops.md) | — |
| XAI (Explainable AI) | [12](research/12_explainability_fairness_bias.md) | [05](research/05_model_validation_methodology.md) |

---

## 7. Abbreviations and Glossary

| Abbreviation | Full Term |
|-------------|-----------|
| AIF360 | IBM AI Fairness 360 (open-source bias toolkit) |
| AML | Anti-Money Laundering |
| APRA | Australian Prudential Regulation Authority |
| ASL | AI Safety Level (Anthropic's Responsible Scaling Policy framework) |
| AUC-ROC | Area Under the Receiver Operating Characteristic Curve |
| BCBS | Basel Committee on Banking Supervision |
| BIS | Bank for International Settlements |
| CCAR | Comprehensive Capital Analysis and Review (US stress testing) |
| CECL | Current Expected Credit Losses (US GAAP) |
| CFPB | Consumer Financial Protection Bureau |
| CPS/CPG | Capital / Credit Prudential Standard/Guidance (APRA) |
| CRO | Chief Risk Officer |
| CSI | Characteristic Stability Index |
| DFAST | Dodd-Frank Act Stress Tests |
| DORA | Digital Operational Resilience Act (EU) |
| EBA | European Banking Authority |
| ECB | European Central Bank |
| ECOA | Equal Credit Opportunity Act (US) |
| ECL | Expected Credit Loss |
| EIOPA | European Insurance and Occupational Pensions Authority |
| ERM | Enterprise Risk Management |
| ESG | Environmental, Social, and Governance |
| FEAT | Fairness, Ethics, Accountability, Transparency (MAS Singapore) |
| FDIC | Federal Deposit Insurance Corporation |
| FSB | Financial Stability Board |
| FRTB | Fundamental Review of the Trading Book (Basel) |
| GDPR | General Data Protection Regulation (EU) |
| Gini | Gini Coefficient (model discrimination metric) |
| GPAI | General Purpose AI (EU AI Act Title VIII) |
| G-SIB | Global Systemically Important Bank |
| HITL | Human-in-the-Loop |
| HKMA | Hong Kong Monetary Authority |
| HMDA | Home Mortgage Disclosure Act (US) |
| HOTL | Human-on-the-Loop |
| HUD | US Department of Housing and Urban Development |
| IBM | International Business Machines Corporation |
| IFRS 9 | International Financial Reporting Standard 9 (expected credit losses) |
| IRB | Internal Ratings-Based approach (Basel credit risk capital) |
| ISO | International Organization for Standardization |
| KL | Kullback-Leibler divergence |
| KPI | Key Performance Indicator |
| KRI | Key Risk Indicator |
| KS | Kolmogorov-Smirnov statistic |
| LIME | Local Interpretable Model-Agnostic Explanations |
| LLM | Large Language Model |
| LoRA | Low-Rank Adaptation (ML fine-tuning technique) |
| MAS | Monetary Authority of Singapore |
| MLOps | Machine Learning Operations |
| MRA | Matter Requiring Attention (US regulatory finding) |
| MRAA | Matter Requiring Immediate Attention |
| MRC | Model Risk Committee |
| MRM | Model Risk Management |
| MVU | Model Validation Unit |
| NLP | Natural Language Processing |
| NIST | National Institute of Standards and Technology |
| OCC | Office of the Comptroller of the Currency |
| OECD | Organisation for Economic Co-operation and Development |
| OWASP | Open Web Application Security Project |
| PEFT | Parameter-Efficient Fine-Tuning |
| PII | Personally Identifiable Information |
| PRA | Prudential Regulation Authority (UK) |
| PSI | Population Stability Index |
| QLoRA | Quantized Low-Rank Adaptation |
| RAG | Retrieval-Augmented Generation |
| RCSA | Risk and Control Self-Assessment |
| RWA | Risk-Weighted Assets |
| SHAP | SHapley Additive exPlanations |
| SM&CR | Senior Managers and Certification Regime (UK FCA/PRA) |
| SR 11-7 | Federal Reserve Supervisory Letter 11-7 (Model Risk Management) |
| SR 26-2 | Federal Reserve Supervisory Letter 26-2 (replaces SR 11-7, April 2026) |
| SSM | Single Supervisory Mechanism (ECB-led banking supervision) |
| TRM | Technology Risk Management guidelines (MAS Singapore) |
| TRIM | Targeted Review of Internal Models (ECB) |
| UDAP | Unfair, Deceptive, or Abusive Acts or Practices |
| UQ | Uncertainty Quantification |
| VaR | Value at Risk |
| XAI | Explainable Artificial Intelligence |
| XGBoost | Extreme Gradient Boosting (ML algorithm) |

---

## 8. Coverage Gaps Log

The following topics are not fully covered or are only partially addressed in this knowledge base. AI agents should not generate content implying these topics are covered here.

| Topic | Status | Nearest Coverage |
|-------|--------|-----------------|
| Actuarial model governance (insurance-specific) | Not covered | [01](research/01_regulatory_landscape_overview.md) mentions EIOPA briefly |
| Climate / ESG model risk | Partially covered | [14](research/14_mrm_maturity_and_emerging_topics.md) mentions open regulatory question |
| Quantitative finance models (pricing, derivatives) | Not covered | [02](research/02_sr11_7_deep_dive.md) references VaR in passing |
| Regulatory capital model documentation (AIRB, A-CVA) | Partially covered | [06](research/06_model_inventory_and_governance_ops.md) covers governance, not methodology |
| Model risk in central banks / public institutions | Not covered | — |
| Fintech / non-bank lender MRM | Not covered | [01](research/01_regulatory_landscape_overview.md) CFPB guidance touches this |
| Small / community bank MRM | Partially covered | [14](research/14_mrm_maturity_and_emerging_topics.md) maturity Level 1–2 |
| Model risk in payment systems | Not covered | — |
| Open banking / API model risk | Not covered | — |
| Reinforcement learning model governance | Not covered | — |
| Quantum computing impact on cryptographic models | Not covered | — |
| Model risk in algorithmic trading (HFT) | Not covered | [02](research/02_sr11_7_deep_dive.md) mentions market models briefly |

---

## 9. Source and Reference Index

Key primary sources cited across this knowledge base, organized by type.

### Regulatory Documents

| Document | Issuer | Year | Primary File(s) |
|----------|--------|------|----------------|
| SR 11-7 — Supervisory Guidance on Model Risk Management | Federal Reserve | 2011 | [02](research/02_sr11_7_deep_dive.md), [04](research/04_bank_mrm_frameworks.md) |
| OCC Bulletin 2011-12 | OCC | 2011 | [02](research/02_sr11_7_deep_dive.md) |
| SR 26-2 / OCC Bulletin 2026-13 — Revised Model Risk Management Guidance | Federal Reserve / OCC | April 2026 | [02](research/02_sr11_7_deep_dive.md), [01](research/01_regulatory_landscape_overview.md) |
| CFPB Circular 2023-03 — Adverse Action and AI | CFPB | 2023 | [12](research/12_explainability_fairness_bias.md) |
| EU AI Act (Regulation 2024/1689) | EU Parliament & Council | 2024 | [03](research/03_eu_ai_act_finance.md) |
| PRA Supervisory Statement SS1/23 — Model Risk Management Principles | PRA (UK) | 2023 | [01](research/01_regulatory_landscape_overview.md), [04](research/04_bank_mrm_frameworks.md) |
| MAS Technology Risk Management Guidelines | MAS (Singapore) | 2021 | [01](research/01_regulatory_landscape_overview.md) |
| MAS Model AI Governance Framework for Generative AI | MAS (Singapore) | May 2024 | [07](research/07_genai_governance_banking.md) |
| FINMA Circular 2023/1 — Operational Risk and Resilience | FINMA | 2023 | [01](research/01_regulatory_landscape_overview.md) |
| HKMA Supervisory Policy Manual CA-G-4 | HKMA | Various | [01](research/01_regulatory_landscape_overview.md) |
| APRA CPS/CPG 220 | APRA (Australia) | Various | [01](research/01_regulatory_landscape_overview.md) |
| ECB Guide to Internal Models | ECB | 2019, updated 2025 | [01](research/01_regulatory_landscape_overview.md), [04](research/04_bank_mrm_frameworks.md) |
| EBA Guidelines on Internal Models (IRB) | EBA | 2017–2023 | [01](research/01_regulatory_landscape_overview.md) |

### Industry Frameworks

| Document | Issuer | Year | Primary File(s) |
|----------|--------|------|----------------|
| NIST AI Risk Management Framework 1.0 | NIST | January 2023 | [10](research/10_industry_frameworks_nist_iso.md) |
| NIST AI 600-1 — Generative AI Profile | NIST | July 2024 | [10](research/10_industry_frameworks_nist_iso.md) |
| ISO/IEC 42001:2023 — AI Management Systems | ISO | 2023 | [10](research/10_industry_frameworks_nist_iso.md) |
| OECD AI Principles | OECD | 2019, revised 2024 | [10](research/10_industry_frameworks_nist_iso.md) |
| G7 Hiroshima Process — Code of Conduct for GPAI | G7 | 2023 | [10](research/10_industry_frameworks_nist_iso.md) |
| OWASP Top 10 for LLM Applications | OWASP | 2025 | [standards/owasp_top10_llm.md](standards/owasp_top10_llm.md) |
| OWASP Top 10 for Agentic AI | OWASP | 2026 | [standards/owasp_top10_agentic.md](standards/owasp_top10_agentic.md) |
| FSB Financial Stability Implications of AI | FSB | November 2024 | [14](research/14_mrm_maturity_and_emerging_topics.md), [07](research/07_genai_governance_banking.md) |

### Vendor / Tech Company Publications

| Document | Publisher | Year | Primary File(s) |
|----------|-----------|------|----------------|
| IBM Cost of a Data Breach Report 2025 | IBM / Ponemon Institute | 2025 | [standards/ibm_cost_of_data_breach_2025.md](standards/ibm_cost_of_data_breach_2025.md), [11](research/11_big_tech_mrm_guidance.md) |
| Microsoft Responsible AI Standard v2 | Microsoft | 2022 | [11](research/11_big_tech_mrm_guidance.md) |
| Anthropic Model Specification | Anthropic | January 2026 | [11](research/11_big_tech_mrm_guidance.md) |
| Anthropic Responsible Scaling Policy (RSP 3.3) | Anthropic | 2025 | [11](research/11_big_tech_mrm_guidance.md) |
| Google Model Cards | Google | 2019 (framework) | [11](research/11_big_tech_mrm_guidance.md) |

---

*Knowledge base maintained in `C:\Study\Myprojects\claudeprojects\MRM`. For navigation questions, start with this README. For missing topics, see Section 7 (Coverage Gaps). For abbreviations, see Section 6.*
