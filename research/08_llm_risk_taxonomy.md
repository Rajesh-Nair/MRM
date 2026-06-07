# LLM Risk Taxonomy for Financial Services: A Four-Dimension Framework

## File Metadata
- **Scope:** Four-dimension risk taxonomy for LLMs in financial services â€” Model Risk, Data Risk, Operational Risk, and Conduct/Consumer Risk â€” with controls and residual risk assessment
- **Cluster:** C â€” Gen AI and LLM Governance
- **Reading order:** 8/14
- **Related files:** [07_genai_governance_banking.md](07_genai_governance_banking.md), [09_agentic_ai_governance.md](09_agentic_ai_governance.md), [11_big_tech_mrm_guidance.md](11_big_tech_mrm_guidance.md), [12_explainability_fairness_bias.md](12_explainability_fairness_bias.md), [../standards/owasp_top10_llm.md](../standards/owasp_top10_llm.md)
- **Regulators/bodies covered:** Federal Reserve, OCC, FCA, CFPB, BCBS, FSB, NIST
- **Tags:** LLM-risk, hallucination, prompt-injection, data-poisoning, PII-memorization, conduct-risk, consumer-risk, discriminatory-AI, risk-taxonomy, OWASP-LLM, operational-risk, vendor-concentration

---

## 1. Introduction: Why Financial Services Needs an LLM-Specific Risk Taxonomy

Traditional model risk management taxonomies â€” developed primarily for quantitative statistical models â€” do not map cleanly onto the risk surface of large language models. A credit scorecard's risks are primarily statistical: overfitting, sample selection bias, temporal instability. A market risk VaR model's risks are primarily mathematical: distributional assumptions, correlation breakdown under stress. The SR 11-7 framework was designed to manage these categories of model risk.

LLMs introduce an entirely different and substantially broader risk surface. They can generate discriminatory text as readily as they generate helpful text. They can memorize and reproduce training data verbatim, exposing PII at inference time. They can be manipulated through crafted inputs in ways that have no analog in traditional model governance. They are deployed through supply chains involving foundation model providers, cloud infrastructure operators, and third-party plugin developers â€” each introducing independent risk. And because they are used to generate customer communications, compliance interpretations, and decision support, the conduct implications of LLM errors are potentially severe.

This file provides a comprehensive, four-dimension risk taxonomy for LLMs in financial services. Each risk is assessed for likelihood in financial services contexts, potential impacts, key controls, and residual risk after controls. The taxonomy is designed to support risk identification and classification work, model risk committee reporting, AI governance policy development, and regulatory examination preparation.

The four dimensions are:
1. **Model Risk** â€” risks arising from the LLM's technical characteristics and behavior
2. **Data Risk** â€” risks arising from training data, fine-tuning data, and retrieval corpora
3. **Operational Risk** â€” risks arising from the infrastructure, deployment, and supply chain
4. **Conduct and Consumer Risk** â€” risks arising from the effect of LLM outputs on customers and markets

For specific security risk descriptions (prompt injection, supply chain, output integrity), cross-reference `../standards/owasp_top10_llm.md` rather than this file.

---

## 2. Dimension 1: Model Risk

Model risk for LLMs encompasses the risks that arise from the inherent technical characteristics of the model itself â€” its output behavior, its calibration, its stability, and the limits of our ability to validate it.

### 2.1 Hallucination Risk

**Risk Description:** Hallucination is the generation of outputs that are factually incorrect, internally inconsistent, or fabricated, presented with fluency and apparent confidence indistinguishable from accurate outputs. The term encompasses several distinct failure modes: factual confabulation (inventing facts not in training data), citation hallucination (fabricating sources or misattributing quotes), logical inconsistency (producing outputs that contradict each other or the provided context), and entity confusion (misidentifying named entities, regulatory codes, or financial instruments).

Hallucination is not a bug to be fixed but a structural feature of how LLMs generate text: they predict the most statistically likely next token given context, which is not the same as the most factually accurate next token. Retrieval-Augmented Generation significantly reduces hallucination for factual recall tasks but does not eliminate it â€” models can still misinterpret retrieved documents, interpolate between conflicting sources, or generate conclusions not supported by retrieved evidence.

**Likelihood in Financial Services:** High. Research indicates hallucination rates of 3%â€“27% depending on model and task type. At operational scale â€” thousands of queries per day â€” even a 3% hallucination rate produces hundreds of potentially incorrect outputs daily. High-stakes financial tasks (regulatory interpretation, loan underwriting documentation, compliance sign-off) face elevated hallucination risk because they require precise, nuanced accuracy rather than general fluency.

**Potential Impact:**
- *Financial:* Erroneous financial information leading to customer losses; regulatory fines for material misstatements; reprocessing costs for transactions initiated on hallucinated data
- *Reputational:* Public exposure of AI-generated misinformation in customer communications or public filings
- *Regulatory:* Breach of Consumer Duty, UDAP, or ECOA obligations where hallucinated outputs affect customer decisions
- *Customer Harm:* Customers acting on incorrect information about product terms, eligibility, rates, or regulatory rights

**Key Controls:**
- Retrieval-Augmented Generation to ground outputs in verified corpora
- Multi-model consensus requiring agreement among independent LLM instances before acting on outputs
- Source citation requirements forcing models to reference specific documents for factual claims
- Human review requirements for high-stakes outputs before they are presented to customers or used in decisions
- Automated factuality checking against authoritative knowledge bases for structured fact types
- Production sampling with human annotation to measure hallucination rates continuously
- "According-to" prompt engineering (e.g., "according to [specified policy document]...") to anchor responses in authoritative sources

**Residual Risk After Controls:** Medium. Even with RAG and human review, hallucination cannot be reduced to zero in complex, open-ended queries. The residual risk is highest in novel situations not well-represented in the retrieval corpus and lowest in narrow, well-specified tasks with comprehensive RAG coverage.

---

### 2.2 Prompt Sensitivity Risk

**Risk Description:** LLM outputs change materially in response to minor variations in prompt wording, structure, ordering of information, or conversational context. Studies have demonstrated that changing the ordering of multiple-choice answer options can shift benchmark accuracy by up to 13%. Adding or removing a single sentence of context can shift outputs between compliant and non-compliant responses. This sensitivity means that prompt templates â€” designed and tested at deployment time â€” may produce systematically different outputs in production when user-provided context is added, when conversation history accumulates, or when minor paraphrasing occurs.

Prompt sensitivity also manifests across languages: a system prompt designed and tested in English may behave differently when users interact in French, Mandarin, or Arabic, due to differences in how the model's training data represents different languages and concepts.

**Likelihood in Financial Services:** High. Financial institutions rely on system prompts and instruction templates to constrain LLM behavior â€” ensuring appropriate risk disclosures, preventing advice-giving in non-advisory contexts, maintaining regulatory compliance messaging. Prompt sensitivity creates persistent risk that these controls function as designed in test but not in production.

**Potential Impact:**
- *Regulatory:* Compliance controls in system prompts may be bypassed by user conversational patterns, creating regulatory exposure
- *Reputational:* Inconsistent AI behavior creates unpredictable customer experiences
- *Operational:* Prompt changes introduced without re-testing may silently degrade controlled behaviors

**Key Controls:**
- Version control and change management for all prompt templates with mandatory re-testing before deployment
- Automated regression testing running a curated suite of prompts against current production models daily
- Red-teaming specifically targeting prompt sensitivity: systematically vary phrasing, ordering, and context to identify fragile control points
- Guard rail layers independent of the primary LLM (separate filtering models or rule-based systems) to enforce critical compliance behaviors regardless of prompt variation
- Language-specific testing for multilingual deployments

**Residual Risk After Controls:** Medium. Comprehensive regression testing reduces the probability of undetected prompt sensitivity failures but cannot cover the full space of possible user inputs. Guard rails independent of the primary LLM provide the most robust residual control.

---

### 2.3 Context Window Limitation Risk

**Risk Description:** LLMs process input through a context window â€” a fixed maximum number of tokens that can be attended to simultaneously. While context windows have grown substantially (many frontier models now support 128,000+ tokens), there are two persistent risks. First, when input exceeds the context window, earlier content is silently truncated â€” models do not warn users that information has been dropped. For a financial institution processing long regulatory documents or multi-day conversation histories, truncation can cause the model to miss material information. Second, research has demonstrated that LLMs struggle to utilize information embedded in the middle of very long contexts (the "lost in the middle" problem) â€” performance degrades for content not located near the beginning or end of the context window even when the total length fits within the maximum.

