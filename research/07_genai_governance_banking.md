# Generative AI Governance in Banking: Extending Model Risk Management for LLMs

## File Metadata
- **Scope:** How banks are extending MRM frameworks to govern Generative AI / LLM systems, including definitional debates, governance structures, and regulatory expectations
- **Cluster:** C â€” Gen AI and LLM Governance
- **Reading order:** 7/14
- **Related files:** [02_sr11_7_deep_dive.md](02_sr11_7_deep_dive.md), [04_bank_mrm_frameworks.md](04_bank_mrm_frameworks.md), [08_llm_risk_taxonomy.md](08_llm_risk_taxonomy.md), [09_agentic_ai_governance.md](09_agentic_ai_governance.md), [../standards/owasp_top10_llm.md](../standards/owasp_top10_llm.md)
- **Regulators/bodies covered:** Federal Reserve, OCC, FCA, ECB, MAS, BCBS, BIS, FSB
- **Tags:** GenAI, LLM, foundation-model, RAG, SR-11-7-extension, JPMorgan, Goldman-Sachs, HSBC, Citi, AI-governance, model-definition, hallucination, prompt-sensitivity, third-party-model

---

## 1. Introduction: A New Governance Frontier

The deployment of Generative AI â€” encompassing large language models (LLMs), retrieval-augmented generation (RAG) pipelines, and multimodal foundation models â€” represents the most significant structural challenge to bank Model Risk Management (MRM) since the 2011 publication of SR 11-7. Traditional MRM was designed for a world where models are deterministic or near-deterministic systems with narrow, well-defined functions: a credit scorecard predicts probability of default; a VaR model estimates portfolio loss distributions. Regulators and model risk managers developed SR 11-7's three-pillar framework â€” sound development practice, rigorous independent validation, and effective governance â€” around these assumptions.

Generative AI breaks virtually every assumption embedded in that framework. Foundation models are stochastic systems that produce different outputs in response to the same input. They are trained on data that banks cannot audit, fine-tuned through processes that banks often do not control, and accessed through APIs that can change behavior without formal notification. A single foundation model can simultaneously power hundreds of banking applications â€” creating a risk concentration phenomenon with no precedent in traditional MRM. And unlike a credit model, whose universe of relevant outputs is numeric probability estimates, an LLM can generate advice, code, regulatory interpretations, customer communications, and (in agentic configurations) take actions in external systems.

By 2024, leading global banks had deployed generative AI at scale. JPMorgan Chase deployed its LLM Suite to over 230,000 employees by mid-2024, running over 450 distinct use cases. Goldman Sachs rolled out its GS AI platform to 46,500 employees under a governance framework that adapted its existing MRM structures. Morgan Stanley deployed AI @ Morgan Stanley Assistant and Debrief to its wealth management advisors. HSBC launched its Gen AI hub-and-spoke architecture, embedding 2,500 AI experts across the organization. These deployments happened in parallel with regulators developing guidance â€” creating a governance gap that banks are actively working to close.

This file examines how banks are extending MRM frameworks to govern generative AI: why existing frameworks are necessary but insufficient, how the definitional questions are being resolved, what governance structures are emerging, and what regulators are beginning to expect.

---

## 2. Why SR 11-7 Is Necessary but Insufficient for LLMs

SR 11-7's core principles â€” that models should be fit for purpose, independently validated, and continuously monitored â€” remain entirely valid for generative AI. What SR 11-7 cannot do is operationalize these principles for systems with radically different technical characteristics. Understanding the specific gaps is essential to designing the extension.

### 2.1 Non-Deterministic Outputs

SR 11-7 implicitly assumes that given the same inputs, a model produces the same output. This enables back-testing, parallel-run validation, and performance benchmarking against historical data. LLMs are governed by temperature parameters and sampling algorithms that introduce randomness by design. Setting temperature to 0 (greedy decoding) reduces but does not eliminate variation; RLHF (Reinforcement Learning from Human Feedback) introduces alignment-driven stochasticity at inference time. The practical consequence: two identical prompts submitted seconds apart may yield materially different responses. For a credit decision support tool, a slight output difference might be tolerable. For a regulatory interpretation assistant, or a customer communication generator, material divergence between runs is a governance failure waiting to happen.

Traditional validation approaches â€” run the model on a test set, measure performance metrics â€” produce point-in-time snapshots that may not represent the distribution of outputs in production. Validators must now think probabilistically: what is the distribution of outputs across multiple runs? What is the tail risk of that distribution? What does a catastrophically wrong output look like, and how often does it occur?

### 2.2 Inability to Back-Test Against Labeled Ground Truth

SR 11-7 validation relies heavily on outcomes analysis: compare model predictions against observed outcomes. For a fraud model, you compare fraud flags against actual confirmed fraud cases. For a credit model, you compare probability of default scores against realized defaults. Generative AI largely lacks this luxury. When an LLM summarizes a regulatory filing, there is no "correct" summary in a historical dataset to compare against. When a coding assistant suggests a refactoring, ground truth is a matter of engineering judgment. When a wealth management assistant recommends reading material, the appropriate answer depends on each advisor's specific context.

This creates a validation gap that banks are addressing through proxy metrics: human-labeled test sets (expensive and potentially inconsistent), automated LLM-as-judge systems (circular â€” using AI to evaluate AI), structured task completion benchmarks (narrow, gameable), and user satisfaction measures (lagging, subjective). None of these approaches satisfies the rigor of traditional outcomes analysis, and regulators are beginning to probe how banks are addressing this gap.

### 2.3 The Hallucination Problem

Perhaps the most commercially salient challenge is hallucination: LLMs generate outputs that are confident, fluent, and factually wrong. Research indicates that hallucination rates vary significantly by model and task type â€” GPT-4 class models hallucinate in approximately 3% of summarization tasks, while smaller open-source models may exceed 15% on the same tasks. For factual question-answering, rates can approach 27% even for leading models. In absolute terms, a financial institution processing thousands of LLM queries per day faces hundreds of potentially incorrect outputs daily even at a 3% hallucination rate.

