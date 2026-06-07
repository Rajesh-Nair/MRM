# CLAUDE.md — MRM Knowledge Base

## What This Repository Is

This is a **Model Risk Management (MRM) knowledge base** for financial services. It covers traditional ML model governance, Generative AI / LLM governance, and Agentic AI governance — including how major banks implement MRM, global regulatory frameworks (SR 11-7/SR 26-2, EU AI Act, PRA SS1/23, MAS TRM), and technical topics (XAI, fairness, drift monitoring, MLOps).

---

## Agent Navigation Protocol — FOLLOW EXACTLY

You are operating in a curated knowledge base. **Token efficiency is critical.** Do not read files speculatively or exhaustively.

### Step 1 — Consult the Cross-Index BEFORE opening any research file

README.md (this directory) is always available. It contains:

- **"File Quicklook" section**: one-line "answers what" summary for every file — scan this first
- **"Cross-Index of Key Topics" section**: alphabetical topic → file mapping (~90 topics)
- **"Abbreviations and Glossary" section**: expand any abbreviation without opening a file
- **"Coverage Gaps Log" section**: topics NOT in this KB — check here before saying something is missing

**Read README.md first.** Navigate via the cross-index. Then read the ONE file that matches.

### Step 2 — Read at most ONE research file per question

The cross-index marks one file as the primary source per topic. Read that file. Do not open additional files unless the cross-index lists a second file explicitly as a primary source for the same topic.

**Exception:** If a question spans two distinct topics (e.g., "What does SR 11-7 say about model validation?"), read the ONE file that covers both (file `02` covers SR 11-7 and validation together).

### Step 3 — Resolve ambiguity from README, not from files

- **Abbreviation unknown?** → Section 6 of README.md
- **Topic not in cross-index?** → Section 7 of README.md (Coverage Gaps log)
- **Unsure which file?** → Section 4 of README.md (File Quicklook) — read the "Answers" column

### Step 4 — Answer directly

Once you have read the target file, answer from its content. Do not open additional files to "fill in gaps" unless the user explicitly asks for a cross-file comparison.

---

## File Map (Quick Reference)

| File | Path | One-Line Topic |
|------|------|---------------|
| 01 | `research/01_regulatory_landscape_overview.md` | Global MRM regulation — US, EU, UK, APAC jurisdictions |
| 02 | `research/02_sr11_7_deep_dive.md` | SR 11-7 and SR 26-2 — foundational US MRM framework |
| 03 | `research/03_eu_ai_act_finance.md` | EU AI Act for financial services — obligations and timeline |
| 04 | `research/04_bank_mrm_frameworks.md` | How JPMorgan, Goldman, HSBC, Citi, Barclays etc. govern models |
| 05 | `research/05_model_validation_methodology.md` | Model validation — back-testing, PSI, ML/LLM-specific methods |
| 06 | `research/06_model_inventory_and_governance_ops.md` | Model inventories, tiering, MRC, shadow models, tooling |
| 07 | `research/07_genai_governance_banking.md` | Extending SR 11-7 to LLMs and Gen AI at banks |
| 08 | `research/08_llm_risk_taxonomy.md` | 33-risk LLM taxonomy: Model / Data / Operational / Conduct |
| 09 | `research/09_agentic_ai_governance.md` | Autonomous agent governance — HITL, kill switches, audit trails |
| 10 | `research/10_industry_frameworks_nist_iso.md` | NIST AI RMF, ISO 42001, OECD AI Principles, COBIT |
| 11 | `research/11_big_tech_mrm_guidance.md` | IBM, Google, Microsoft, AWS, Anthropic responsible AI frameworks |
| 12 | `research/12_explainability_fairness_bias.md` | LIME, SHAP, fairness definitions, disparate impact, ECOA |
| 13 | `research/13_model_drift_monitoring_mlops.md` | Drift types, PSI/CSI, MLOps pipelines, LLM monitoring |
| 14 | `research/14_mrm_maturity_and_emerging_topics.md` | MRM maturity levels, emerging topics, regulatory horizon |
| S1 | `standards/owasp_top10_llm.md` | OWASP Top 10 for LLM Applications 2025 |
| S2 | `standards/owasp_top10_agentic.md` | OWASP Top 10 for Agentic AI 2026 |
| S3 | `standards/ibm_cost_of_data_breach_2025.md` | IBM/Ponemon Cost of Data Breach 2025 — full structured summary |

---

## Common Question → File Routing

These are the most frequent question types and which single file to open:

| Question pattern | Open this file |
|-----------------|---------------|
| "What is SR 11-7?" / "What is SR 26-2?" / "US model risk regulation" | `02` |
| "EU AI Act" / "high-risk AI" / "GPAI" / "conformity assessment" | `03` |
| "How does [bank name] govern models?" / "3 lines of defense" / "Model Risk Committee" | `04` |
| "How do banks validate ML models?" / "back-testing" / "PSI" / "conceptual soundness" | `05` |
| "Model inventory" / "model tiering" / "shadow models" / "vendor models" | `06` |
| "Gen AI governance" / "LLM governance" / "is it a model?" / "RAG governance" | `07` |
| "LLM risks" / "hallucination" / "prompt injection" / "PII memorization" | `08` |
| "Agent risk" / "HITL" / "kill switch" / "agentic AI governance" | `09` |
| "NIST AI RMF" / "ISO 42001" / "OECD AI Principles" | `10` |
| "IBM AIF360" / "Google Model Cards" / "SageMaker Clarify" / "Anthropic RSP" | `11` |
| "SHAP" / "LIME" / "fairness" / "disparate impact" / "ECOA adverse action" | `12` |
| "Model drift" / "concept drift" / "MLOps" / "monitoring" / "decommissioning" | `13` |
| "MRM maturity" / "synthetic data" / "federated learning" / "systemic AI risk" | `14` |
| "OWASP LLM" / "prompt injection security" / "LLM security risks" | `S1` |
| "OWASP agentic" / "agent security" / "agent hijacking" | `S2` |
| "IBM data breach" / "breach cost" / "shadow AI risk" / "AI breach statistics" | `S3` |
| Global regulatory overview / "what does MAS/FCA/FINMA require?" | `01` |

---

## Rules Summary (for agents)

1. **README first, file second.** Always use README.md to navigate before opening a research file.
2. **One file per question.** Read the one most relevant file; do not chain-read.
3. **Cross-index is authoritative.** README Section 5 tells you which file covers which topic.
4. **Gaps are logged.** If README Section 7 lists a topic as not covered, say so — don't invent content.
5. **Glossary is in README.** Don't open files to resolve abbreviations.
6. **Do not re-read files.** If a file was already read in this conversation, use that context; do not re-read.