**Likelihood in Financial Services:** Medium-High. Banks routinely work with long documents: regulatory filings, loan agreements, prospectuses, multi-year audit trails. Deploying LLMs to analyze these documents without context management controls creates risk.

**Potential Impact:**
- *Financial:* Material information missed in document analysis leading to incorrect decisions
- *Regulatory:* Incomplete review of compliance-relevant documents creating regulatory exposure
- *Audit:* No record of what information was dropped from context, creating audit trail gaps

**Key Controls:**
- Document chunking strategies that ensure critical sections appear at prompt boundaries
- Explicit context length monitoring with warnings when input approaches limits
- Hierarchical summarization for very long documents (summarize sections first, then synthesize)
- Retrieval-based architectures (RAG) that retrieve only the most relevant sections rather than passing full documents
- User disclosure when document length exceeds optimal context processing parameters

**Residual Risk After Controls:** Low-Medium with appropriate architectural controls; High without them.

---

### 2.4 Model Version Drift Risk

**Risk Description:** For banks accessing foundation models through vendor APIs, the model being served may change without the bank's knowledge or consent. Behavioral updates can be pushed to a model version without a new version name, API changelog entry, or advance customer notification. A longitudinal study published in 2026 confirmed "meaningful behavioral drift across deployed transformer services" over a ten-week period, with some models exhibiting systematically shorter, less detailed responses after undisclosed updates. For institutions that rely on consistent model behavior as a control â€” for example, a model consistently refusing to provide advice outside its defined scope â€” undisclosed behavioral updates can silently undermine those controls.

Under SR 11-7 (and its successor SR 26-2), a material change to model behavior requires re-validation. If the model is changing silently, the bank cannot identify when re-validation is required.

**Likelihood in Financial Services:** High. All banks using frontier model APIs are exposed to this risk. It is not a hypothetical â€” OpenAI pushed a behavioral update to GPT-4o in April 2025 without advance notification.

**Potential Impact:**
- *Regulatory:* Undetected model changes may mean deployed models have not been re-validated after material changes, creating SR 26-2 examination findings
- *Operational:* Behavioral drift may silently degrade controlled behaviors (guardrails, scope limitations)
- *Financial:* Degraded model performance can affect decision quality

**Key Controls:**
- Pin deployments to specific named model versions (e.g., `claude-3-5-sonnet-20241022`) rather than floating aliases (e.g., `claude-sonnet-latest`)
- Automated daily regression testing comparing current model outputs against a historical baseline on a curated benchmark suite
- Contractual change notification requirements specifying advance notice periods (typically 30 days minimum for behavioral changes)
- Automated alerting when regression test scores deviate beyond defined thresholds
- API response logging enabling post-hoc analysis of behavioral changes

**Residual Risk After Controls:** Low-Medium. Pinned versions eliminate undisclosed in-version drift but create deprecation risk. Regression testing provides early warning of behavioral changes even for pinned versions.

---

### 2.5 Temperature and Sampling Parameter Sensitivity

**Risk Description:** LLM output distribution is controlled by parameters including temperature (higher temperature = more diverse but less focused outputs), top-p (nucleus sampling), top-k, and frequency/presence penalties. These parameters are typically set by the application developer and may not be formally reviewed or documented. Inappropriate parameter settings can increase hallucination rates (high temperature increases creative but less accurate outputs), reduce consistency (making audit trail comparison more difficult), or produce outputs outside the expected distribution for compliance monitoring purposes.

**Likelihood in Financial Services:** Medium. Most enterprise deployments operate with temperature near 0 for consistency, but lack of formal governance over parameter settings means misconfiguration risk is real.

**Potential Impact:**
- *Operational:* Inconsistent outputs making monitoring and compliance verification more difficult
- *Model Risk:* Validation conducted at one temperature setting may not represent production behavior if parameters are changed after validation

**Key Controls:**
- Formal documentation of all inference parameters as part of model/application governance records
- Change control requirements for parameter changes analogous to prompt change management
- Validation conducted at production parameter settings, with retesting required for parameter changes
- Parameter locking mechanisms (API configuration management) preventing unauthorized changes

**Residual Risk After Controls:** Low. This is a well-understood and controllable risk.

---

### 2.6 Reproducibility Failure

**Risk Description:** SR 11-7 implicitly relies on reproducibility: the ability to re-run a model and obtain the same output. This enables audit trail validation, dispute resolution (recreating the model output that informed a decision), and regulatory examination (reproducing historical decisions for supervisory review). LLMs with non-zero temperature are not reproducible by design. Even at temperature 0, variations in hardware, software versions, and batch processing can introduce output differences. For regulated financial decisions supported by LLM outputs, the inability to reproduce the exact output that informed a decision creates audit trail and dispute resolution challenges.

**Likelihood in Financial Services:** High. Any LLM application supporting regulated decisions faces this risk.

**Potential Impact:**
- *Regulatory:* Inability to reproduce historical model outputs creates examination challenges; potential findings on audit trail completeness
- *Legal:* Dispute resolution in credit decisions requires demonstrating what the model actually output; reproducibility failure complicates this
- *Operational:* Cannot reproduce and investigate incident-causing outputs

**Key Controls:**
- Log complete model outputs (not just final responses) for all regulated decisions, with timestamps and model version identifiers
- Log inference parameters alongside outputs to enable best-effort reconstruction
- For high-stakes applications, consider deterministic generation settings (temperature 0 with seed) to maximize reproducibility within hardware limitations
- Retain complete conversation context (system prompt, user turns, model turns) enabling audit trail reconstruction
- Define and document what "reproducing" a historical LLM output means in the context of SR 26-2 examination readiness

**Residual Risk After Controls:** Medium. Perfect reproducibility is not achievable for stochastic LLMs. Comprehensive logging reduces residual risk substantially by preserving the inputs and outputs even when exact reproduction is not possible.

---

### 2.7 Emergent Capability Risk

**Risk Description:** Foundation models exhibit emergent capabilities â€” behaviors that appear as models scale in parameter count, training data, and compute. These emergent capabilities are difficult to predict and may not be apparent during pre-deployment testing. An LLM deployed for document summarization may demonstrate emergent capabilities in financial reasoning, code generation, or persuasion that the deploying institution never tested for and has no controls around. The challenge is compounded by the fact that foundation models continue to be updated, potentially introducing new emergent capabilities in models the bank is already running in production.

**Likelihood in Financial Services:** Medium-High. The risk is highest for broad-scope deployments (general-purpose chat assistants, unconstrained research tools) and lowest for narrow-scope applications (document summarization with strict output format requirements).

**Potential Impact:**
- *Regulatory:* Models demonstrating unauthorized capabilities (advice-giving, trading signals) in contexts where these are prohibited
- *Reputational:* Unexpected model behaviors causing public harm or embarrassment
- *Conduct:* Unsupervised capability activation leading to consumer harm

**Key Controls:**
- Capability-scoped system prompts that explicitly define the model's role and constrain behavior to a defined domain
- Guard rail layers that independently filter outputs for out-of-scope content categories
- Red-teaming specifically probing for capabilities beyond the intended scope of deployment
- Regular capability assessment updates as foundation model versions are updated
- Principle of least capability: choose the smallest model capable of the task, reducing the emergent capability surface

**Residual Risk After Controls:** Medium. Emergent capability risk cannot be fully eliminated, particularly for complex frontier models deployed in broad-scope applications. The residual risk is manageable for narrow, well-defined use cases and elevated for broad-scope deployments.

---

### 2.8 Benchmark Gaming and Goodhart's Law for LLM Evaluation

**Risk Description:** Goodhart's Law states: "when a measure becomes a target, it ceases to be a good measure." This principle applies powerfully to LLM evaluation. Foundation model providers optimize performance on public benchmarks (MMLU, HumanEval, etc.) during training. Models can perform well on benchmarks while failing on closely related real-world tasks â€” "contaminating" the test set with training data, or optimizing for superficial patterns rather than genuine capability. Research has demonstrated that changing the ordering of multiple-choice answers in MMLU can decrease accuracy by up to 13%, indicating that some performance reflects pattern matching rather than reasoning.