The financial consequences of hallucination are severe. A chatbot that misstates insurance coverage limits exposes the institution to breach of contract liability. An LLM that generates incorrect regulatory interpretations creates compliance risk. A research assistant that fabricates analyst citations could damage investment decisions. A lending support system that hallucinates about borrower eligibility criteria creates ECOA exposure. Banks are required under SR 11-7 to characterize model uncertainty â€” and for LLMs, hallucination is a fundamental, irreducible form of uncertainty that must be acknowledged, measured, and controlled.

The mitigation landscape is evolving: Retrieval-Augmented Generation (RAG) grounds model outputs in verified corpora and reduces hallucination materially for factual recall tasks, though it introduces its own risks (wrong documents retrieved, poisoned retrieval corpus). Multi-model consensus â€” requiring agreement among multiple LLM outputs before acting â€” is used by some financial firms for high-stakes applications. Structured output formats with citations reduce undetectable confabulation. Human review requirements for high-stakes outputs remain the most robust control but introduce latency.

### 2.4 Prompt Sensitivity

LLM behavior changes materially in response to minor variations in prompt wording, structure, and ordering. Systematic studies have demonstrated that changing the order of multiple-choice answer options in prompts can decrease benchmark accuracy by up to 13%. Adding or removing a single sentence of context can shift outputs from compliant to non-compliant responses. For banks that rely on prompt templates to control LLM behavior â€” ensuring, for example, that a customer-facing assistant always includes appropriate risk disclosures â€” prompt sensitivity creates a persistent control risk.

This has several governance implications. First, prompt templates must be treated as controlled artifacts subject to change management: versioned, approved, and tested before deployment. Second, prompt changes â€” however minor â€” may require re-validation of the dependent system. Third, in adversarial scenarios, bad actors can craft prompts that shift model behavior toward outcomes the institution has not tested or approved. This is the domain of prompt injection attacks, covered in depth in the OWASP Top 10 for LLM Applications (see `../standards/owasp_top10_llm.md`).

### 2.5 Emergent Capabilities

Foundation models exhibit emergent capabilities â€” abilities that appear at scale that were not present in smaller models and were not explicitly trained for. These emergent behaviors are poorly understood and difficult to predict. In financial services contexts, this creates a specific governance problem: a model deployed for document summarization may be capable of generating investment advice, executing mathematical reasoning, or producing code â€” capabilities the deploying institution never tested for and may have no controls around.

Research has shown that capabilities can emerge discontinuously as model scale increases, making pre-deployment testing insufficient to characterize behavior across the full capability space. Banks that deploy foundation models â€” particularly those with broad permission to process and respond to unstructured user queries â€” must implement controls that constrain the effective capability surface rather than relying solely on testing for specific failure modes.

### 2.6 Version Opacity and API Drift

Banks that access foundation models through APIs (OpenAI, Anthropic, Google) face a novel risk: the model they validated may not be the model they are running in production. OpenAI pushed a behavioral update to GPT-4o in April 2025 without a public announcement, API changelog entry, or advance notification to enterprise customers. A longitudinal study published in 2026 confirmed "meaningful behavioral drift across deployed transformer services" over a ten-week period. Vendors typically commit to providing three months' notice for deprecation of generally available model versions, but preview models may be retired with as little as two weeks' notice â€” and behavioral updates within a version may receive no formal notification at all.

Under SR 11-7, any material change to a model requires re-validation. If the model is changing silently, the bank has no visibility into when re-validation is required. Banks are addressing this through several mechanisms: pinning to specific named model versions rather than floating aliases (e.g., `gpt-4o-2024-08-06` rather than `gpt-4o`); automated daily regression testing against a curated benchmark suite to detect behavioral drift; contractual change notification obligations with foundation model vendors; and maintaining shadow deployment of the previously validated model version for comparison.

### 2.7 Training Data Opacity

SR 11-7 requires understanding of the data used to develop a model, including its quality, representativeness, and potential biases. For foundation models, this is nearly impossible. Training datasets for GPT-4 class models are not publicly disclosed. Reported contamination issues in public training corpora are well-documented: Common Crawl archives have been found to contain thousands of live API keys, PII, potentially biased web content, and content that violates copyright. Banks cannot audit OpenAI's training data. They cannot determine whether their institution's own public filings, customer communications, or proprietary research appears in the training corpus.

This creates a risk that banks can partially mitigate but cannot eliminate through vendor management. Contractual prohibitions on using customer interactions for model training provide some protection. Data handling agreements that specify data residency and isolation provide further assurance. However, the fundamental opacity of foundation model training data remains a governance gap that regulators are beginning to question.

### 2.8 The "Model Within a Model" Problem: RAG, Chains, and Agent Frameworks

Modern LLM deployments rarely consist of a single model producing outputs. Instead, they involve architectures where multiple components interact: a retrieval system selects documents from a vector database; an embedding model converts those documents into vector representations; the foundation model generates a response conditioned on the retrieved documents; a reranking model reorders candidates; output guard rails filter the response. Each component introduces its own failure modes, and failures can compound across the chain.

This creates what practitioners call the "model within a model" problem from an MRM perspective. Which component constitutes "the model" for SR 11-7 purposes? Should each component be independently validated? How should the interaction effects between components be tested? Banks are actively developing answers. The emerging consensus is that the entire pipeline requires governance, not just the foundation model at its center, and that pipeline testing (evaluating end-to-end outputs, not just component outputs) is required alongside component-level validation.

---

## 3. The Definitional Debate: Is an LLM a "Model" Under SR 11-7?

### 3.1 The SR 11-7 Definition

