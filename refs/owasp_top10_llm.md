# OWASP GenAI Security Reference

> Source: [OWASP Gen AI Security Project](https://genai.owasp.org)
> Last reviewed: 2025 (LLM Top 10 v2025) · 2026 (Agentic Top 10)

---

## OWASP Top 10 for LLM Applications (2025)

### LLM01 — Prompt Injection

**Risk:** Crafted inputs override system instructions, causing unauthorized access, data exfiltration, or harmful actions. Attacks are *direct* (user prompt) or *indirect* (malicious content embedded in documents, web pages, or tool outputs the model reads).

**Mitigations:**
- Model Gateway / guardrail layer to inspect request and response content
- Treat all external content retrieved by the model as untrusted; sanitize before passing to the model context
- Privilege separation — the model should not hold elevated credentials
- Continuous red-teaming and adversarial prompt testing

---

### LLM02 — Sensitive Information Disclosure

**Risk:** LLMs memorize or regurgitate training data, system prompts, or user context, leaking PII, credentials, business data, or model internals.

**Mitigations:**
- Minimize data collection; apply data minimization at ingestion
- Role-based access control on what context the model can see
- Output monitoring and DLP (Data Loss Prevention) on responses
- Differential privacy techniques during training/fine-tuning
- AI Security Posture Management (AI-SPM) to audit model data exposure

---

### LLM03 — Supply Chain

**Risk:** Compromised foundation models, fine-tuning datasets, third-party APIs, RAG data sources, or plugins introduce malicious behavior that is extremely hard to detect post-deployment.

**Mitigations:**
- Vet and verify all data suppliers and model providers before use
- Maintain an **AI Bill of Materials (AI-BOM)** — track every model, dataset, plugin, and API dependency
- Pin model versions with checksum validation; prefer signed artifacts
- Continuous scanning of dependencies for known vulnerabilities
- Red-team supply chain components as part of the CI/CD pipeline
- Apply patch and update policies for third-party model components

---

### LLM04 — Data and Model Poisoning

**Risk:** Adversarial or backdoor data inserted into pre-training, fine-tuning, or embedding pipelines causes the model to produce biased, manipulated, or malicious outputs at inference time.

**Mitigations:**
- Trace and verify the provenance of all training and fine-tuning data
- Access control and change control on training pipelines and datasets
- Anomaly detection on training data and model outputs during evaluation
- Continuous model evaluation after any data or parameter update

---

### LLM05 — Improper Output Handling

**Risk:** LLM outputs passed unsanitized to downstream systems enable XSS, SQL injection, command injection, or remote code execution.

**Mitigations:**
- Validate and sanitize all LLM outputs before passing to browsers, databases, or shells
- Treat model output as untrusted user input in downstream components
- Sandbox execution environments that consume model output
- Output monitoring for known injection payloads

---

### LLM06 — Excessive Agency

**Risk:** An LLM granted too much autonomy — over tools, APIs, file systems, or external services — can be manipulated or malfunction, causing unintended destructive actions.

**Mitigations:**
- Apply **least privilege** — scope tool and API access to the minimum required
- Require human-in-the-loop confirmation for high-impact actions
- Rate-limit the number of actions an LLM can perform per session
- Log and monitor all autonomous actions for anomaly detection

---

### LLM07 — System Prompt Leakage

**Risk:** Hidden instructions (system prompts) containing credentials, business logic, or security policies can be extracted by adversarial queries or side-channel analysis.

**Mitigations:**
- Never store secrets (API keys, passwords) in system prompts
- Apply output masking to suppress system prompt echoing
- Use randomized or indirect prompt references rather than verbatim secrets
- Monitor outputs for patterns that indicate prompt extraction attempts

---

### LLM08 — Vector and Embedding Weaknesses

**Risk:** Weaknesses in RAG pipelines, vector databases, or embedding generation enable embedding poisoning, similarity-based data retrieval attacks, and embedding inversion.

**Mitigations:**
- Validate and sanitize all documents before they are embedded and stored
- Enforce access controls on vector databases (users should only retrieve content they are authorized to see)
- Regularly audit and validate knowledge base integrity
- Monitor retrieval patterns for anomalous or adversarial queries

---

### LLM09 — Misinformation

**Risk:** LLMs generate or amplify false, fabricated, or misleading content (hallucinations), compromising decision-making, spreading disinformation, or creating legal liability.

**Mitigations:**
- Require human review for high-stakes or safety-critical outputs
- Integrate automated fact-checking and grounding against authoritative sources
- Apply retrieval-augmented generation (RAG) to anchor responses to verified data
- Disclose to end users that outputs may be inaccurate; implement confidence scoring

---

### LLM10 — Unbounded Consumption

**Risk:** Uncontrolled resource use — from prompt flooding, recursive loops, or expensive inference — leads to Denial of Service (DoS) or Denial of Wallet (DoW).

**Mitigations:**
- Enforce per-user and per-application **rate limiting**
- Set token, compute, and cost quotas at the API/gateway layer
- Monitor for request patterns indicative of abuse or automation
- Protect autoscaling configurations to prevent runaway cost growth

---

## Quick-Reference Matrix

| ID | Name | Primary Control |
|----|------|----------------|
| LLM01 | Prompt Injection | Input/output validation · Model gateway |
| LLM02 | Sensitive Info Disclosure | Access control · DLP · AI-SPM |
| LLM03 | Supply Chain | AI-BOM · Provenance · Scanning |
| LLM04 | Data & Model Poisoning | Data provenance · Change control |
| LLM05 | Improper Output Handling | Output sanitization · Sandboxing |
| LLM06 | Excessive Agency | Least privilege · Rate limiting |
| LLM07 | System Prompt Leakage | Masking · No secrets in prompts |
| LLM08 | Vector/Embedding Weaknesses | Vector DB access control · Input validation |
| LLM09 | Misinformation | RAG grounding · Human review |
| LLM10 | Unbounded Consumption | Rate limiting · Cost quotas |
---


## Sources

- [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/resource/owasp-top-10-for-llm-applications-2025/)
- [Agentic AI Threats and Mitigations](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/)
- [OWASP Gen AI Security Project](https://genai.owasp.org/)