For banks that rely on vendor-reported benchmark performance to justify model selection, benchmark gaming creates a risk that selected models underperform in production relative to pre-deployment evaluation.

**Likelihood in Financial Services:** Medium. Banks conducting sophisticated independent evaluation using financial-domain benchmarks face lower risk. Banks relying solely on vendor-published benchmarks face higher risk.

**Potential Impact:**
- *Model Risk:* Overestimation of model capability leading to insufficient human oversight
- *Operational:* Underperformance in production applications not predicted by benchmark evaluations

**Key Controls:**
- Independent evaluation using domain-specific financial benchmarks (FinBen, MultiFinBen) rather than relying solely on vendor-published results
- Blind evaluation on held-out financial service task datasets never published or shared with model providers
- Multi-benchmark assessment using diverse evaluation sets to reduce susceptibility to any single benchmark's limitations
- Real-world pilot testing with human expert grading before production deployment

**Residual Risk After Controls:** Low-Medium. Independent evaluation substantially reduces benchmark gaming risk.

---

### 2.9 Overconfidence Calibration Failures

**Risk Description:** Well-calibrated probabilistic models express uncertainty proportional to their actual accuracy â€” a model saying it is 90% confident should be right 90% of the time. LLMs are often poorly calibrated: they express high confidence for correct and incorrect answers alike. This overconfidence is particularly dangerous in financial services, where users often rely on expressed confidence as a signal of reliability. An LLM that says "the capital requirement under CRR2 Article 92 is X%" with complete confidence when it is actually wrong by a factor of two is more dangerous than a model that flags its own uncertainty.

**Likelihood in Financial Services:** High. LLMs consistently present outputs with the same fluency and confidence tone regardless of actual accuracy. Most enterprise deployments do not implement uncertainty quantification.

**Potential Impact:**
- *Customer Harm:* Customers treating confident but wrong AI outputs as authoritative
- *Regulatory:* Misrepresentation of information to customers without appropriate uncertainty qualification

**Key Controls:**
- System prompt requirements for explicit uncertainty language ("I am not certain about this," "you should verify this with..." )
- Domain-specific uncertainty probes during evaluation to assess calibration
- User interface design that communicates the inherently probabilistic nature of LLM outputs
- Output filtering that requires model outputs to include source citations, limiting confident unsupported claims

**Residual Risk After Controls:** Medium. Calibration improvement is an active research area but no fully reliable solution exists for instruction-following LLMs.

---

### 2.10 Out-of-Distribution Behavior

**Risk Description:** LLMs trained on web-scale text corpora may perform reliably for tasks well-represented in training data but behave erratically for novel inputs â€” financial instruments introduced after the training cutoff, newly enacted regulatory frameworks, proprietary terminology specific to a particular institution. Out-of-distribution inputs are particularly likely in financial services because the domain uses specialized terminology, evolves with regulatory changes, and involves novel financial structures.

**Likelihood in Financial Services:** High. Financial terminology, regulations, and products evolve continuously. Models trained with data cutoffs of 12-24 months lag real-world financial service environments.

**Potential Impact:**
- *Model Risk:* Systematically incorrect outputs for financial inputs that fall outside training distribution
- *Regulatory:* Outputs reflecting outdated regulatory frameworks

**Key Controls:**
- Knowledge cutoff monitoring: track foundation model training data cutoffs and flag use cases where recent developments are material
- RAG with continuously updated corpora to inject current regulatory and market information
- Regular evaluation on recent financial events and regulatory changes outside the model's training period
- Disclaimer requirements in outputs noting training data limitations

**Residual Risk After Controls:** Low-Medium with RAG; High without.

---

## 3. Dimension 2: Data Risk

Data risk for LLMs encompasses risks arising from the data used to train and fine-tune the model, data used in retrieval corpora, and data processed at inference time.

### 3.1 Training Data Contamination

**Risk Description:** Foundation model training data is assembled from massive web corpora, books, code repositories, and other sources. This data is not curated with financial services standards: it contains biased content, outdated information, contested assertions, and in some cases factually wrong financial information. The Common Crawl corpus â€” a primary training data source for many frontier models â€” contains web content spanning decades, including superseded regulatory guidance, incorrect financial information, and text produced by non-expert sources. Banks cannot audit the training data composition of closed-source foundation models.

Beyond quality issues, training data may be contaminated with content specifically designed to influence model behavior â€” a form of data poisoning at the corpus level that may not be detectable post-training.

**Likelihood in Financial Services:** High. All banks using commercial foundation models are exposed to training data quality risk; the magnitude depends on the task and the degree to which outputs are grounded in verified proprietary corpora.

**Potential Impact:**
- *Model Risk:* Systematically biased outputs in domains where training data was unrepresentative
- *Regulatory:* Outputs reflecting discriminatory patterns in training data creating fair lending exposure
- *Reputational:* Biased or incorrect outputs traced to training data contamination

**Key Controls:**
- Foundation model selection due diligence including review of vendor data sourcing documentation and training data characteristics
- Fine-tuning or instruction tuning on high-quality, curated financial data to partially override biased base model behavior
- RAG architectures to ground outputs in bank-curated, quality-controlled corpora rather than relying on training data recall
- Output monitoring for demographic bias patterns and factual error patterns
- Regulatory examination readiness: document the limitations of training data quality as a known residual risk

**Residual Risk After Controls:** Medium. Training data quality risk is partially mitigable but cannot be fully controlled for commercial foundation models.

---

### 3.2 PII Memorization

**Risk Description:** LLMs memorize portions of their training data and can reproduce this data verbatim in response to certain prompts. Research has demonstrated that membership inference attacks â€” testing whether a specific piece of text was in a model's training data â€” succeed at rates significantly above random chance. More practically, models can be prompted to regurgitate personally identifiable information present in training data: real names, email addresses, phone numbers, account details if financial records appeared in training data. For fine-tuned models trained on internal bank data, this risk extends to customer PII included in fine-tuning datasets.

A 2025 Truffle Security research project found approximately 12,000 live API keys and passwords in a single major training dataset crawl, with 63% of those secrets appearing across multiple pages. This demonstrates that sensitive credentials can be memorized and potentially reproduced.

**Likelihood in Financial Services:** Medium-High. The risk is highest for fine-tuned models (where bank-specific data directly enters training) and lower for commercial foundation models where financial institution-specific data is unlikely to appear at training-corpus scale.

**Potential Impact:**
- *Privacy:* Exposure of customer PII in response to queries, violating GDPR, CCPA, and related privacy regulations
- *Legal:* Regulatory fines for privacy violations; litigation from affected customers
- *Regulatory:* FCA Consumer Duty violations; CFPB enforcement actions

**Key Controls:**
- Data minimization in fine-tuning datasets: use synthetic data, k-anonymized data, or aggregate statistics rather than real customer PII
- Differential privacy techniques during fine-tuning (DP-SGD) to limit memorization mathematically
- Output scanning for PII patterns (names, account numbers, national ID numbers) before returning responses
- Red-teaming specifically targeting memorization: probe the model with partial PII to assess completion risk
- Regular privacy audits of fine-tuned models using membership inference techniques

**Residual Risk After Controls:** Low-Medium with differential privacy and output scanning; Medium-High for fine-tuned models without these controls.

---

### 3.3 Copyright and Intellectual Property Exposure

**Risk Description:** Foundation models trained on web corpora have ingested substantial copyrighted material â€” books, research papers, news articles, financial research reports, proprietary databases. When these models reproduce substantially similar content at inference time, there is potential copyright liability. Ongoing litigation (New York Times v. OpenAI, class action suits against Anthropic) has not yet produced definitive judicial rulings on whether training on copyrighted data constitutes infringement, but the legal risk is live and material. For banks that use LLMs to generate content, the concern is whether model-generated output could constitute a copyright derivative work creating liability.

Additionally, if a bank's proprietary financial models, trading algorithms, or research appear in LLM training data (through inadvertent publication or deliberate leakage), those models may be reproduced or described by the LLM.

**Likelihood in Financial Services:** Medium. Copyright litigation is ongoing and not yet settled. The risk is higher for applications that generate long-form content (research reports, regulatory documents) and lower for short-response applications.

**Potential Impact:**
- *Legal:* Copyright infringement liability for reproducing protected works in model outputs
- *Competitive:* Proprietary methods or research appearing in LLM outputs accessible to competitors
- *Reputational:* Association with AI copyright controversy