SR 11-7 defines a "model" as: "a quantitative method, system, or approach that applies statistical, economic, financial, or mathematical theories, techniques, and assumptions to process input data into quantitative estimates." The definition further specifies three components: an information input component, a processing component, and a reporting component.

The immediate challenge for LLMs is that "quantitative estimates" is a narrow description. An LLM producing free-text output â€” a summarization, a response to a customer query, a draft regulatory interpretation â€” is not producing a quantitative estimate in any traditional sense. Yet it is plainly using statistical and mathematical theory (transformer attention mechanisms, probability distributions over token sequences) to process input into output. A strict textual reading might exclude LLMs from the definition; a purposive reading â€” applying the governance intent of SR 11-7 â€” clearly encompasses them.

### 3.2 Does a RAG Pipeline Constitute a Model?

The question is even more acute for RAG pipelines. A RAG system takes a query, retrieves relevant documents from a corpus using embedding-based similarity search, augments the prompt with retrieved content, and passes the augmented prompt to a foundation model. The retrieval step uses an embedding model (a neural network trained to produce meaningful vector representations). The similarity search uses mathematical operations (cosine similarity or approximate nearest neighbor search). The foundation model applies statistical inference.

Industry practice in 2024-2025 has generally resolved this as follows: the RAG pipeline as a whole should be subject to model governance, not just the constituent foundation model. The retrieval component's accuracy (does it retrieve the right documents?) and freshness (is the corpus current?) require ongoing monitoring. Retrieval failures can produce hallucinated outputs even from a technically sound foundation model. From a governance perspective, the combination of retrieval + augmentation + generation constitutes a system whose outputs require the same scrutiny as any other model output.

### 3.3 Does a Prompt Template Constitute a Model?

This is perhaps the most contested question in the industry. A prompt template â€” a structured input designed to direct LLM behavior â€” can dramatically shape outputs. A prompt that instructs a model to "always recommend consulting a financial advisor before making investment decisions" is performing a control function analogous to a business rule in a traditional scoring system. A prompt that defines the persona and knowledge scope of a customer-facing assistant is defining system behavior.

Some banks have argued that prompt templates are closer to software configuration than model development and should be managed through IT change control rather than MRM. Others have taken the position that because prompt engineering directly determines model output, changes to system prompts require MRM review and approval. The emerging consensus, supported by supervisory feedback at major institutions, is a risk-based approach: prompts that determine model behavior in material, customer-facing, or risk-bearing applications require MRM-adjacent governance (documentation, testing, approval, change control), even if not full model validation.

### 3.4 The "AI Application vs. AI Model" Distinction

Several large banks â€” particularly JPMorgan Chase and Goldman Sachs â€” have articulated a distinction between an "AI model" (a quantitative system requiring full MRM treatment) and an "AI application" (a system that uses an AI model as a component but whose primary risk is operational rather than model risk). Under this framework, the LLM itself is the model; the RAG pipeline, prompt templates, and surrounding infrastructure constitute the AI application.

This distinction has practical governance implications. Model validation focuses on the foundation model's capabilities, limitations, and behavior under stress. Application governance â€” which may sit with a Chief Information Officer or Chief Data Officer rather than a Model Risk Officer â€” focuses on the pipeline design, data quality, access controls, and use case appropriateness. The critical requirement is that neither domain be left ungoverned: the risk is that splitting responsibility between MRM and technology governance creates a coverage gap.

---

## 4. How Banks Categorize Gen AI Systems for Governance Purposes

Different categories of Gen AI deployment carry different risk profiles and require different governance approaches. The following taxonomy has emerged across large financial institutions:

### 4.1 Tier 1: Self-Hosted Open-Source Models

