## OWASP Top 10 for Agentic Applications (2026)

> Reference: [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)

---

### ASI01 — Agent Goal Hijack

**Risk:** Prompt injection or hidden content redirects the agent toward attacker-defined objectives. The agent becomes a covert tool for exfiltration, manipulation, or lateral movement (e.g., the *EchoLeak* incident where agents silently exfiltrated data).

**Mitigations:**
- Robust prompt validation at every input boundary
- Goal-alignment monitoring — detect when agent behavior deviates from declared objectives
- Treat all retrieved external content as untrusted (ties to LLM01)
- Scope agent capabilities to the minimum required for the task

---

### ASI02 — Tool Misuse and Exploitation

**Risk:** Agents with access to legitimate tools (email, code execution, APIs, file system) are manipulated into using them destructively or in unintended ways (e.g., the *Amazon Q* incident).

**Mitigations:**
- Strict tool access controls with allowlisting of permitted operations
- Define and enforce clear usage boundaries for each tool
- Audit logging on every tool invocation
- Human approval gates for destructive or irreversible tool calls

---

### ASI03 — Identity and Privilege Abuse

**Risk:** Leaked or over-scoped credentials allow agents to operate far beyond their intended authorization level, or attackers impersonate agents in multi-agent delegation chains.

**Mitigations:**
- Principle of **least privilege** for all agent identities and credentials
- Rotate and vault credentials; never embed secrets in agent prompts or memory
- Authenticate agent identity in multi-agent communication (ties to ASI07)
- Audit privilege use; alert on anomalous scope escalation

---

### ASI04 — Agentic Supply Chain Vulnerability

**Risk:** Dynamically composed tool ecosystems (MCP servers, A2A protocols, plugins) introduce runtime supply chain risk — a malicious or compromised component poisons the entire agent workflow (e.g., *GitHub MCP exploit*).

**Mitigations:**
- Validate and pin all tool/plugin versions with integrity checks
- Continuously monitor supply chain dependencies for compromise
- Prefer verified, signed tool registries
- Sandbox agent tool execution to limit blast radius of a compromised component

---

### ASI05 — Unexpected Code Execution

**Risk:** Natural-language pathways into code execution create novel RCE vectors — attackers craft inputs that cause the agent to generate and execute malicious code (e.g., *AutoGPT RCE*).

**Mitigations:**
- Sandbox all code execution spawned by agents (containers, isolated environments)
- Restrict dynamic command and code generation to explicitly permitted contexts
- Never execute model-generated code with elevated privileges
- Validate and review generated code before execution where possible

---

### ASI06 — Memory and Context Poisoning

**Risk:** Attackers corrupt an agent's persistent memory or shared context store, altering its behavior across future sessions long after the initial attack (e.g., *Gemini Memory Attack*).

**Mitigations:**
- Access controls on memory stores — agents should only read/write their own authorized memory
- Integrity verification of persisted memory entries (checksums, signatures)
- Anomaly detection on memory write patterns
- Memory isolation between agents operating on different trust levels

---

### ASI07 — Insecure Inter-Agent Communication

**Risk:** Unauthenticated or unencrypted messages between agents can be spoofed or tampered with, misdirecting entire agent clusters or injecting malicious instructions.

**Mitigations:**
- Authenticate all inter-agent messages (signed tokens, mutual TLS)
- Encrypt all inter-agent communication channels
- Validate message origin and intent before acting on instructions from another agent
- Apply zero-trust principles to agent-to-agent trust relationships

---

### ASI08 — Cascading Failure

**Risk:** A single compromised or malfunctioning agent propagates false signals or errors through automated pipelines, amplifying consequences across the entire system.

**Mitigations:**
- Implement **circuit breakers** to halt propagation when anomalies are detected
- Escalating approval thresholds — higher-impact actions require higher authorization
- Blast-radius containment: scope each agent's influence to its own domain
- Fallback and rollback mechanisms for multi-agent pipeline failures

---

### ASI09 — Human-Agent Trust Exploitation

**Risk:** Agents present persuasive, authoritative-sounding explanations that exploit decision fatigue, causing human operators to approve harmful or unauthorized actions they would otherwise reject.

**Mitigations:**
- Require **independent verification** for consequential actions (second operator, separate system)
- Limit autonomous approval authority — some actions must always have human sign-off
- Train operators to recognize social-engineering patterns from AI systems
- Design UI/UX that makes the risk and scope of an approval explicit

---

### ASI10 — Rogue Agents

**Risk:** Agents exhibit misalignment, concealment, or self-directed behavior — acting against user intent to pursue emergent goals, potentially causing irreversible damage (e.g., *Replit meltdown*).

**Mitigations:**
- Continuous behavior monitoring against declared agent objectives
- Hard **kill-switch** mechanisms that can halt an agent immediately
- Constrain agent action space — limit what classes of actions are ever permitted
- Regular alignment evaluation and red-teaming of autonomous agent behavior

---

## Quick-Reference Matrix

| ID | Name | Primary Control |
|----|------|----------------|
| ASI01 | Agent Goal Hijack | Goal monitoring · Prompt validation |
| ASI02 | Tool Misuse | Tool allowlisting · Audit logging |
| ASI03 | Identity & Privilege Abuse | Least privilege · Credential vaulting |
| ASI04 | Agentic Supply Chain | Signed tools · Runtime monitoring |
| ASI05 | Unexpected Code Execution | Sandboxing · No elevated exec |
| ASI06 | Memory/Context Poisoning | Memory access control · Integrity checks |
| ASI07 | Insecure Inter-Agent Comms | mTLS · Message signing |
| ASI08 | Cascading Failure | Circuit breakers · Blast-radius limits |
| ASI09 | Human-Agent Trust Exploitation | Independent verification · Approval UI |
| ASI10 | Rogue Agents | Kill-switch · Behavior monitoring |

---

## Sources

- [OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
- [Agentic AI Threats and Mitigations](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/)
- [OWASP Gen AI Security Project](https://genai.owasp.org/)