**Key Controls:**
- System prompt requirements prohibiting verbatim reproduction of extended text passages
- Output monitoring for verbatim text matching against known protected works
- Vendor contractual protections: major foundation model providers offer intellectual property indemnification for enterprise customers
- Clear attribution requirements in outputs where content is drawn from specific sources
- Legal review of high-volume content generation use cases

**Residual Risk After Controls:** Low-Medium. IP indemnification from major vendors reduces financial exposure substantially.

---

### 3.4 Fine-Tuning Data Leakage

**Risk Description:** When a bank fine-tunes a foundation model on internal data â€” customer records, loan files, compliance documents, trading data â€” that data is baked into the model's weights. If the fine-tuned model is later accessed by parties other than intended users (through API exposure, model weight exfiltration, or overly broad query access), training data may be recoverable through targeted prompting. Fine-tuning data leakage is a higher risk than base model memorization because the bank directly controls what data enters fine-tuning and bears responsibility for the resulting risk.

**Likelihood in Financial Services:** Medium. This risk is specific to institutions that fine-tune models on internal data. It is not relevant for institutions using commercial API access without fine-tuning.

**Potential Impact:**
- *Privacy:* Customer PII included in fine-tuning datasets potentially extractable by users
- *Competitive:* Proprietary internal data potentially exposed through model outputs
- *Regulatory:* Privacy regulation violations

**Key Controls:**
- Strict data hygiene for fine-tuning datasets: remove PII, use aggregated or synthetic data
- Model weight security: treat fine-tuned model weights as sensitive assets with access controls equivalent to the most sensitive data included in training
- Access controls on fine-tuned model APIs limiting the query space to prevent targeted extraction attacks
- Regular extraction testing: probe fine-tuned models for memorized training data as a validation component

**Residual Risk After Controls:** Low-Medium with rigorous data hygiene; High without.

---

### 3.5 RAG Retrieval Errors

**Risk Description:** Retrieval-Augmented Generation systems retrieve documents from a corpus and pass them as context to the LLM. If the retrieval system returns the wrong documents â€” semantically related but not directly relevant, outdated versions of the correct documents, or documents from the wrong jurisdiction or product line â€” the LLM will base its response on incorrect context. The LLM may not detect that retrieved documents are wrong; it will generate fluent, confident-sounding responses based on whatever context is provided. This creates a failure mode where RAG introduces a new class of error: retrieval failure compounded by confident generation.

Research suggests that at deployment scale, even a 5% retrieval error rate translates to a material proportion of outputs potentially based on incorrect source documents.

**Likelihood in Financial Services:** Medium-High. Financial institutions deploying RAG for regulatory compliance, customer queries, or research synthesis face this risk continuously.

**Potential Impact:**
- *Financial:* Decisions based on incorrect source documents (wrong regulatory version, wrong product terms)
- *Compliance:* Regulatory compliance interpretations based on outdated or incorrect documents
- *Customer Harm:* Product information based on incorrect retrieved documents

**Key Controls:**
- Retrieval accuracy testing: regular evaluation of retrieval precision and recall on representative financial query sets
- Embedding model validation: confirm the embedding model correctly represents financial domain semantics
- Reranking models to improve final document selection quality
- Source citation requirements: force the LLM to cite retrieved documents, enabling human verification
- Corpus freshness monitoring: automated alerts when documents in the corpus are older than defined thresholds
- Relevance score thresholds: reject retrieval results below minimum similarity scores rather than passing poor-quality context

**Residual Risk After Controls:** Low-Medium with comprehensive retrieval monitoring; Medium-High without.

---

### 3.6 Data Poisoning in RAG Corpus

**Risk Description:** If the RAG retrieval corpus can be manipulated by external parties â€” either through compromised document ingestion pipelines or through malicious content injection in documents that the system is designed to ingest â€” an attacker can poison the knowledge base to cause the LLM to produce attacker-controlled outputs. Research published in 2024 demonstrated the PoisonedRAG attack: injecting just 5 malicious documents into a corpus of millions caused the AI system to return attacker-specified false answers 90% of the time for targeted trigger questions. This attack is particularly insidious because the foundation model itself behaves correctly â€” the manipulation is in the retrieval corpus.

For cross-reference on data poisoning at the LLM level, see `../standards/owasp_top10_llm.md` (LLM04 â€” Data and Model Poisoning).

**Likelihood in Financial Services:** Medium. Internal corpora (bank policies, regulatory documents) are relatively well-controlled. Corpora incorporating external sources (web content, vendor documents, public filings) face higher poisoning risk.

**Potential Impact:**
- *Security:* Attacker-controlled information appearing in compliance interpretations, customer communications, or decision support outputs
- *Financial:* Corrupted financial information influencing decisions
- *Reputational:* Demonstrably false information produced by bank AI systems

**Key Controls:**
- Pre-ingestion document validation: content scanning, provenance verification, and anomaly detection before documents enter the corpus
- Strict access controls on corpus ingestion pipelines (minimizing the surfaces through which malicious content can enter)
- Document integrity verification (hash-based) for the corpus, detecting unauthorized modifications
- Corpus change auditing: log all corpus additions, modifications, and deletions
- Monitoring for anomalous output patterns that may indicate corpus manipulation

**Residual Risk After Controls:** Low-Medium for internal-only corpora; Medium for corpora incorporating external sources.

---

### 3.7 Embedding Model Vulnerabilities

**Risk Description:** RAG systems use embedding models to convert text into vector representations for semantic search. These embedding models are themselves machine learning models with their own risk surface: they may encode demographic biases from training data, causing semantically similar content to be ranked differently across demographic groups; they may be vulnerable to adversarial embedding attacks where crafted text produces vectors mispositioned in the embedding space; and they introduce additional computational and supply chain complexity. Changes to embedding models (version updates) can materially affect retrieval accuracy and may require re-indexing the entire corpus.

**Likelihood in Financial Services:** Medium. Embedding model risks are less visible than LLM risks but can significantly affect RAG system performance.

**Potential Impact:**
- *Model Risk:* Systematically biased retrieval affecting which documents inform LLM responses
- *Operational:* Embedding model updates causing retrieval degradation without detection

**Key Controls:**
- Embedding model validation including bias assessment for financial domain queries
- Version pinning for embedding models with equivalent controls to foundation model version pinning
- Retrieval accuracy regression testing when embedding model versions are updated
- Pre- and post-update corpus comparison testing when re-indexing after embedding model changes

**Residual Risk After Controls:** Low-Medium.

---

### 3.8 Cross-Contamination in Multi-Tenant Deployments

**Risk Description:** Some financial institutions deploy shared LLM infrastructure serving multiple business units, products, or customer segments. In shared multi-tenant deployments, there is risk that context, memory, or retrieval outputs from one tenant "leak" to another â€” either through inadequate session isolation in the application layer, or through vector database cross-tenant retrieval in shared RAG architectures. This risk is heightened in cloud-hosted foundation model APIs where the infrastructure is shared across many customers (though leading providers implement isolation at inference time).

**Likelihood in Financial Services:** Medium. Shared internal deployments are more likely to have cross-tenant risks than commercial APIs with mature isolation controls.

**Potential Impact:**
- *Privacy:* Customer data from one business unit visible to another (regulatory and privacy violation)
- *Compliance:* Cross-contamination of information across regulatory information barriers (Chinese Wall violations in investment banking)
- *Legal:* Confidentiality obligation breach

**Key Controls:**
- Logical isolation of vector database indices by tenant with cryptographic access controls
- Session isolation at the application layer with strict conversation scoping
- Information barrier enforcement: Chinese wall compliance requirements should explicitly extend to AI system deployment architecture
- Security testing for cross-tenant isolation including penetration testing specifically targeting multi-tenant LLM infrastructure

**Residual Risk After Controls:** Low with rigorous architecture design; High with insufficient isolation.

---

## 4. Dimension 3: Operational Risk

Operational risk for LLMs encompasses risks from infrastructure, deployment, supply chain, and adversarial exploitation of the LLM system.

### 4.1 Latency and Throughput Risk

**Risk Description:** LLMs are computationally intensive and significantly slower than traditional analytical models. A credit scorecard produces a decision in milliseconds; a frontier LLM generating a detailed response may take 2â€“30 seconds depending on response length and infrastructure. At high query volumes, this latency creates queue buildup, timeout risks, and user experience degradation. For customer-facing applications where response time directly affects satisfaction and engagement, LLM latency is a material operational risk.