Banks that deploy open-source LLMs (Meta's Llama series, Mistral AI models, Falcon) on their own infrastructure have the greatest control but also the greatest responsibility. These deployments require full MRM treatment because the bank is the model developer. Governance obligations include: documentation of model selection rationale; pre-training data sourcing and quality assessment (where feasible); fine-tuning process documentation; comprehensive validation against use-case-specific benchmarks; ongoing performance monitoring; and a formal model change process for updates or fine-tuning iterations.

HSBC's multi-year agreement with Mistral AI (announced 2024) exemplifies this approach. HSBC's framework for open-source model deployment includes its AI Centre of Excellence providing hub-level oversight, with business-line AI Review Councils providing spoke-level review before any model moves from pilot to production.

### 4.2 Tier 2: Fine-Tuned Models (PEFT, LoRA, Instruction Tuning)

Banks that take a foundation model and fine-tune it on proprietary data â€” whether through full fine-tuning, Parameter-Efficient Fine-Tuning (PEFT), or Low-Rank Adaptation (LoRA) â€” occupy an intermediate governance tier. The base model's characteristics are inherited from the foundation model provider; the fine-tuning process introduces new behaviors that the bank controls. Governance requirements include: documentation of the fine-tuning dataset (its provenance, quality, and potential biases); validation of the fine-tuned model against both the base model (to characterize the behavioral delta) and use-case-specific benchmarks; assessment of whether fine-tuning has degraded capabilities present in the base model; and ongoing monitoring for fine-tuning-induced drift as new model versions are released.

Goldman Sachs' approach to LLM deployment illustrates this tier: the firm fine-tuned LLMs with internal codebases to improve relevance for finance-specific tasks, deploying models within private AI environments with code compliance checks to ensure output met regulatory and security standards.

### 4.3 Tier 3: API-Connected Foundation Models

The dominant deployment pattern for most banks is access to frontier foundation models (GPT-4/o/4.1, Claude 3/3.5/4, Gemini 1.5/2.0) through vendor APIs. This creates a third-party model risk framework that combines elements of traditional MRM with third-party vendor management. Key governance components include: foundation model selection due diligence (performance on relevant financial tasks, provider's own safety mitigations, contractual protections, data handling); contract terms specifying change notification requirements, data prohibition from training use, and incident reporting obligations; independent testing of the model on representative financial service tasks before deployment; ongoing monitoring for behavioral drift; and a model deprecation response plan.

The JPMorgan LLM Suite exemplifies this tier at scale: the platform is model-agnostic, integrating LLMs from both OpenAI and Anthropic, with JPMorgan's own data infrastructure and governance layer providing control regardless of which underlying model is being accessed.

### 4.4 Tier 4: RAG Systems

Retrieval-Augmented Generation systems add retrieval infrastructure to any of the above model tiers, creating a combined governance requirement. In addition to foundation model governance, RAG systems require: corpus curation governance (what documents are ingested, how they are validated, how they are kept current); embedding model validation (does the embedding model correctly represent the semantic content of the financial corpus?); retrieval accuracy testing (does the system retrieve relevant documents rather than semantically adjacent but incorrect ones?); data poisoning controls (is the retrieval corpus protected against malicious content injection?); and ongoing corpus hygiene monitoring. For a cross-reference on RAG-specific security risks including corpus poisoning, see `../standards/owasp_top10_llm.md` (LLM04 â€” Data and Model Poisoning).

### 4.5 Tier 5: Agent Frameworks

AI agents that use LLMs as reasoning engines and interact with external systems represent the highest-risk deployment tier, requiring governance that extends beyond both traditional MRM and Gen AI model governance. Agent governance is treated in depth in [09_agentic_ai_governance.md](09_agentic_ai_governance.md).

---

## 5. Bank Gen AI Governance Structures: Case Studies

### 5.1 JPMorgan Chase

JPMorgan Chase has developed what is arguably the most mature Gen AI governance structure among global banks. The bank's AI/ML governance framework, described in its public "AI and Model Risk Governance" publications, establishes that no AI model can be deployed without registration in the firm's model control process. Developers must document and test their use cases, and all applications must pass through control processes before reaching production.

At the institutional level, JPMorgan's AI strategy is overseen by a C-suite-led AI Governance Council that supervises agentic AI development, operational deployment, and compliance. The Firmwide Chief Data Officer (CDO) function aligns data governance, quality standards, and access patterns with MRM, legal, and security requirements. The bank's annual technology budget reached $17 billion in 2024, with approximately $1.3 billion explicitly dedicated to advancing AI capabilities.

The LLM Suite â€” JPMorgan's proprietary Gen AI platform â€” was initially deployed to 50,000 employees and scaled to over 230,000 by late 2024. The platform is model-agnostic, integrating LLMs from OpenAI and Anthropic, with JPMorgan's own control layer providing governance regardless of underlying model. The firm has publicly acknowledged operating over 450 distinct AI use cases, with plans to expand further into agentic AI configurations.

JPMorgan's governance philosophy is expressed in its public statement: "In banking, we have a dedicated function called Model Risk Governance to assess the risk of each use of ML/AI to ensure the application of this technology does not introduce risks to our customers or to the firm." This extends to LLMs, with the bank requiring adequate testing of each use case and documentation of governance controls.

### 5.2 Goldman Sachs

Goldman Sachs' AI governance framework is built around adaptation of its existing MRM infrastructure for LLM deployments. The firm evaluated and approved AI models under its Model Risk Management (MRM) framework, with bias detection and data lineage tracking implemented for deployed systems. Goldman's GS AI platform serves all 46,500 employees, with internal fine-tuning of LLMs using proprietary codebases to improve relevance for finance-specific tasks.

The firm's risk management priorities for LLMs include in-house capabilities to evaluate AI performance, bias, and drift, with MRM teams co-developing control frameworks alongside data scientists. Goldman's approach emphasizes explainability: in 2025, the bank reduced AI budgets by 15% while shifting focus toward explainable AI (XAI), targeting 92% model transparency â€” a metric that reflects regulatory pressure on black-box AI systems.

Goldman's AI working group conducts model review for LLM deployments, adapting the firm's existing model review standards to the characteristics of foundation models. The review process includes assessment of foundation model selection rationale, validation of use-case-specific performance, and ongoing monitoring protocols.

### 5.3 HSBC

HSBC's approach to Gen AI governance follows a "hub-and-spoke" architecture that is particularly well-suited to the bank's complex multi-jurisdictional structure. Individual business lines and functions serve as "spokes" â€” generating use case ideas, running initial experiments, and submitting proposals to a central "hub" comprising the AI Centre of Excellence and Group-level technology and risk teams.

The governance lifecycle has three stages: experimentation (use case identification with minimal controls), pilot (tightly controlled deployment to limited users with active monitoring), and production (full deployment with ongoing performance monitoring). Use cases must pass through a governance review before transitioning from pilot to production, with the AI Centre of Excellence providing independent assessment.

HSBC's Gen AI risk governance is anchored in its Group AI Review Committee, which was augmented in the first half of 2025 by AI Review Councils embedded across business lines. The bank introduced mandatory Responsible AI training for all staff and established an AI Academy to build capability. HSBC also created the position of Chief AI Officer (effective April 2026), reflecting the elevation of AI governance to C-suite visibility.

The bank's Mistral partnership illustrates its approach to open-source model adoption: rolling out tools from Mistral under its responsible-AI governance framework, with transparency and data protection as explicit requirements.

### 5.4 Citi

Citi's Gen AI governance framework emerged in the context of broader data governance and risk management remediation requirements under regulatory consent orders. The bank deployed AI coding tools to 30,000 developers in 2024 using enterprise-grade platforms and fine-tuned LLMs aligned with internal governance standards. Treasury operations Gen AI tools operate under a governance framework specifying policies for data security, privacy, and model integrity, with audits for fairness and accuracy.

Citi's forward-looking strategy explicitly anticipates agentic AI deployment, with the bank's architecture, data governance frameworks, and talent pipelines explicitly designed for more autonomous AI agents beyond current Gen AI capabilities.

### 5.5 Morgan Stanley

Morgan Stanley's AI governance framework is built on the principle of rigorous testing with human oversight at every stage. Before deployment, every AI use case is subjected to an evaluation (eval) framework that tests models systematically against real-world scenarios, with human experts grading responses for accuracy and coherence.

The AI @ Morgan Stanley Assistant â€” a wealth management tool powered by an OpenAI-backed system â€” underwent rigorous compliance-integrated evaluation. Advisors review and adjust AI-generated outputs before finalizing them, maintaining human-in-the-loop oversight. Daily regression testing using a curated suite of sample questions identifies weaknesses and improves compliance-aligned outputs.

The June 2024 launch of AI @ Morgan Stanley Debrief (automated meeting notes) and October 2024 launch of AskResearchGPT demonstrated the breadth of Morgan Stanley's LLM deployment. In March 2024, the bank appointed 15-year veteran Jeff McMillan as Head of Firmwide Artificial Intelligence, consolidating AI strategy and governance under a single executive. Morgan Stanley also maintains a dedicated "Artificial Intelligence Oversight and Governance" function at Vice President level, tasked with ongoing oversight of AI deployments.

### 5.6 Bank of America

Bank of America's approach to Gen AI governance is characterized by caution about "black box" generative AI for customer-facing applications. The bank chose to build Erica â€” its AI virtual assistant, which has handled over 2.7 billion engagements â€” on a controlled, proprietary platform rather than on a frontier foundation model. BofA executives have explicitly expressed concerns about hallucinations and unpredictability of LLMs for critical financial tasks.

The bank's AI oversight council evaluates capabilities across 16 parameters before approving deployment. Guiding principles include model agnosticism, strong governance enforcing bias control, transparency, and data stewardship, and incremental scaling through pilot projects. The bank achieves a 98% containment rate for Erica interactions, reflecting the robustness of its narrowly scoped, controlled AI system.

Bank of America's approach illustrates a risk-proportionate stance: applying more cautious governance to customer-facing applications while potentially being more permissive for internal productivity tools where the consequence of errors is lower.

### 5.7 Wells Fargo

Wells Fargo's Gen AI governance framework operates in the context of legacy risk management remediation requirements. The bank has developed modular enterprise data science infrastructure supporting governance, transparency, and integration of both internal and third-party models. All AI-driven decisions must be auditable and compliant with regulatory expectations, with particular attention to model documentation and validation rigor given the bank's history of regulatory scrutiny.

---

## 6. The Extended Gen AI Model Lifecycle

Traditional SR 11-7 defines a model lifecycle spanning development, implementation, and use, with ongoing monitoring and validation embedded throughout. For Gen AI systems, this lifecycle requires extension to accommodate new stages and actors.

### 6.1 Stage 0: Foundation Model Selection and Vetting

Before a bank begins building a Gen AI application, it must select a foundation model. This selection is itself a governance decision requiring documentation and approval. Selection criteria include: performance on relevant financial service tasks (measured through independent benchmarking rather than relying on vendor-reported benchmarks); safety and alignment characteristics (how does the model respond to adversarial inputs? what are the vendor's published safety mitigations?); transparency and explainability (does the vendor publish model cards, system cards, or safety evaluations?); data handling practices (will customer data submitted to the API be used for model training?); and contractual protections (change notification requirements, incident reporting, data residency, SLA).

Foundation model transparency is an active area of research. The 2025 Foundation Model Transparency Index evaluated leading foundation models across dozens of transparency dimensions, finding significant variation in disclosure quality. Banks should establish minimum transparency requirements for foundation model providers as a condition of deployment.

### 6.2 Stage 1: Use Case Definition and Risk Classification

Each Gen AI use case must be classified by risk tier before development begins. The classification determines the level of governance overhead and the rigor of subsequent validation. A four-tier risk classification, widely adopted across large banks, is described in Section 7 below.

### 6.3 Stage 2: Prompt Engineering and System Design

The design of the system prompt, conversation flow, and guard rails is a critical governance stage that has no direct analog in traditional MRM. Prompt engineers are effectively defining system behavior â€” a function analogous to model developers in traditional MRM. Governance requirements at this stage include: documentation of prompt design rationale (why specific instructions are included, what risks they mitigate); version control for all prompt templates; adversarial testing of prompts (red-teaming for jailbreaks, indirect injection, and unintended behavior); and approval workflow before deployment to production.

### 6.4 Stage 3: RAG Pipeline Design and Corpus Curation

Where a RAG architecture is used, the retrieval corpus requires governance. This includes: documentation of corpus composition (what sources are included and why); quality assurance for ingested documents (currency, accuracy, authorization to include); embedding model selection and validation; retrieval accuracy testing (does the system retrieve the right documents for representative queries?); and corpus update governance (how are new documents ingested, and is updated ingestion tested before production deployment?).

### 6.5 Stage 4: Independent Validation

Validation of Gen AI systems requires adapting SR 11-7's three validation components â€” conceptual soundness, ongoing monitoring, and outcomes analysis â€” to the characteristics of LLMs. Conceptual soundness assessment for an LLM involves: review of foundation model selection rationale and provider documentation; assessment of the prompt engineering approach against the intended use case; review of guard rail and safety control design; and evaluation of the retrieval pipeline (for RAG systems). Outcomes analysis requires use-case-specific benchmarks, human evaluation panels, and adversarial testing. Ongoing monitoring design must include both quantitative metrics (response latency, error rates, user feedback scores) and qualitative sampling (human review of model outputs).

Red-teaming â€” systematic adversarial testing by teams attempting to elicit harmful or inappropriate outputs â€” has emerged as a critical validation component with no traditional MRM analog. Red teams should include domain specialists (finance, compliance) who can recognize harmful outputs that a general tester might miss.

### 6.6 Stage 5: Deployment with Guardrails

Production deployment of Gen AI systems requires both technical and operational controls. Technical guard rails include: input validation and prompt injection detection; output filtering for prohibited content categories; rate limiting and circuit breakers to prevent runaway generation; and latency monitoring to detect model availability issues. Operational controls include: user disclosure requirements (customers should know they are interacting with AI); escalation paths to human agents; and incident reporting procedures.

### 6.7 Stage 6: Ongoing Monitoring and Model Refresh

The model monitoring obligation under SR 11-7 becomes more complex for Gen AI. Traditional model monitoring focuses on performance metric stability (PSI, KS tests, rejection rates). Gen AI monitoring requires a broader set of metrics: hallucination rate (measured through regular human-labeled sampling or automated LLM-as-judge with calibration); factual accuracy on use-case-specific benchmarks; guard rail bypass rate; user satisfaction and escalation rates; response latency (LLMs are slower than traditional models and performance can degrade); and behavioral drift detection (automated comparison of current outputs against a historical baseline).

Model refresh for Gen AI also differs from traditional practice. Foundation model version updates require re-validation of the dependent system, even if the bank did not initiate the change. This requires contractual change notification from vendors and an internal process to assess re-validation requirements when notifications arrive.

---

## 7. Use Case Governance Categorization

A risk-tiered use case governance framework is the practical foundation for scaling Gen AI governance across hundreds of potential applications. The following four-tier framework reflects emerging industry practice:

### Tier 1: Internal Productivity (Low Risk)

Use cases in this category include code assistants (GitHub Copilot equivalents deployed internally), document summarization tools, meeting note generators, and internal search assistants. The defining characteristics are: outputs are not directly used in customer-facing decisions; errors are correctable by the human user before action is taken; there is no regulatory obligation triggered by outputs; and the scope is limited to internal information retrieval and drafting.

Governance requirements for Tier 1 tools are relatively lightweight: use case documentation, user training on limitations, basic monitoring of usage patterns, and periodic review. Full model validation is not required, but vendor due diligence on the underlying foundation model is still necessary to ensure data handling protections are in place.

### Tier 2: Internal Analytics and Decision Support (Medium Risk)

This tier includes research synthesis tools, regulatory reading and interpretation assistants, risk analysis support, and internal compliance checking tools. Outputs influence â€” but do not replace â€” human judgment in material decisions. Errors may not be immediately apparent to users. There may be regulatory implications if outputs are systematically wrong.

Governance requirements escalate: formal use case approval, documented user guidance on appropriate reliance, validation against a representative benchmark, ongoing accuracy monitoring, and periodic revalidation when model versions change. The key control is ensuring that human decision-makers understand the limitations of the system and do not over-rely on AI outputs without independent verification.

### Tier 3: Customer-Facing Applications (High Risk)

Customer-facing Gen AI â€” chatbots, virtual assistants, advice-generation tools, personalized product recommendation systems â€” carries significantly higher risk because errors directly affect customers and create regulatory exposure. Consumer protection laws (UDAP, FCA Consumer Duty, EU AI Act provisions) impose obligations around accuracy, fairness, and non-discrimination.

Full model governance applies: independent validation including red-teaming, human-in-the-loop requirements for material commitments, robust output monitoring, mandatory disclosure that the customer is interacting with AI, and escalation paths to human agents. Adverse action notice obligations (ECOA/Regulation B) apply where AI outputs influence credit decisions. Regular fairness testing is required to detect disparate impact.

### Tier 4: Autonomous Action (Critical Risk)

Agentic AI that takes actions in external systems â€” executing trades, initiating payments, filing regulatory reports, committing to contractual terms â€” represents the highest-risk Gen AI deployment category. Critical risk governance, including human-in-the-loop design for material actions, kill-switch capability, immutable audit trails, and dedicated agentic AI risk frameworks, is addressed in depth in [09_agentic_ai_governance.md](09_agentic_ai_governance.md).

---

## 8. Gen AI Risk Committee Structures

### 8.1 The Governance Architecture Question

Banks face a structural question when creating Gen AI governance: should they extend the existing Model Risk Committee (MRC) or create a dedicated AI Governance Committee? The answer depends on the bank's existing governance architecture and the maturity of its Gen AI program.

The case for extension is integration: Gen AI risks â€” including model risk, third-party risk, and data risk â€” already have homes in existing risk committees. Creating parallel governance structures risks fragmentation and gaps. The Model Risk Committee has the expertise and standing to evaluate AI systems; what it needs is expanded scope and adapted standards.

The case for a dedicated committee is specialization: Gen AI risks are sufficiently novel â€” encompassing ethics, reputational risk, emerging regulation, and frontier technology â€” that a dedicated forum allows deeper focus. A dedicated AI Council can also include executives from functions (Chief Ethics Officer, Chief AI Officer, General Counsel) who might not typically attend Model Risk Committee meetings.

### 8.2 Industry Practice

In practice, most large banks have adopted a hybrid approach. JPMorgan operates a C-suite-led AI Governance Council that sets firmwide AI strategy and approves major AI initiatives, with the Model Risk Governance function providing technical review of individual AI systems. HSBC has a Group AI Review Committee at the top level, supported by business-line AI Review Councils that provide distributed governance across the hub-and-spoke structure. Morgan Stanley maintains a dedicated AI Oversight and Governance function that interfaces with existing risk governance structures.

The key principle, validated by regulatory feedback at multiple institutions, is that all Gen AI applications must have a clearly identified governance home â€” either within MRM or within a formal AI governance structure that has equivalent rigor. The risk is not in choosing one structure over another; it is in creating coverage gaps where some applications fall between the cracks.

---

## 9. Regulatory Expectations for Gen AI in Banks

### 9.1 US Regulatory Framework

**SR 26-2 (April 2026):** The Federal Reserve, OCC, and FDIC issued revised model risk management guidance in April 2026, superseding SR 11-7. Critically, the revised guidance explicitly places generative AI and agentic AI outside the formal scope of the model risk management framework, noting that "institutions apply their existing risk management practices to govern them" and that "separate guidance or rulemaking will address AI-related risks." In practice, supervisors and internal audit are already applying MRM expectations by analogy to LLM-based systems, and the exclusion is better understood as a placeholder pending dedicated Gen AI guidance rather than a governance exemption.

**2024 AI in Financial Services RFI:** The OCC, Federal Reserve, FDIC, CFPB, and NCUA issued an interagency Request for Information in 2024 on the uses, opportunities, and risks of AI in financial services. The RFI signaled that comprehensive AI-specific guidance is in development and that regulators are actively assessing whether existing frameworks are adequate.

**Federal Reserve Bank of Chicago Tail Risk Paper (2026):** This paper specifically identified GenAI as creating tail risks for banks, with particular attention to third-party concentration risk from banks' dependence on a small number of foundation model providers.

**2021 Interagency AI Statement:** The foundational US regulatory position on AI remained the 2021 Interagency Statement on the Use of AI by Financial Institutions, which applied existing guidance (including SR 11-7) to AI/ML systems and called for enhanced explainability and fairness standards.

### 9.2 UK Regulatory Framework

The FCA has consistently maintained a principles-based, outcomes-focused approach to AI regulation, explicitly declining to introduce AI-specific rules. Its November 2024 AI in UK Financial Services survey (conducted with the Bank of England) found 75% of firms using AI, with foundation models accounting for 17% of use cases. The FCA's position is that firms must demonstrate how AI deployments comply with existing principles â€” particularly around treating customers fairly (Consumer Duty) and managing conflicts of interest â€” rather than following AI-specific prescriptive requirements.

The PRA and FCA's publication of SS6/24 (Critical Third Parties) in November 2024 has particular relevance for Gen AI: if a foundation model provider is deemed to pose financial stability risks, it could be designated as a Critical Third Party subject to direct regulatory oversight. This represents a potential structural intervention in the market for foundation model services.

### 9.3 European Regulatory Framework

**EU AI Act (Regulation EU 2024/1689):** The EU AI Act entered into force in August 2024. For financial services, the critical classification is "high-risk AI" â€” a category that explicitly includes AI systems used to evaluate creditworthiness or establish credit scores. High-risk AI systems face comprehensive requirements: risk management systems, data governance obligations, technical documentation, transparency measures, human oversight, and conformity assessment. The compliance deadline for high-risk AI systems is August 2, 2026, with fines up to â‚¬30 million for non-compliance.

Foundation models and general-purpose AI systems (GPAI) face additional obligations under the EU AI Act: transparency requirements regarding training data, compliance with copyright law, and (for high-capability GPAI models) systemic risk assessments and adversarial testing obligations.

**ECB Internal Models Guide (July 2025):** The ECB published a revised supervisory guide that formally extended model risk management expectations to every model used by institutions, including ML models. A new Chapter 9 specifically addresses machine learning models, requiring higher explainability standards and robust data governance for training data. The ECB's 2024-2025 supervisory reviews conducted targeted reviews of AI use in credit scoring, fraud detection, and generative AI.

**EBA:** The EBA's November 2025 Risk Assessment Report confirmed that national competent authorities will expect supervised institutions to demonstrate progress on EU AI Act compliance by mid-2026. EBA guidance on AI use in supervisory reporting is expected.

### 9.4 Singapore Regulatory Framework

**MAS Model AI Governance Framework:** Singapore's MAS issued its Model AI Governance Framework in 2019 (updated 2020), establishing foundational AI governance expectations for financial institutions. The framework covers AI risk assessment, decision-making processes, governance structure, and consumer communication.

**Singapore Gen AI Framework (May 2024):** IMDA launched the Model AI Governance Framework for Generative AI in May 2024, identifying nine dimensions for comprehensive Gen AI governance: accountability, trusted data sources, trusted development and deployment, incident reporting, testing and assurance, security, content provenance, safety and alignment, and AI safety research. The framework specifically addresses risks including hallucinations, bias, intellectual property, cybersecurity, and systemic risk.

**Singapore Agentic AI Framework (January 2026):** IMDA launched the world's first governance framework specifically designed for agentic AI systems in January 2026 (updated with case studies in May 2026). See [09_agentic_ai_governance.md](09_agentic_ai_governance.md) for coverage.

---

## 10. Third-Party Foundation Model Risk

### 10.1 Vendor Concentration Risk

The foundation model market is currently dominated by a small number of providers: OpenAI (GPT series), Anthropic (Claude series), Google DeepMind (Gemini series), and Meta (open-source Llama series). Most large banks access multiple providers but remain substantially dependent on this concentrated ecosystem. The FSB's November 2024 report on AI financial stability implications explicitly identified third-party dependencies and service provider concentration as a primary vulnerability.

The concentration risk has two dimensions. At the firm level, a bank with hundreds of applications depending on GPT-4o is vulnerable to any availability, quality, or policy disruption affecting that model. At the systemic level, if many banks are running the same model, correlated failures could amplify system-wide stress. The FSB noted that AI may increase market correlations â€” if many institutions use similar models generating similar recommendations, markets could become more susceptible to synchronized behavior.

### 10.2 API Reliability and SLA Considerations

Foundation model APIs are cloud-hosted services subject to the same reliability constraints as any cloud service: planned maintenance, unplanned outages, degraded performance under peak load, and geographic service variations. For banks deploying Gen AI in operational workflows â€” particularly customer service, where response time directly affects customer experience â€” API reliability is a critical risk consideration.

Service level agreements for foundation model APIs typically provide 99.9% availability guarantees at the platform level. However, performance guarantees (latency, throughput) are typically softer, with rate limiting and throttling applied during peak periods. Banks deploying Gen AI in high-volume customer service contexts must design for degraded-mode operation: fallback to traditional rule-based responses when LLM API performance degrades, circuit-breaker patterns to prevent cascading latency, and queuing mechanisms to manage burst traffic.

### 10.3 Contractual Data Handling Protections

The terms under which banks may use foundation model APIs are a critical governance consideration. Enterprise API agreements should specify:

- **Zero-training-data obligation:** Customer data submitted through the API must not be used to train, fine-tune, or improve the provider's foundation models. This is standard in enterprise agreements for major providers but must be confirmed and documented.
- **Data residency:** Where data is processed geographically. This affects GDPR compliance (for EU customer data) and data sovereignty requirements in various jurisdictions.
- **Subprocessor obligations:** Foundation model providers may use third-party infrastructure (cloud compute, specialized hardware) to serve inference requests. Banks must understand this supply chain.
- **Incident reporting:** Requirements for the provider to notify the bank of security incidents, data breaches, or significant behavioral changes within defined timeframes.
- **Audit rights:** Whether the bank has any right to audit the provider's data handling practices.

### 10.4 Foundation Model Deprecation Risk

OpenAI retired GPT-3.5 Turbo in late 2024. Banks that had built applications on this model faced a forced migration â€” revalidating applications against the successor model, potentially updating system prompts and integration code, and managing the transition without service interruption. This experience underscored the importance of model deprecation planning as a standard component of Gen AI governance.

Best practice includes: maintaining validated deployments on pinned model versions rather than floating aliases; monitoring vendor deprecation notices; maintaining test suites that can rapidly assess a successor model's suitability; and including model migration procedures in the Gen AI application's incident response plan.

### 10.5 Regulatory Expectations on Vendor Oversight for AI

Third-party risk management guidance issued by US banking regulators in June 2023 (OCC Bulletin 2023-17) applies to AI vendors, requiring banks to conduct appropriate due diligence before entering relationships, negotiate contracts with appropriate protections, and conduct ongoing monitoring. The FS AI Risk Management Framework (published February 2026 by the Cyber Risk Institute and 108 financial institutions) contains extensive controls specifically for third-party and fourth-party AI oversight, representing the most detailed industry-developed standard for AI vendor due diligence.

Key areas of AI-specific due diligence that extend beyond traditional third-party risk management include: independent testing of vendor AI systems on representative financial task benchmarks; independent bias and hallucination rate testing; assessment of the vendor's own AI safety and governance practices; and review of model card and system card disclosures for transparency.

---

## 11. Emerging Best Practices and Industry Gaps

### 11.1 What Leading Institutions Are Doing Well

Across the major banks, several governance practices have emerged as markers of leadership. The most effective Gen AI governance programs share common characteristics: they are risk-tiered (applying proportionate governance to diverse use cases rather than one-size-fits-all); they treat prompt templates as controlled artifacts; they have invested in dedicated red-teaming capability; they have contracted appropriate protections from foundation model vendors; and they have created clear escalation paths from Gen AI application governance to MRM and ultimately to senior risk committees.

### 11.2 Persistent Industry Gaps

Despite significant progress, several governance gaps remain common across the industry. Hallucination monitoring in production is rarely as rigorous as pre-deployment testing â€” the cost and latency of human-labeled monitoring makes continuous sampling difficult, and automated LLM-as-judge systems introduce circular evaluation risks. Prompt change management is frequently treated as a software engineering concern rather than a model governance concern. Foundation model behavioral drift monitoring is absent at many institutions despite its material governance implications. And the "model within a model" governance question for complex RAG and agent pipelines remains unresolved in most institutions' formal governance frameworks.

---

## 12. Cross-References

- **OWASP Top 10 for LLM Applications** â€” for specific security risk taxonomy including prompt injection, sensitive information disclosure, supply chain risks, and output integrity failures: see `../standards/owasp_top10_llm.md`
- **LLM Risk Taxonomy** â€” for the four-dimension risk framework (Model Risk, Data Risk, Operational Risk, Conduct/Consumer Risk): see [08_llm_risk_taxonomy.md](08_llm_risk_taxonomy.md)
- **Agentic AI Governance** â€” for governance of autonomous AI agents in financial services: see [09_agentic_ai_governance.md](09_agentic_ai_governance.md)
- **SR 11-7 Deep Dive** â€” for the foundational model risk management framework: see [02_sr11_7_deep_dive.md](02_sr11_7_deep_dive.md)
- **Bank MRM Frameworks** â€” for how major banks have operationalized MRM: see [04_bank_mrm_frameworks.md](04_bank_mrm_frameworks.md)
- **Big Tech MRM Guidance** â€” for how technology providers frame AI governance: see [11_big_tech_mrm_guidance.md](11_big_tech_mrm_guidance.md)

---

*Sources consulted: JPMorgan Chase AI and Model Risk Governance public statements; Goldman Sachs AI governance disclosures; HSBC Responsible AI framework and AI governance announcements; Morgan Stanley AI governance and press releases; Bank of America AI oversight publications; FSB Financial Stability Implications of AI (November 2024); NIST AI 600-1 Generative AI Profile (July 2024); OCC/Fed/FDIC SR 26-2 Model Risk Management Guidance (April 2026); EU AI Act (Regulation EU 2024/1689); ECB Supervisory Guide to Internal Models (July 2025); MAS Model AI Governance Framework for Generative AI (May 2024); Singapore Agentic AI Framework (January 2026); Bank of England/FCA AI in UK Financial Services Survey (November 2024); Federal Reserve Bank of Chicago Tail Risk Paper (2026); US Treasury Financial Services AI RMF (February 2026); Deloitte Agentic AI Risks in Banking (2025).*