**Likelihood in Financial Services:** High. Most banking use cases involve user-facing applications where latency directly affects product quality.

**Potential Impact:**
- *Operational:* Service degradation during peak loads; customer dissatisfaction
- *Financial:* Loss of customer engagement; SLA breach in third-party integrations

**Key Controls:**
- Streaming response APIs to provide incremental output, reducing perceived latency
- Response caching for common queries (with appropriate invalidation mechanisms)
- Load balancing across multiple inference endpoints
- Circuit breaker patterns to prevent latency cascades
- Latency SLA monitoring with automated alerting
- Graceful degradation design: predefined fallback responses when LLM performance degrades

**Residual Risk After Controls:** Low-Medium. Latency risk is well understood and manageable with standard cloud architecture practices.

---

### 4.2 API Dependency and Vendor Lock-In

**Risk Description:** Banks that build core applications on a specific foundation model API develop deep technical dependencies: system prompts designed for one model's instruction format, evaluation benchmarks calibrated to one model's characteristics, and fine-tuning data aligned to one model's behavior. Migrating to a different model provider involves re-validation of all dependent applications, which may be impractical at scale. This technical lock-in amplifies the vendor concentration risk described in [07_genai_governance_banking.md](07_genai_governance_banking.md) â€” even if a bank wants to diversify providers after an incident, migration cost and complexity may prevent rapid response.

**Likelihood in Financial Services:** Medium-High. Most banks have developed deep dependencies on one or two foundation model providers.

**Potential Impact:**
- *Strategic:* Inability to exit poor vendor relationships due to migration complexity
- *Operational:* Vulnerable to single-provider outages or capability changes

**Key Controls:**
- Model-agnostic abstraction layers (API gateways) that enable underlying model substitution without application code changes
- Maintenance of evaluation benchmarks and test suites that can be rapidly applied to successor models
- Parallel testing of alternative models for critical applications to maintain migration readiness
- Multi-model deployments for highest-criticality applications
- Contractual provisions limiting vendor's ability to unilaterally change API specifications without notice

**Residual Risk After Controls:** Medium. Full migration readiness is difficult to maintain practically, but abstraction layers reduce transition time significantly.

---

### 4.3 Cost Unpredictability

**Risk Description:** Foundation model APIs use token-based pricing: each input token and output token incurs a charge. At scale, costs can be substantial and difficult to predict. A user who passes a very long document as context, or triggers a long-chain reasoning response, incurs costs many times higher than a typical query. Without token limits and cost controls, a single application incident (prompt injection triggering verbose generation loops, for example) can produce unexpected cost spikes. For banks with strict technology cost governance, unpredictable AI infrastructure costs create budget and approval challenges.

**Likelihood in Financial Services:** High. Token-based pricing is the standard commercial model for frontier foundation models.

**Potential Impact:**
- *Financial:* Unexpected cost overruns from uncontrolled token consumption
- *Operational:* Budget exhaustion causing service interruption

**Key Controls:**
- Token limits per request and per user/session
- Cost monitoring dashboards with real-time alerting on spending anomalies
- Budget caps with circuit breakers that suspend API access when budget thresholds are reached
- Request logging to attribute costs to business units and use cases
- Periodic cost optimization review (are long context windows justified? can shorter prompts achieve equivalent results?)

**Residual Risk After Controls:** Low. Cost risk is well-understood and manageable with standard cloud cost governance.

---

### 4.4 Rate Limiting and Availability Risk

**Risk Description:** Foundation model APIs impose rate limits â€” maximum requests per minute, maximum tokens per minute â€” that can constrain throughput for high-volume applications. Rate limit encounters cause either API errors (hard failures) or queuing delays (soft failures). For applications where response time is critical â€” fraud detection assistance, real-time customer service â€” rate limiting can cause service degradation precisely when demand is highest. Availability risk extends to planned and unplanned outages: major API providers have experienced multi-hour outages affecting global customer bases.

**Likelihood in Financial Services:** Medium. High-volume deployments are at meaningful risk of rate limit encounters; availability risk affects all API-dependent deployments.

**Potential Impact:**
- *Operational:* Service interruption or degradation during peak periods or outages
- *Customer:* Degraded customer service experience
- *Regulatory:* For critical functions, service interruptions may have regulatory implications (operational resilience)

**Key Controls:**
- Rate limit monitoring with predictive alerting before limits are reached
- Request batching and queue management to smooth demand peaks
- Multi-region deployment to reduce single-region outage risk
- Fallback design: predefined responses when API is unavailable
- Tiered application prioritization: during API constraint periods, prioritize highest-criticality applications
- SLA contracts specifying availability commitments and remedies

**Residual Risk After Controls:** Low-Medium. API availability risk is partially mitigated by redundancy but cannot be fully eliminated for externally hosted services.

---

### 4.5 Model Deprecation Risk

**Risk Description:** Foundation model providers retire older model versions on a rolling basis. OpenAI retired GPT-3.5 Turbo in late 2024, forcing customers to migrate to newer models. The typical deprecation notice period for generally available models is 3 months; for preview models, it can be as little as 2 weeks. Banks that have built validated, production applications on a specific model version face a forced re-validation when that version is deprecated. For large institutions with hundreds of LLM-dependent applications, coordinating re-validation across all applications within a 3-month window is operationally challenging.

**Likelihood in Financial Services:** High. All banks using commercial foundation model APIs will face deprecation events on a regular basis.

**Potential Impact:**
- *Operational:* Forced migration of validated applications within compressed timelines
- *Regulatory:* Risk that deprecated versions are replaced with unvalidated alternatives
- *Financial:* Migration cost and resource diversion

**Key Controls:**
- Proactive deprecation monitoring: subscribe to vendor deprecation announcements and maintain a deprecation schedule for all deployed model versions
- Successor model evaluation pipeline: maintain tested evaluation benchmarks that can be rapidly applied to successor models
- Application tiering: prioritize re-validation resources toward highest-risk applications first
- Buffer period policy: begin re-validation at least 6 weeks before deprecation date, not when notice is received
- Contractual deprecation notice requirements: negotiate minimum advance notice periods in enterprise agreements

**Residual Risk After Controls:** Low-Medium. Proactive management reduces but does not eliminate migration pressure.

---

### 4.6 Context Injection Attacks (Indirect Prompt Injection)

**Risk Description:** Indirect prompt injection occurs when malicious instructions are embedded in content that the LLM retrieves or processes as context â€” documents, emails, web pages, database records â€” rather than in the direct user input. Unlike direct prompt injection (where the attacker has direct access to the user interface), indirect injection can be executed by any party who can influence content that the LLM will process. For a bank's document processing system, an attacker could embed malicious instructions in a loan application document, a regulatory filing, or a customer email, causing the LLM to execute attacker-specified behavior when processing that content.

For the detailed security taxonomy of prompt injection, see `../standards/owasp_top10_llm.md` (LLM01 â€” Prompt Injection).

**Likelihood in Financial Services:** High. Banks process enormous volumes of external content â€” customer documents, emails, third-party filings â€” all of which represent potential injection surfaces.

**Potential Impact:**
- *Security:* Unauthorized data exfiltration; unauthorized actions initiated by the LLM; bypass of safety controls
- *Regulatory:* AI-initiated actions violating regulatory requirements
- *Financial:* Unauthorized transactions, data theft

**Key Controls:**
- Treat all externally-sourced content as untrusted input, regardless of format
- Architectural separation between LLM instruction context (system prompt) and data context (retrieved documents, user content)
- Input sanitization and anomaly detection before content enters the LLM context
- Principle of least privilege for LLM capabilities: limit what actions the LLM can initiate
- Output monitoring for anomalous patterns that might indicate injection-triggered behavior
- For agentic systems, require human approval for high-impact actions regardless of LLM instruction source

**Residual Risk After Controls:** Medium. Indirect prompt injection is difficult to fully prevent for systems that process arbitrary external content.

---

### 4.7 Jailbreaking and Safety Bypass

**Risk Description:** Jailbreaking refers to crafted prompt techniques that bypass foundation model safety training, causing models to produce content they were trained to refuse â€” harmful information, discriminatory content, regulatory violations, confidential disclosures. Research has demonstrated attack success rates approaching 97-99% against leading models using automated red-teaming and fuzzing techniques. For financial institutions that rely on foundation model safety training as a control, the near-universal exploitability of these controls is a governance vulnerability that cannot be treated as robust.

**Likelihood in Financial Services:** Medium-High. Deliberate jailbreaking is less common from internal users but remains a risk in customer-facing applications where adversarial users may attempt to manipulate AI system behavior.

**Potential Impact:**
- *Compliance:* Safety-bypassed outputs violating regulatory requirements (investment advice without licensing, discriminatory content)
- *Reputational:* Demonstrably unsafe model behavior publicly exposed
- *Customer Harm:* Harmful or misleading information delivered to customers

**Key Controls:**
- Independent guard rail layers that do not rely on foundation model safety training (external classifiers for prohibited content categories)
- Rate limiting and anomaly detection on conversation patterns consistent with jailbreak attempts
- Human-in-the-loop requirements for high-stakes outputs regardless of model safety behavior
- Regular automated red-teaming for jailbreak vulnerabilities with new attack techniques
- Defense-in-depth: multiple independent control layers rather than reliance on any single safety measure

**Residual Risk After Controls:** Medium. The arms-race nature of jailbreaking means no defense is permanent; defense-in-depth reduces but does not eliminate risk.

---

### 4.8 Supply Chain Risk

**Risk Description:** LLM applications depend on a complex supply chain: foundation model weights, inference infrastructure, vector databases, embedding models, orchestration frameworks (LangChain, LlamaIndex), plugin ecosystems, and API integrations. Each supply chain component introduces potential compromise risk. Malicious fine-tunes â€” model weights deliberately poisoned before distribution â€” have been documented in the open-source model ecosystem. Compromised plugin code can be injected into LLM orchestration frameworks, causing malicious behavior at inference time.

For the detailed security taxonomy of supply chain risk, see `../standards/owasp_top10_llm.md` (LLM03 â€” Supply Chain).

**Likelihood in Financial Services:** Medium. Commercial foundation model providers have supply chain security practices, but the broader ecosystem of orchestration frameworks and plugins is less mature.

**Potential Impact:**
- *Security:* Malicious model behavior introduced through supply chain compromise
- *Data:* Data exfiltration through compromised pipeline components

**Key Controls:**
- AI Bill of Materials (AI-BOM): maintain an inventory of all model components, libraries, and dependencies
- Version pinning with checksum verification for all dependencies
- Prefer signed artifacts from verified providers
- Continuous vulnerability scanning of the dependency ecosystem
- Isolated testing environments for evaluating new components before production integration

**Residual Risk After Controls:** Low-Medium. AI-BOM and checksum verification substantially reduce supply chain risk.

---

## 5. Dimension 4: Conduct and Consumer Risk

Conduct and consumer risk encompasses the risks that LLM outputs cause harm to customers, create regulatory violations, or generate reputational damage.

### 5.1 Discriminatory Outputs in Credit and Insurance Decisions

**Risk Description:** LLMs may generate outputs that exhibit discriminatory patterns in credit, insurance, and hiring decisions â€” either because training data encoded historical discrimination, or because model architecture propagates correlations between protected characteristics and adverse decisions. Research has demonstrated significant racial discrepancies in local LLM outputs for mortgage lending tasks, with biases exceeding those observed in empirical human lending data. Under the Equal Credit Opportunity Act (ECOA) and Fair Housing Act, lenders are prohibited from discrimination regardless of whether the discriminating system is human or AI. The CFPB and OCC have made clear that ECOA applies to AI-generated credit decisions.

**Likelihood in Financial Services:** High. Any LLM deployed in credit decision support, underwriting assistance, or customer eligibility determination faces discrimination risk.

**Potential Impact:**
- *Regulatory:* ECOA, Fair Housing Act, and state fair lending law violations; CFPB and OCC enforcement actions
- *Legal:* Class action litigation; civil money penalties
- *Reputational:* Public exposure of discriminatory AI practices

**Key Controls:**
- Disparate impact testing of LLM outputs across protected characteristics before deployment and ongoing in production
- Prohibition on using protected characteristics (or highly correlated proxies) as model inputs for credit decisions
- Adverse action notice compliance: ensure LLM-supported credit decisions can generate ECOA/Regulation B-compliant specific reasons for denial
- Human review requirements for all adverse credit decisions supported by LLM
- Regular fairness audits by independent parties
- Explainability requirements: for high-stakes decisions, maintain explanations that can be provided to customers

**Residual Risk After Controls:** Medium. Discrimination risk in AI-supported credit decisions remains an active regulatory enforcement priority; ongoing monitoring is essential.

---

### 5.2 Misleading Financial Information and Hallucinated Advice

**Risk Description:** LLMs deployed in customer-facing financial services applications can generate responses that function as financial advice â€” even when not intended to do so. When that advice is based on hallucinated information, the customer harm is compounded. A virtual assistant that confidently states incorrect investment risk characteristics, incorrect fee structures, or incorrect account terms causes direct customer harm and potentially creates regulatory liability. Under Consumer Duty (UK), UDAP (US), and equivalent consumer protection frameworks, financial institutions are responsible for the accuracy of information provided to consumers, including through AI systems.

**Likelihood in Financial Services:** High. Customer-facing LLM applications that respond to product and financial questions are inherently at risk of generating misleading responses.

**Potential Impact:**
- *Customer Harm:* Financial losses from decisions made on incorrect AI-provided information
- *Regulatory:* FCA Consumer Duty violations; CFPB UDAP enforcement; FINRA supervisory findings
- *Legal:* Breach of contract; negligent misrepresentation

**Key Controls:**
- Scope limitation in system prompts: explicitly define and enforce the topics the LLM will address
- Factual grounding through RAG with authoritative product information corpora
- Mandatory disclaimers for financial information outputs
- Escalation design: identify and route questions about sensitive financial topics (investment advice, tax implications) to human advisors
- Regular monitoring of customer interaction transcripts for misleading outputs
- Consumer testing before deployment: test with representative users to identify misleading response patterns

**Residual Risk After Controls:** Medium. Despite controls, the risk that an LLM generates misleading financial information in edge cases cannot be fully eliminated.

---

### 5.3 Regulatory Liability for AI-Generated Customer Communications

**Risk Description:** When a bank uses LLMs to draft or generate customer communications â€” account notices, product disclosures, terms and conditions updates, collection letters â€” those communications carry the same regulatory obligations as manually drafted communications. Regulatory requirements for financial communications include: accuracy and non-misleading content (UDAP, FCA Consumer Duty); required disclosure language (Truth in Lending Act, Truth in Savings Act); specific formatting requirements for adverse action notices (ECOA/Regulation B); and prohibition on unfair, deceptive, or abusive practices. LLM-generated communications may inadvertently omit required disclosures, include prohibited language, or present required information in non-compliant formats.

**Likelihood in Financial Services:** Medium-High. As banks deploy LLMs for marketing content, correspondence, and disclosures, regulatory compliance of AI-generated text becomes critical.

**Potential Impact:**
- *Regulatory:* Regulatory violations in communications sent to millions of customers; potential for systemic enforcement actions
- *Legal:* Class action exposure for regulatory non-compliance in mass communications
- *Financial:* Remediation costs for non-compliant communications already sent

**Key Controls:**
- Compliance template overlay: generate initial drafts with LLM but pass through a rule-based compliance checker for required disclosures and prohibited language before use
- Human review and sign-off requirements for all regulatory-sensitive customer communications
- Legal and compliance approval workflows for new communication templates
- Regular testing of LLM-generated communications against current regulatory requirements

**Residual Risk After Controls:** Low-Medium. Human review of final communications substantially reduces regulatory risk; the residual risk is process failure where review steps are bypassed.

---

### 5.4 Consumer Harm from Automated Decisions

**Risk Description:** Where LLM outputs contribute to automated or semi-automated decisions affecting consumers â€” credit approvals, insurance underwriting, account closure, fraud alerts â€” consumers may suffer harm from incorrect decisions without meaningful recourse. Adverse action notice requirements under ECOA/Regulation B require specific, accurate reasons for credit denial. If an LLM-supported decision cannot produce those specific reasons â€” because the reasoning chain is opaque or stochastic â€” the institution is in breach of regulatory obligations. The CFPB's 2023 Circular explicitly stated that "creditors cannot state reasons for adverse actions by pointing to broad buckets" and must provide behavioral specificity.

**Likelihood in Financial Services:** High. Any use of LLM in credit decision support must address ECOA/Regulation B adverse action notice requirements.

**Potential Impact:**
- *Regulatory:* ECOA violation for inadequate adverse action notices; CFPB enforcement
- *Customer Harm:* Customers denied credit without legally required explanation
- *Legal:* Individual and class action litigation

**Key Controls:**
- Explainability architecture: for each LLM-supported credit decision, maintain a deterministic explanation layer that generates compliant adverse action reasons
- Human decision authority: final credit decisions must be made by humans who can attest to the reasons, with AI providing decision support only
- Legal review of adverse action notice practices for AI-supported decisions
- Regular ECOA/Regulation B compliance testing of the full decision-to-notice pipeline

**Residual Risk After Controls:** Medium. The explainability challenge for LLMs in credit decisions is not fully resolved; the residual risk is that explanation layers do not accurately represent actual model reasoning.

---

### 5.5 Reputational Risk from Harmful or Offensive Outputs

**Risk Description:** LLMs can generate outputs that are offensive, inappropriate, or harmful in ways that create severe reputational damage. Despite safety training, models can produce outputs that are discriminatory, sexually inappropriate, politically inflammatory, or otherwise harmful â€” particularly in adversarial scenarios (deliberate jailbreaking) or unusual conversational contexts. In financial services, where brand trust is a critical competitive asset, even isolated incidents of harmful AI outputs can cause disproportionate reputational damage.

**Likelihood in Financial Services:** Medium. Customer-facing LLMs with millions of interactions generate substantial opportunity for edge cases, and adversarial users may deliberately seek harmful outputs.

**Potential Impact:**
- *Reputational:* Public exposure of harmful AI outputs causing customer trust damage
- *Regulatory:* Depending on content, regulatory implications (discriminatory content, financial misinformation)
- *Financial:* Customer attrition following reputational incidents

**Key Controls:**
- Content safety guard rails (independent classifier layers for harmful content detection)
- Human-readable harm categories defined and tested in adversarial red-teaming
- Incident response procedures for harmful output events, including public communication templates
- User reporting mechanism allowing customers to flag inappropriate outputs for rapid investigation
- Ongoing monitoring of output quality using automated and human sampling

**Residual Risk After Controls:** Low-Medium. Defense-in-depth guard rails substantially reduce harmful output frequency; residual risk lies in novel attack vectors and edge cases.

---

### 5.6 Manipulation Risk

**Risk Description:** LLMs can be fine-tuned or prompted to favor particular outcomes â€” recommending specific products, steering customers toward high-margin options, or presenting information in ways that systematically favor the institution over the customer. Unlike human sales manipulation (which is governed by individual conduct obligations), AI-mediated manipulation can be applied uniformly across millions of customer interactions, creating systemic conduct risk. This risk is particularly acute when banks deploy LLMs in customer engagement contexts where there is inherent tension between customer interests and institutional revenue objectives.

**Likelihood in Financial Services:** Medium. Most institutions have not deliberately designed manipulative LLMs, but the risk of inadvertent optimization toward commercial outcomes is real.

**Potential Impact:**
- *Regulatory:* FCA Consumer Duty violations for failing to act in customer interests; CFPB UDAP enforcement for manipulation
- *Reputational:* Systematic AI-mediated manipulation of customers causing severe trust damage
- *Legal:* Class action for unfair sales practices

**Key Controls:**
- Prohibition on instruction tuning or fine-tuning LLMs on objective functions that reward commercial outcomes (click-through rates, product uptake)
- Independent testing for systematic output bias toward institutional interests
- Consumer Duty/best interest monitoring: regular sampling of customer interactions to assess whether AI recommendations reflect customer interests
- Conflict of interest disclosure in AI-mediated advisory interactions

**Residual Risk After Controls:** Medium. The boundary between legitimate product promotion and manipulation in AI contexts is contested and evolving in regulatory guidance.

---

### 5.7 Privacy Violations in Customer Interactions

**Risk Description:** LLM-powered customer service agents process sensitive customer information in the course of interactions. This creates multiple privacy risks: context retention across sessions may cause one customer's information to influence another's experience; customer data submitted through conversation may be stored in ways inconsistent with privacy policy representations; fine-tuned models trained on customer interaction logs may memorize and reproduce individual customer details; and in multi-tenant shared infrastructure, session isolation failures could expose customer data across boundaries.

**Likelihood in Financial Services:** Medium-High. Given the volume of customer data processed by bank LLM applications, privacy exposure risk is material.

**Potential Impact:**
- *Privacy:* GDPR, CCPA, GLBA, and equivalent violations; regulatory fines
- *Customer:* Customer trust damage from privacy incidents
- *Legal:* Individual and class action litigation

**Key Controls:**
- Minimal data retention: do not retain conversational context beyond the immediate session without customer consent and regulatory basis
- Privacy-by-design in LLM application architecture: implement data minimization at the collection layer
- Regular privacy impact assessments for LLM applications processing customer PII
- Customer transparency: clear disclosure of how AI systems use and retain customer information
- Data subject access rights: enable customers to access, correct, and delete their information processed by AI systems

**Residual Risk After Controls:** Low-Medium with comprehensive privacy-by-design architecture.

---

## 6. Master Risk Heat Map

The following table provides a consolidated risk heat map across all four dimensions, summarizing likelihood and impact ratings before and after controls.

| Risk | Dimension | Likelihood (Pre-Control) | Impact | Likelihood (Post-Control) | Residual Risk Level |
|------|-----------|------------------------|--------|--------------------------|---------------------|
| Hallucination | Model | High | High | Medium | Medium |
| Prompt Sensitivity | Model | High | Medium | Medium | Medium |
| Context Window Limitation | Model | Medium-High | Medium | Low | Low-Medium |
| Model Version Drift | Model | High | Medium-High | Low | Low-Medium |
| Temperature/Sampling Sensitivity | Model | Medium | Low-Medium | Low | Low |
| Reproducibility Failure | Model | High | Medium | Medium | Medium |
| Emergent Capabilities | Model | Medium-High | Medium-High | Medium | Medium |
| Benchmark Gaming | Model | Medium | Medium | Low | Low-Medium |
| Overconfidence Calibration | Model | High | Medium | Medium | Medium |
| Out-of-Distribution Behavior | Model | High | Medium-High | Low-Medium | Low-Medium |
| Training Data Contamination | Data | High | Medium | Medium | Medium |
| PII Memorization | Data | Medium-High | High | Low-Medium | Low-Medium |
| Copyright Exposure | Data | Medium | Medium | Low | Low-Medium |
| Fine-Tuning Data Leakage | Data | Medium | High | Low-Medium | Low-Medium |
| RAG Retrieval Errors | Data | Medium-High | Medium-High | Low-Medium | Low-Medium |
| RAG Corpus Poisoning | Data | Medium | High | Low-Medium | Low-Medium |
| Embedding Model Vulnerabilities | Data | Medium | Medium | Low | Low-Medium |
| Cross-Tenant Contamination | Data | Medium | High | Low | Low |
| Latency and Throughput | Operational | High | Medium | Low | Low-Medium |
| API Dependency / Lock-In | Operational | Medium-High | Medium | Medium | Medium |
| Cost Unpredictability | Operational | High | Low-Medium | Low | Low |
| Rate Limiting / Availability | Operational | Medium | Medium | Low | Low-Medium |
| Model Deprecation | Operational | High | Medium | Low-Medium | Low-Medium |
| Indirect Prompt Injection | Operational | High | High | Medium | Medium |
| Jailbreaking / Safety Bypass | Operational | Medium-High | High | Medium | Medium |
| Supply Chain Risk | Operational | Medium | High | Low-Medium | Low-Medium |
| Discriminatory Outputs | Conduct | High | High | Medium | Medium |
| Misleading Financial Information | Conduct | High | High | Medium | Medium |
| AI-Generated Communication Liability | Conduct | Medium-High | High | Low-Medium | Low-Medium |
| Adverse Action Notice Non-Compliance | Conduct | High | High | Medium | Medium |
| Reputational Risk / Harmful Output | Conduct | Medium | High | Low-Medium | Low-Medium |
| Manipulation Risk | Conduct | Medium | High | Medium | Medium |
| Privacy Violations | Conduct | Medium-High | High | Low-Medium | Low-Medium |

---

## 7. OWASP LLM Top 10 Mapping to Risk Dimensions

The OWASP Top 10 for LLM Applications (see `../standards/owasp_top10_llm.md`) provides a security-focused taxonomy that maps to and complements this four-dimension financial risk taxonomy. The following table shows the mapping:

| OWASP LLM Risk | Primary Dimension | Secondary Dimension | Key Overlap |
|----------------|------------------|---------------------|-------------|
| LLM01 â€” Prompt Injection | Operational | Conduct | Indirect prompt injection (Section 4.6) |
| LLM02 â€” Sensitive Information Disclosure | Data | Conduct | PII memorization (Section 3.2), Privacy (Section 5.7) |
| LLM03 â€” Supply Chain | Operational | Data | Supply chain risk (Section 4.8), Training data contamination (Section 3.1) |
| LLM04 â€” Data and Model Poisoning | Data | Operational | RAG corpus poisoning (Section 3.6), Training data contamination (Section 3.1) |
| LLM05 â€” Insecure Output Handling | Conduct | Operational | AI communication liability (Section 5.3), Hallucination (Section 2.1) |
| LLM06 â€” Excessive Agency | Operational | Conduct | Emergent capabilities (Section 2.7) â€” expanded in agentic AI governance file |
| LLM07 â€” System Prompt Leakage | Operational | Data | Fine-tuning data leakage (Section 3.4) |
| LLM08 â€” Vector and Embedding Weaknesses | Data | Operational | RAG retrieval errors (Section 3.5), Embedding model vulnerabilities (Section 3.7) |
| LLM09 â€” Misinformation | Conduct | Model | Hallucination (Section 2.1), Misleading financial information (Section 5.2) |
| LLM10 â€” Unbounded Consumption | Operational | â€” | Cost unpredictability (Section 4.3), Rate limiting (Section 4.4) |

---

## 8. LLM Risks vs. Traditional ML Model Risks: Comparative Analysis

Understanding how LLM risks compare to traditional ML model risks is essential for MRM teams extending existing frameworks rather than building from scratch.

### Risks That Are Fundamentally New for LLMs

The following risks have no meaningful analog in traditional ML model governance and require entirely new controls:

- **Hallucination** â€” Traditional models produce outputs within trained distributions; LLMs generate novel text that may be fabricated
- **Prompt sensitivity** â€” Traditional models have fixed input schemas; LLMs respond to unstructured natural language with extreme input sensitivity
- **Indirect prompt injection** â€” Traditional models process structured data inputs that cannot contain hidden instructions; LLMs process natural language that can embed adversarial instructions
- **Context window truncation** â€” Traditional models process fixed-length feature vectors; LLMs have context limits with silent truncation behavior
- **Jailbreaking** â€” Traditional models have stable behavioral characteristics; LLMs can be manipulated into behaving outside trained parameters through adversarial input
- **Benchmark gaming / evaluation contamination** â€” Traditional model validation uses clean train/test splits; LLM evaluation is complicated by training data contamination in public benchmarks

### Risks That Are Materially Amplified for LLMs

The following risks exist in traditional ML but are substantially more severe or more complex to manage for LLMs:

- **Model version drift** â€” Traditional model versions are explicitly deployed; LLM API versions can change behavior without formal release management
- **Training data opacity** â€” Traditional models use bank-curated training data; LLM training data is largely undisclosed to the deploying institution
- **PII memorization** â€” Traditional models do not memorize training data verbatim; LLMs can recall and reproduce training data at inference time
- **Emergent capabilities** â€” Traditional models do only what they were trained to do; LLMs may exhibit capabilities not anticipated in pre-deployment testing
- **Overconfidence calibration** â€” Traditional probabilistic models can provide calibrated uncertainty estimates; LLMs present outputs with uniform confidence regardless of actual accuracy
- **Supply chain complexity** â€” Traditional model supply chains are simple; LLM applications involve foundation models, embedding models, orchestration frameworks, vector databases, and plugin ecosystems

### Risks That Are Continuous from Traditional ML

The following risks require the same governance approach for LLMs as for traditional models, though the specific controls must adapt:

- **Training data bias / discrimination risk** â€” Both traditional and LLM models can encode discriminatory patterns from training data
- **Out-of-distribution behavior** â€” Both model types can fail on inputs outside the training distribution
- **Vendor concentration risk** â€” Both model types create vendor dependency, though LLM dependency is typically higher
- **Documentation and reproducibility** â€” Both model types require documentation and audit trail management
- **Model deprecation** â€” Both traditional and LLM model versions can be deprecated, requiring migration planning

---

## 9. Financial Services-Specific Risk Intensification Factors

Certain characteristics of the financial services industry intensify the risks described above:

**Regulatory Density:** Banking is one of the most heavily regulated industries globally. Every LLM output that intersects with regulatory obligations â€” credit decisions, customer communications, compliance interpretations, regulatory reports â€” carries heightened regulatory risk. The volume of regulatory touchpoints means that even low-frequency failure modes (hallucination at 3% frequency) produce material compliance events at banking scale.

**High-Stakes Decisions:** Unlike consumer internet applications where LLM errors are primarily a user experience issue, banking LLM applications support decisions with significant financial consequences for customers: credit approvals, insurance coverage, investment recommendations. The consequence of errors is therefore amplified beyond what the error frequency alone would suggest.

**Information Asymmetry:** Bank customers often lack the financial sophistication to detect erroneous AI-generated financial information. Unlike professional users who can identify hallucinations in their domain, retail customers may treat bank AI outputs as authoritative. This amplifies the consumer harm dimension of all Model Risk errors.

**Systemic Risk Concentration:** Large financial institutions process millions of interactions through the same foundation models. If a foundation model exhibits systematic failure â€” biased outputs, hallucination about a specific type of financial instrument, incorrect regulatory interpretation â€” the failure affects millions of customers simultaneously. This systemic dimension amplifies the potential impact of Model Risk and Conduct Risk categories.

**Real-Time Market Interaction:** For banks deploying LLMs in trading support, market intelligence, or real-time risk assessment, output errors can cause immediate financial market impacts rather than delayed harm.

---

## 10. Cross-References

- **OWASP Top 10 for LLM Applications** â€” Full security-focused risk taxonomy that complements and overlaps with Sections 4 and 5 above: see `../standards/owasp_top10_llm.md`
- **OWASP Top 10 for Agentic Applications** â€” Extended risk taxonomy for autonomous AI agents, which amplifies many of the risks above: see `../standards/owasp_top10_agentic.md`
- **Gen AI Governance in Banking** â€” Governance frameworks and institutional approaches that implement controls for these risks: see [07_genai_governance_banking.md](07_genai_governance_banking.md)
- **Agentic AI Governance** â€” How agentic deployment amplifies Model Risk, Operational Risk, and Conduct Risk: see [09_agentic_ai_governance.md](09_agentic_ai_governance.md)
- **Explainability, Fairness, and Bias** â€” Deep treatment of discriminatory output risk and adverse action notice compliance: see [12_explainability_fairness_bias.md](12_explainability_fairness_bias.md)
- **Big Tech MRM Guidance** â€” How technology providers frame AI risk for deploying institutions: see [11_big_tech_mrm_guidance.md](11_big_tech_mrm_guidance.md)

---

*Sources consulted: NIST AI 600-1 Generative AI Profile (July 2024); NIST AI 100-1 AI Risk Management Framework (January 2023); FSB Financial Stability Implications of AI (November 2024); FSB Monitoring AI Adoption Report (October 2025); EU AI Act (Regulation EU 2024/1689); ECB Supervisory Guide to Internal Models (July 2025); CFPB Consumer Protection Circular 2023-03; OCC/Fed/FDIC SR 26-2 (April 2026); MITRE ATLAS adversarial AI framework; PoisonedRAG research (2024); Vectara hallucination research (2024); BioTech Magazine LLM Hallucination in Financial Institutions (2025); Deloitte Agentic AI Risks in Banking (2025); US Treasury Financial Services AI RMF (February 2026); Truffle Security training data research (2025); CFPB AI lending comment letter (August 2024); Brookings Institution AI fair lending policy (2024); Skadden AI fair lending analysis (2024).*

