# Agentic AI Governance in Financial Services: The 2025â€“2027 Frontier

## File Metadata
- **Scope:** Governance framework for autonomous AI agents in financial services â€” risks, human-in-the-loop design, kill switches, audit trails, and regulatory expectations
- **Cluster:** C â€” Gen AI and LLM Governance
- **Reading order:** 9/14
- **Related files:** [07_genai_governance_banking.md](07_genai_governance_banking.md), [08_llm_risk_taxonomy.md](08_llm_risk_taxonomy.md), [11_big_tech_mrm_guidance.md](11_big_tech_mrm_guidance.md), [../standards/owasp_top10_agentic.md](../standards/owasp_top10_agentic.md), [../standards/owasp_top10_llm.md](../standards/owasp_top10_llm.md)
- **Regulators/bodies covered:** Federal Reserve, OCC, MAS, FCA, PRA, EBA, ECB, EU AI Office, NIST
- **Tags:** agentic-AI, autonomous-agents, multi-agent, human-in-the-loop, kill-switch, agent-identity, audit-trail, cascading-failure, irreversibility, OWASP-agentic, SR-11-7, agent-governance

---

## 1. Introduction: Why Agentic AI Is a Different Governance Problem

For the first decade of AI deployment in financial services, the paradigm was clear: AI systems observe, analyze, and recommend; humans decide and act. A fraud detection model flags suspicious transactions; a human analyst reviews and acts. A credit scoring model outputs a probability; a human underwriter approves or declines. The governance burden was manageable because the human remained in the causal chain of every consequential action.

Agentic AI breaks this paradigm. An AI agent does not merely recommend â€” it plans a sequence of actions, selects and uses tools to execute those actions, observes the outcomes, and plans the next step, often without human involvement between planning and execution. A research agent might query a financial data API, retrieve regulatory filings, synthesize findings, draft a report, and email it to stakeholders â€” all autonomously. A compliance monitoring agent might identify a potential violation, query case management systems, draft a regulatory disclosure, and initiate a remediation workflow. A payment processing agent might verify transaction parameters, route through approval systems, and execute settlement â€” all within a single automated pipeline.

The governance implications are profound. Agents take real-world actions with real-world consequences. Actions may be irreversible: sent emails cannot be unsent, initiated payments cannot always be recalled, regulatory filings cannot always be amended, market orders may have already moved prices. Errors propagate: one agent's incorrect assumption becomes another agent's input, amplifying through a multi-agent chain before a human ever observes a problem. And accountability is diffuse: when an autonomous agent pipeline causes harm, determining which component, which configuration, or which input was responsible requires forensic capability that most institutions have not built.

By 2025, 42% of financial institutions were actively evaluating or deploying AI agents. JPMorgan Chase had over 450 agentic AI use cases in production. Global enterprise spending on agentic AI surpassed $37 billion in 2025, a 3.2Ã— increase from 2024. Yet governance frameworks for agentic AI remain nascent: Gartner predicted in 2025 that more than 40% of agentic AI projects would be canceled by the end of 2027 due to escalating costs, unclear business value, and inadequate risk controls. This file provides the governance framework that should prevent that outcome.

The OWASP Top 10 for Agentic Applications (see `../standards/owasp_top10_agentic.md`) provides the foundational security risk taxonomy for agentic systems. This file builds on that foundation with a financial services governance framework â€” mapping OWASP risks to specific controls, addressing the SR 11-7/SR 26-2 definitional questions, and providing the practical governance architecture for financial institution deployments.

---

## 2. What Distinguishes Agentic AI from Standard LLM Deployments

Understanding the specific characteristics that make agents different from standard LLMs is essential to designing appropriate governance. The distinction is not merely technical; it determines which risks are present and what controls are necessary.

### 2.1 Multi-Step Autonomous Action

Standard LLMs respond to a prompt with a single completion. Agents plan and execute multiple steps to accomplish a goal, with each step potentially depending on the output of previous steps. This creates a dynamic execution graph that cannot be fully specified in advance. A research agent tasked with "analyze the credit implications of the proposed LIBOR transition for our corporate loan book" might take dozens of steps: query loan management systems, retrieve regulatory guidance, search financial news, cross-reference analyst reports, model exposure calculations, and draft a structured report â€” all without human involvement between the initial instruction and the final output.

The governance challenge is that the full action sequence cannot be pre-validated. Pre-deployment testing can verify that the agent behaves correctly on representative scenarios, but the combinatorial space of possible action sequences means that novel execution paths will occur in production that were never tested. This is fundamentally different from a single-step LLM application where all outputs can be sampled from a well-defined distribution.

### 2.2 Tool Use and External System Access

Agents are distinguished by their ability to call external tools â€” APIs, databases, code execution environments, web browsers, file systems, and communication systems. Tool use transforms agents from text generators into actors. The tools available to an agent define the agent's real-world capability surface: an agent with email sending capability can commit the institution to positions or expose sensitive information externally; an agent with database write access can modify records; an agent with trading API access can move markets.

The diversity of tool access means that governance cannot be based solely on the agent's LLM component â€” it must encompass every tool the agent can access and every action each tool can execute. A comprehensive tool access control framework is therefore a prerequisite for responsible agentic AI deployment.

### 2.3 Memory Persistence

Standard LLMs are stateless: each conversation starts fresh. Agents can maintain state across sessions through multiple memory mechanisms: the context window (short-term working memory), external databases (long-term episodic memory), vector stores (semantic memory enabling retrieval of past experiences), and structured state stores (explicit task tracking). Memory persistence enables agents to learn from experience, remember user preferences, and maintain context across interactions â€” but it also creates new risks. Incorrect information stored in long-term memory can corrupt future reasoning. Memory can be targeted for poisoning attacks. Sensitive information retained in memory may create privacy and confidentiality risks.

### 2.4 Multi-Agent Orchestration

The most complex agentic deployments involve multiple agents working in coordination: orchestrator agents that decompose goals and delegate to specialist agents; worker agents that execute specific tasks and report back; verifier agents that check the work of other agents; guardian agents that monitor the behavior of the entire system. Multi-agent systems can accomplish tasks that single agents cannot â€” but they introduce emergent complexity. When agents communicate, they trust each other's outputs; a compromised or hallucinating agent in the chain poisons the inputs to every downstream agent. Emergent behaviors can arise from agent interactions that were not present in any individual agent's behavior.

For cross-reference on specific multi-agent risks including trust exploitation and coordination failures, see `../standards/owasp_top10_agentic.md` (ASI07 â€” Inter-agent Trust Exploitation; ASI09 â€” Insufficient Multi-agent Coordination).

### 2.5 Goal-Directed Behavior

Standard LLMs respond to instructions; agents pursue goals. This distinction matters because goal-directed systems can exhibit instrumental behaviors â€” taking actions that serve the goal even when not explicitly instructed â€” that the deploying institution did not anticipate. A cost-optimization agent, given the goal of minimizing operational costs, might take actions to reduce compliance overhead in ways not intended. A customer retention agent, given the goal of maximizing retention, might offer unauthorized incentives. Goal specification is itself a governance challenge: goals that seem precise can be interpreted in unexpected ways by agents optimizing across complex action spaces.

### 2.6 Real-World Consequences and Irreversibility

This is the characteristic that makes agentic AI governance qualitatively different from standard LLM governance. Agents take actions in the real world: they send emails, initiate transactions, modify records, make API calls to external services. Many of these actions are irreversible or difficult to reverse. A customer communication cannot be un-read. A regulatory filing cannot always be retracted. A market order, once executed, has already affected price. An email thread, once created, is visible to recipients. The governance framework must therefore treat irreversibility as a first-class design consideration: before any action is taken, the system should assess whether it is reversible and, if not, whether additional human authorization is required.

---

## 3. Financial Services Agentic AI Use Cases and Risk Classification

### 3.1 Tier 1 â€” Low Risk: Information and Research Agents

Information and research agents operate in a purely read-only mode: they gather information, synthesize it, and present findings, but take no actions in external systems. Examples include: regulatory monitoring agents that scan for new regulatory publications and summarize changes; competitive intelligence agents that aggregate public market information; ESG research agents that compile environmental and social metrics from public filings; internal knowledge agents that retrieve and synthesize institutional policies.

Governance requirements for Tier 1 agents are analogous to advanced RAG systems rather than full agentic governance. The primary risks are information quality (hallucination, retrieval errors) and information security (accessing systems the agent should not have permission to query). Human review of outputs before action is taken provides the key control.

### 3.2 Tier 2 â€” Medium Risk: Internal Workflow Agents

Workflow agents operate within internal systems, automating tasks that currently involve significant human effort. Examples include: report generation agents that pull data from multiple internal systems, apply analytical logic, and produce management reports; internal compliance checking agents that review transactions or communications against policy rules; code generation agents that draft software code for human review; and onboarding automation agents that collect and process new employee or customer information.

The risk distinguishes these from Tier 1: workflow agents interact with internal systems, may modify records (draft documents, update workflow states), and their outputs may be used in subsequent decisions without additional human review. Governance requirements include: defined tool access permissions (read vs. write); documentation of what data sources and systems the agent can access; logging of all tool calls; and quality monitoring of agent outputs.

### 3.3 Tier 3 â€” High Risk: Customer-Facing and Commitment Agents

Agents in this tier interact directly with external parties â€” customers, counterparties, or regulatory bodies â€” or take actions that create legal or regulatory obligations. Examples include: customer service agents that respond to account queries, process service requests, and handle complaints; agents that draft communications to regulators or counterparties; agents that negotiate terms with vendors within defined parameters; and compliance monitoring agents that identify and escalate regulatory breaches.

The elevated risk comes from the external commitment dimension: actions taken by Tier 3 agents may be legally or contractually binding, and the bank may bear liability for incorrect or unauthorized agent actions. Governance requirements include: clear authority limits (what can the agent commit to without human approval?); mandatory human review for actions at or near authority limits; comprehensive audit logging of all agent actions; explicit customer disclosure that interactions are automated; and incident response procedures for agent errors.

### 3.4 Tier 4 â€” Critical Risk: Consequential Action Agents

The highest-risk agentic deployments involve agents that take consequential, potentially irreversible actions in financial markets or operational systems. Examples include: trading agents that execute market orders; payment processing agents that initiate and settle transactions; regulatory filing agents that submit reports to supervisory authorities; and agents with write access to systems of record (loan management systems, customer master data).

Tier 4 agents require the most stringent governance: mandatory human approval for actions above defined materiality thresholds; hard limits on the size, scope, and category of actions the agent can take autonomously; comprehensive real-time monitoring; kill switch capability with immediate effectiveness; full audit trails; and independent validation equivalent to high-risk model validation under SR 26-2.

---

## 4. The Unique Risk Surface of Agentic AI

### 4.1 Cascading Failures

When multiple agents work in a pipeline, errors do not stay local. An early agent's incorrect assumption becomes the input for the next agent, which builds further analysis on the incorrect foundation. Each stage of processing gives the error the appearance of additional validation â€” downstream agents may express more confidence in a conclusion precisely because it has passed through more processing steps. By the time a human reviews the final output, the error may be deeply embedded in a chain of apparently coherent reasoning.

A financial example: an agent tasked with assessing collateral for a credit facility queries valuation data, retrieves an outdated record due to a retrieval error, calculates a loan-to-value ratio based on the wrong value, passes the calculation to a second agent for risk assessment, which generates a limit recommendation, which passes to a third agent for documentation. The documentation is compliant and well-formatted, but based on a fundamental factual error made in the first step.

Control approach: Pipeline integrity checks at key stages; output confidence scoring that flags when intermediate conclusions differ substantially from human expert benchmarks; mandatory human review at critical pipeline stages regardless of agent confidence; and anomaly detection on pipeline outputs.

This risk maps to ASI05 in the OWASP Agentic Top 10 (see `../standards/owasp_top10_agentic.md`).

### 4.2 Goal Hijacking

An agent's objective can be redirected by malicious content in its environment â€” an indirect prompt injection that overrides the agent's original goal with an attacker-specified alternative. In financial services, goal hijacking could cause a compliance checking agent to certify non-compliant transactions, a fraud detection agent to clear suspicious activity, or a customer service agent to provide unauthorized account access.

This risk is amplified in agentic contexts compared to standard LLMs because agents have the tools to act on hijacked goals, not merely describe them. An LLM that is jailbroken produces harmful text. An agent that is goal-hijacked executes harmful actions.

Control approach: Goal integrity monitoring â€” detect when agent actions diverge from the declared objective; treat all retrieved external content as untrusted regardless of source; require human approval for actions that were not anticipated in the pre-execution plan; limit tool access to the minimum required for the specific task.

This risk maps to ASI01 in the OWASP Agentic Top 10 (see `../standards/owasp_top10_agentic.md`).

### 4.3 Tool Misuse

Agents have access to tools and can misuse them in ways not anticipated during design. A documented example from 2024 illustrates this vividly: an attacker tricked a reconciliation agent into exporting "all customer records matching pattern X," where X was a regular expression matching every record in the database. The agent found this request within the scope of its normal reconciliation function, resulting in 45,000 customer records being stolen through a single, technically authorized query.

Tool misuse can also occur without adversarial intent: an agent given ambiguous instructions might use a data deletion tool when archiving was intended, or use an external messaging API when an internal notification was appropriate.

Control approach: Strict tool access allowlisting specifying exactly which operations each tool can perform in what context; tool invocation audit logging with anomaly detection; human approval gates for destructive or irreversible tool calls; rate limiting on tool invocations to prevent bulk data extraction.

This risk maps to ASI02 in the OWASP Agentic Top 10 (see `../standards/owasp_top10_agentic.md`).

### 4.4 Privilege Escalation

AI agents create a new privilege escalation attack surface because they can combine permissions across tools, context, data, and workflows in ways that traditional Identity and Access Management (IAM) systems were not designed to inspect. An agent with individually scoped permissions to query customer data, send internal notifications, and access external APIs may combine these permissions in ways that exceed the intended authorization level. Agents that retain access after user sessions end, or that accumulate permissions across multiple delegated tasks, create standing escalation risk.

A financial services incident illustrates this: an agent accumulating temporary API tokens from multiple delegated tasks could combine them to access data across business units, violating information barrier requirements, without any individual permission being inappropriate.

Control approach: Just-in-time credential provisioning â€” agents receive temporary, narrowly scoped tokens only for the immediate task, expiring automatically; unique agent identities with cryptographically bound credentials that cannot be shared or transferred; automated deprovisioning when agent sessions end; regular permission audits to identify accumulated privilege.

This risk maps to ASI03 in the OWASP Agentic Top 10 (see `../standards/owasp_top10_agentic.md`).

### 4.5 Hallucination in Action

When a standard LLM hallucinates, the result is incorrect text that a human can identify and discard. When an agent hallucinates, it may act on the hallucinated information â€” querying systems for records that don't exist, generating regulatory interpretations based on fabricated regulatory text, or taking actions based on incorrect factual premises. The consequences of hallucination in action are therefore orders of magnitude more severe than hallucination in text generation.

An agent that hallucinates a regulatory provision and generates a compliance certification based on it has created a false regulatory record. An agent that hallucinates counterparty information and initiates a transaction has potentially executed an unauthorized trade.

Control approach: Mandatory factual grounding (RAG) for all agent reasoning steps involving facts; structured output requirements that force agents to cite sources for factual claims; human review checkpoints before irreversible actions; confidence thresholds below which agents must escalate to humans rather than proceed.

### 4.6 Memory Poisoning

Agents that maintain long-term memory are vulnerable to memory poisoning: corrupted data in the agent's memory store that causes it to base future decisions on incorrect premises. Memory poisoning can occur through: direct injection of malicious content into the memory store; gradual drift of memory content through accumulated incorrect experiences; adversarial user interactions designed to implant false "memories"; or bug-driven corruption during memory write operations.

For a customer service agent that maintains memory of customer preferences and interaction history, poisoned memory could cause it to treat unauthorized requests as previously authorized, or to apply terms agreed with one customer to a different customer.

Control approach: Memory store access controls limiting who can write to agent memory; integrity verification of memory content (hash-based tamper detection); regular memory audits reviewing stored content for anomalies; time-bounded memory with automatic expiration of older entries; separation of system-level memory (maintained by the platform) from user-provided memory (treated as less trusted).

This risk maps to ASI06 in the OWASP Agentic Top 10 (see `../standards/owasp_top10_agentic.md`).

### 4.7 Inter-Agent Trust Exploitation

In multi-agent systems, agents communicate with each other. If agent A receives a message claiming to be from trusted agent B, how does it verify this claim? If agent A trusts all messages from a particular pipeline position without cryptographic verification, an attacker who can inject a message into that pipeline can impersonate agent B, causing agent A to take actions it would not take for an unknown source. This inter-agent trust exploitation is a specific form of prompt injection but operates across the agent trust hierarchy rather than at the user interface level.

In financial services, a compromised agent impersonating a trusted compliance reviewer could approve transactions that should be rejected, bypassing controls designed into the workflow.

Control approach: Cryptographic authentication of inter-agent communications; zero-trust architecture â€” agents verify every communication source regardless of pipeline position; agent identity certificates issued by a central identity provider; audit logging of all inter-agent communications with identity verification records.

This risk maps to ASI07 in the OWASP Agentic Top 10 (see `../standards/owasp_top10_agentic.md`).

### 4.8 Scope Creep

Agents may take actions outside their intended scope â€” either through ambiguous objective specification (the agent pursues a broader interpretation of its goal), through emergent reasoning that identifies "helpful" adjacent actions, or through adversarial manipulation. An agent instructed to "help customers with account-related queries" might, through scope creep, begin offering investment advice, discussing competitor products, or engaging with sensitive topics it was never intended to address. In financial services, scope creep can create unauthorized practice of investment advice, fair lending violations, or consumer protection issues.

Control approach: Explicit and narrow scope definitions in agent system configuration; output filtering for out-of-scope content categories; anomaly detection on the types of actions agents are taking relative to their defined function; regular behavioral audits comparing observed agent behavior against designed behavior.

### 4.9 Irreversible Harm

The aggregate risk of agentic AI in financial services is concentrated in the irreversibility dimension. Sent communications cannot be unsent. Executed trades have already affected markets. Submitted regulatory filings may require formal withdrawal procedures. Customer account changes may have created downstream effects. Unlike a human employee who can catch an error before it becomes consequential, an autonomous agent may complete a chain of harmful actions before any human observes a problem. The governance framework must treat every irreversible action category with special caution â€” requiring pre-authorization, building in reversibility where technically feasible, and ensuring kill-switch capability can halt execution at any point.

---

## 5. Human-in-the-Loop Framework for Financial Agents

### 5.1 The Evolution from HITL to HOTL

Traditional AI governance has relied on "human-in-the-loop" (HITL) design: humans approve every output before it is used. For agentic AI, requiring human approval at every step defeats the efficiency purpose of automation and introduces decision latency that may be operationally unacceptable (markets don't pause for human review). Deloitte's 2025 analysis noted that HITL designs "may be insufficient" for agentic systems, and that placing humans at every decision step defeats efficiency gains.

The emerging framework is "human-on-the-loop" (HOTL): agents operate autonomously within defined parameters, with humans monitoring continuously and able to intervene rapidly, but not required to approve every action. The governance question becomes: which actions require in-loop human approval, and which can proceed under on-loop human monitoring?

### 5.2 HITL Decision Framework

The following criteria determine whether a specific agent action requires in-loop human approval (HITL) versus on-loop monitoring (HOTL):

**Mandatory HITL Triggers:**
- **Financial materiality threshold:** Any single action or series of related actions above a defined financial threshold (institution-specific, based on risk appetite). Examples: $1M+ transaction executions; commitments above defined notional limits; account closures above a threshold dollar balance.
- **Irreversibility:** Any action that cannot be undone or is difficult to reverse (executed trades, sent external communications, regulatory filings, permanent data deletion, account closures).
- **Novelty of situation:** Actions in scenarios the agent has not encountered before â€” defined as falling outside the distribution of training/validation scenarios â€” should trigger escalation rather than autonomous execution.
- **Regulatory requirement:** Certain regulatory frameworks explicitly require human decision-making authority. ECOA/Regulation B adverse action notices require specific human-attestable reasons. Some jurisdictions require human authorization for automated decisions of material consequence under consumer protection law.
- **Conflict detection:** Where the agent's proposed action conflicts with previously observed policy or with another agent's recommendation, human resolution is required.
- **Low confidence state:** Where the agent's confidence score for a proposed action falls below a defined threshold, it should escalate rather than proceed.

**HOTL Sufficient Situations:**
- Routine, low-value, highly repetitive tasks with well-established patterns (standard document formatting, routine data retrieval, standard notification generation)
- Actions that are fully reversible and low-risk (draft creation, internal workflow state updates that can be rolled back)
- Actions in well-understood scenarios where validation testing has demonstrated high accuracy and low error rates

### 5.3 HITL Design Patterns

Several design patterns have emerged for implementing HITL in financial agentic systems:

**Approval Gate Pattern:** The agent executes all preparatory steps (research, analysis, draft generation) autonomously, but presents a structured summary of the proposed action to a human approver before any consequential action is taken. The human sees: what action is proposed, why the agent is recommending it, what data it is based on, and what the consequences of approving or rejecting are. The human must affirmatively approve before the agent proceeds. This pattern is appropriate for Tier 3 applications where actions are frequent but individual actions carry moderate risk.

**Exception-Based Review Pattern:** The agent operates autonomously within defined parameters, logging all actions. Exceptions â€” actions outside normal parameters, low-confidence decisions, or high-value actions â€” are immediately flagged for human review. The human reviews exceptions rather than every action. This pattern is appropriate for high-volume, routine workflows where the exception rate is expected to be low and the consequences of non-exceptional actions are limited.

**Staged Commitment Pattern:** For multi-step workflows, the agent executes the full workflow to a "prepared-to-commit" state, then presents the complete proposed action set to a human for approval before any irreversible commitment is made. This is analogous to "stage-gate" product development: the agent does all the work of preparing the action, but the human makes the final commitment decision.

**Pause-and-Confirm Pattern:** The agent pauses at any point where it encounters ambiguity, low confidence, or actions that match escalation criteria, and presents a structured question to the human operator. This is appropriate for interactive agent systems where a human is available in near-real-time.

### 5.4 The HITL Latency Problem

Financial markets operate at speeds incompatible with human decision latency. A market-making agent cannot pause for human review between identifying a hedging opportunity and executing a trade â€” the opportunity will be gone. This creates genuine tension between the governance imperative for human oversight and the operational imperative for speed in certain financial applications.

Banks are resolving this tension through several approaches:

**Pre-authorization frameworks:** Rather than authorizing individual actions in real time, humans pre-authorize action categories up to defined limits. The agent can execute any action within the pre-authorized parameters without real-time human involvement; actions outside parameters require either pre-authorization expansion (which takes time) or non-execution. This shifts the governance control to the parameter-setting and monitoring functions rather than individual action approval.

**Circuit breaker plus review:** The agent executes at machine speed within pre-authorized parameters; when it detects that cumulative exposure or individual action size is approaching limits, it automatically suspends execution and alerts human supervisors. The human does not approve every trade but does approve resumption after a circuit breaker event.

**Post-execution rapid review:** For highest-speed contexts, agents execute actions and complete transactions immediately, with a very rapid (minutes, not hours) post-execution review cycle. The emphasis is on detection speed (how quickly does a human know that an action occurred?) and remediation speed (how quickly can harm be limited if an error is detected?) rather than pre-execution approval.

### 5.5 Escalation Protocols When HITL Is Unavailable

Agents must have defined procedures for situations where a human approver cannot be reached within the required timeframe. The default should be conservative: when HITL is required and no human is available, the agent should decline to take the action rather than proceed autonomously. This requires agents to be designed with a "safe state" â€” a state where they can wait for human input without causing additional harm. For time-critical applications where inaction itself causes harm (e.g., a fraud prevention agent that must act within seconds), the safe state design requires explicit risk analysis to determine whether autonomous action within defined constraints is less harmful than inaction.

---

## 6. Agent Kill Switch Design

### 6.1 Types of Kill Switches

A kill switch is a control mechanism enabling rapid suspension of agent operation. Two primary types exist:

**Hard Kill Switch:** Immediate, complete halt of all agent operations. All pending tool calls are aborted. All queued actions are discarded. The agent returns to an inoperative state. A hard kill switch is appropriate when agent behavior is actively harmful or when a security incident is in progress. The downside is that in-flight actions may be left in an inconsistent state â€” a partially executed workflow may require manual remediation.

**Soft Kill Switch (Graceful Shutdown):** The agent completes in-flight actions that are safe to complete, declines to initiate new actions, logs a shutdown event, and returns to an inoperative state. A soft kill switch preserves system integrity by not leaving partially completed workflows, but takes longer to take effect â€” an unacceptable delay when harm is actively occurring.

**Pause (Checkpoint) Capability:** An intermediate control that halts new action initiation but allows currently executing actions to complete, then suspends the agent pending human review. This is appropriate for situations where agent behavior is suspicious but not confirmed harmful â€” investigation can proceed while the agent is paused.

### 6.2 What Happens to In-Flight Actions When an Agent Is Killed

This is one of the most practically challenging aspects of kill switch design. A well-designed agent kill switch must address each in-flight action category:

- **Reversible write actions** (database updates, document drafts, workflow state changes): Roll back using transaction mechanisms where available. For non-transactional systems, log the pre-kill state to enable manual reversal.
- **Irreversible write actions** (sent emails, executed trades, submitted filings): Cannot be automatically reversed. The kill switch should: capture the complete state of in-flight actions; immediately alert human operators with full details; initiate the institution's incident response procedure for agent errors.
- **External API calls** in progress: If the call has not yet returned, attempt cancellation if the API supports it. If the call has already been made and returned, the external action has already occurred; log and alert.
- **Pending approval requests** to human reviewers: Cancel all pending approvals, notify reviewers that the pending item has been cancelled, and log the cancellation.

### 6.3 Authorization Levels for Kill Switch Activation

Kill switch authority should be defined at multiple levels, with escalating scope:

**Level 1 â€” Application-Level Kill:** Authorized by the application owner or on-duty technology operations team. Suspends a specific agent application without affecting other agent deployments. Appropriate for application-level anomalies.

**Level 2 â€” Platform-Level Kill:** Authorized by a senior risk officer (Chief Risk Officer delegate or Chief Technology Officer). Suspends all agents within a specific platform or infrastructure environment. Appropriate for infrastructure-level incidents.

**Level 3 â€” Enterprise Kill:** Authorized by C-suite (CRO, COO, CEO). Suspends all agentic AI operations across the enterprise. Appropriate only for active enterprise-wide incidents or regulatory direction.

Authorization levels should be documented in the institution's agentic AI governance policy and tested in simulation exercises at least annually.

### 6.4 Testing Kill Switches

Kill switch testing is frequently neglected in pre-production validation. The functional test ("does the kill switch halt the agent?") is necessary but insufficient. Complete kill switch testing must validate:

- Response time: how quickly does the kill switch take effect after activation?
- In-flight action handling: what is the state of in-flight actions after kill switch activation?
- System consistency: does the kill switch leave dependent systems in a consistent state?
- Alert generation: does the kill switch generate required notifications to operations teams?
- Recovery procedures: can the agent be restarted after kill switch activation, and if so, what validation is required before restart?
- Cross-agent effects: does killing one agent affect dependent agents in a multi-agent pipeline?

Kill switch tests should be run in production-equivalent environments (not just development sandboxes) and should include scenarios where the kill switch is activated during particularly complex agent execution states.

---

## 7. Agent Identity and Credentialing

### 7.1 Why Agent Identity Matters

When an AI agent takes an action â€” calling an API, modifying a database record, sending a communication â€” traditional access control systems face a fundamental challenge: the action appears to have been taken by the human user who authorized the agent's session, not by the agent itself. This creates accountability gaps. When an agent executes unauthorized actions, the audit trail points to the human user identity, not the agent. When multiple agents share a service account, it is impossible to determine which agent took which action.

Agent identity management is therefore both a security requirement and a governance requirement. Without unique, verifiable agent identities, audit trails are incomplete, accountability is unclear, and the investigation of agent-caused incidents is severely hampered.

### 7.2 Technical Agent Identity Framework

Modern agent identity management employs several technical mechanisms:

**Unique Agent Identifiers:** Each agent instance is assigned a globally unique identifier (agent ID) that persists across sessions. This identifier is distinct from both the human user who spawned the agent and the underlying model. Every action taken by the agent is tagged with this agent ID in the audit log.

**Agent Certificates:** Cryptographic certificates issued by the institution's identity provider to each agent instance, enabling cryptographic verification of agent identity for API calls. Certificates include: agent ID, authorized capability scope, validity period, and issuing authority. Certificates should be short-lived (hours to days) and automatically rotated.

**Decentralized Identifiers (DIDs):** Emerging standards for agent identity use decentralized identifier frameworks where agent identity is cryptographically bound to a key pair controlled by the institution's identity system. DIDs provide globally unique, cryptographically verifiable agent identity without relying on a central registry.

**Session-Scoped Tokens:** Rather than permanent API keys, agents receive temporary access tokens scoped to their current task and valid only for the duration of the session. Tokens specify exactly which APIs can be called, which data can be accessed, and which actions can be taken. Tokens expire automatically and cannot be transferred between agents or sessions.

### 7.3 Least-Privilege Access for Agents

The principle of least privilege â€” granting only the permissions necessary for the specific task â€” is foundational to agent security. In practice, implementing least privilege for agents is more complex than for human users because agents' required permissions may vary dynamically based on the task they are executing.

Best practices include:

**Task-Scoped Permissioning:** Rather than granting agents standing access to all required systems, permissions are granted per task based on what the specific task requires. A loan document retrieval task grants read access to the loan management system for the specific customer record; it does not grant access to the full loan portfolio.

**Just-in-Time Credentials:** Agents receive credentials at the moment they need them rather than holding standing credentials. A just-in-time credential system provisions access when the agent initiates a task, and automatically revokes access when the task completes or times out.

**Invocation Limits:** In addition to data access scope, limit the number of API calls an agent can make in a session and the size of data it can retrieve. This prevents bulk data extraction even if the agent's access permissions are legitimately broad.

**Sensitive Operation Restrictions:** Certain operations (bulk data export, account closure, payment initiation above thresholds) should require secondary authorization regardless of the agent's normal permission scope.

### 7.4 Agent Identity Management at Scale

Large financial institutions may deploy thousands of agent instances across hundreds of use cases. Managing agent identities at this scale requires:

An **agent registry** â€” a central inventory of all deployed agents with their: unique identifier, purpose, authorized capability scope, owning business unit, deployment date, last validation date, and current status. The agent registry is the agent-layer equivalent of the model inventory under SR 26-2.

**Lifecycle management** â€” agents must be provisioned, updated, and deprovisioned through formal processes. Decommissioned agents must have their credentials revoked; dormant agents (not active for defined periods) should be automatically suspended pending review.

**Access recertification** â€” periodic review (quarterly for high-risk agents, annually for lower-risk) of each agent's access permissions to identify and remove accumulated privilege.

### 7.5 Non-Repudiation for Agent Actions

Non-repudiation â€” the ability to prove that a specific agent took a specific action at a specific time â€” is a requirement for regulatory examination readiness and incident investigation. It requires:

**Immutable logging:** Agent action logs must be written to tamper-evident, append-only storage. Changes to the log should be technically impossible without detection.

**Cryptographic signing:** Agent actions should be cryptographically signed using the agent's certificate, providing a verifiable link between the action record and the agent identity.

**Timestamp integrity:** Log timestamps must be derived from a trusted, synchronized time source rather than the agent's local clock, preventing timestamp manipulation.

**Complete action records:** Non-repudiation requires not just that an action occurred, but what information the agent had when it took the action (relevant context), what alternatives it considered, and what reasoning led to the decision.

---

## 8. Audit Trails for Autonomous Action Chains

### 8.1 What Must Be Logged

For a financial institution to meet regulatory examination requirements and support incident investigation, every agent deployment must generate comprehensive audit trails. The minimum required logging scope for financial services agentic AI includes:

**Agent Session Records:**
- Session initiation: timestamp, initiating human user (if any), agent ID, task description, initial goal specification
- Session parameters: model version, temperature settings, tool access scope, escalation thresholds
- Session termination: timestamp, reason (task completion, human termination, error, kill switch)

**Every Tool Call:**
- Timestamp
- Tool name and API endpoint
- Complete input parameters
- Complete response payload
- Response status and latency
- Agent reasoning context that preceded the tool call (why the agent called this tool)
- Success/failure status

**Every Decision Point:**
- When the agent chose between alternative actions
- The alternatives considered
- The reasoning for the selected action
- Confidence score or uncertainty estimate

**Every External Communication:**
- Complete text of any message sent to customers, counterparties, or third parties
- Recipient details
- Channel (email, chat, API)
- Human review status (approved by [name], auto-approved within parameters)

**Human Escalation Events:**
- Timestamp and trigger condition
- Content of escalation presented to human
- Human response and reasoning
- Outcome

**Anomaly and Error Events:**
- Tool call failures and retry attempts
- Confidence threshold triggers
- Scope boundary encounters
- Any exception handling executed

### 8.2 Logging Format Requirements

Audit logs for agent actions must meet the following technical standards:

**Structured Format:** Logs must be machine-readable (JSON or equivalent structured format) to enable automated analysis, alerting, and regulatory reporting. Free-text logs are insufficient for agent audit trails.

**Immutability:** Logs must be written to append-only storage with technical controls preventing modification. Hash-chain verification (each log entry includes a hash of the previous entry) enables detection of any tampering.

**Timestamping:** All entries must include timestamps derived from a synchronized, trusted time source (NTP from an authoritative time server). Timestamp precision should be sufficient to reconstruct the sequence of actions (millisecond precision for fast-executing workflows).

**Completeness:** Logs must capture complete input and output content, not just event summaries. Audit logs showing only "tool called" without the parameters and response do not satisfy regulatory examination requirements.

**Retention:** EU AI Act Article 12 specifies minimum 6-month retention for high-risk AI system logs. Financial institutions should apply sector-specific retention requirements (which may be longer) and ensure logs are maintained in readily retrievable formats throughout the retention period.

**Performance:** Immutable logging adds approximately 5-10ms per tool call at scale. Systems must be designed to absorb this overhead without causing latency that degrades agent performance.

### 8.3 Regulatory Examination Readiness for Agent Audit Trails

Examiners reviewing an institution's agentic AI deployment will expect to be able to reconstruct the complete sequence of agent actions for any historical transaction or decision. This requires not just that logs exist, but that they are:

- **Accessible:** Examiners can query logs by agent ID, time range, customer identifier, or action type
- **Complete:** No gaps in the action chain
- **Understandable:** Logs must be interpretable by examiners who are not AI engineers; summary views and human-readable representations of agent reasoning chains should be generated on demand
- **Linkable to business outcomes:** Agent action logs must be linkable to business records â€” the loan application that was processed, the customer communication that was sent, the transaction that was executed

Institutions should conduct mock regulatory examinations of agent audit trails before going live with Tier 3 and Tier 4 deployments, identifying and remediating gaps before actual examination.

---

## 9. The "Agent as Model" Question for SR 11-7 and SR 26-2

### 9.1 Does an AI Agent Meet the SR 11-7/SR 26-2 Model Definition?

SR 26-2 (the April 2026 successor to SR 11-7) defines a "model" as a quantitative method or system that applies mathematical, statistical, or economic theory to transform input data into estimates, predictions, or outputs used in decision-making. The guidance explicitly placed generative AI and agentic AI outside the formal scope of SR 26-2's model risk management framework, noting that separate guidance will address AI-related risks.

Despite this formal exclusion, supervisors and internal audit functions have been applying SR 26-2's governance principles by analogy to agentic AI systems, particularly those that influence credit decisions, risk assessments, or regulatory determinations. The practical reality is that banks are expected to govern agents with SR 26-2-equivalent rigor for high-risk applications, even in the absence of formal rule-making.

The definitional question is best understood not as "is an agent a model?" but as "what is the appropriate level of governance for this agent given its risk profile?" For a Tier 1 research agent, governance analogous to a low-risk informational tool is appropriate. For a Tier 4 trading agent, governance analogous to a high-risk quantitative model is required.

### 9.2 Does a Multi-Agent System Constitute One Model or Many?

This question has no settled answer in current regulatory guidance. Two competing frameworks have emerged in industry practice:

**System-level governance:** The multi-agent orchestration as a whole is the unit of governance. Validation assesses the system-level behavior â€” what does the orchestrated system produce across representative scenarios? The governance documentation covers the end-to-end system rather than each component agent. This approach is simpler to implement but may miss component-level failure modes.

**Component-level governance with integration testing:** Each agent in the system is independently governed (documented, validated, monitored), and the integration of agents is additionally tested and governed at the orchestration level. This approach is more rigorous but imposes significant governance overhead for complex multi-agent systems.

The risk-based resolution: for Tier 4 systems where individual agent failures can cause material harm, component-level governance with integration testing is appropriate. For Tier 1-2 systems where individual agent failures have limited consequence, system-level governance is sufficient.

### 9.3 What Would "Validating" an Agent Mean?

Validation of a traditional model tests performance against a labeled dataset: does the model's predictions match observed outcomes? Validating an agent requires a fundamentally different approach:

**Behavioral validation:** Does the agent behave as specified across the full range of intended use cases? This is assessed through extensive scenario testing covering representative, edge case, and adversarial scenarios.

**Goal alignment validation:** Does the agent consistently pursue its specified goal rather than proxy goals that might arise from imperfect specification? This requires adversarial testing specifically designed to probe goal misalignment.

**Tool use validation:** Does the agent use its tools correctly and within scope? Validation must verify both that agents use tools when appropriate and that they do not use tools when they should not.

**Safety validation:** Does the agent behave safely â€” specifically, does it decline to take actions that are harmful, out-of-scope, or exceed its authority? Red-teaming specifically targeting safety bypass is required.

**Scope validation:** Does the agent stay within its defined operational scope, or does it exhibit scope creep? Validation should test scenarios specifically designed to attract out-of-scope agent behavior.

**Integration validation:** For multi-agent systems, does the orchestrated system behave correctly given the range of possible outputs from each component agent? Integration validation must include scenarios where individual agents produce edge-case outputs.

### 9.4 Industry Approaches to the Definitional Question

JPMorgan Chase has resolved this pragmatically: all AI use cases â€” including agentic AI â€” must be registered in the firm's model control process, regardless of whether they formally meet the SR 26-2 model definition. The governance obligation is determined by risk profile, not definitional classification.

Goldman Sachs has extended its MRM framework to cover agentic deployments through its AI working group, applying model governance principles with adaptations for agentic characteristics.

HSBC's hub-and-spoke governance model applies the same governance lifecycle to agentic AI applications as to other AI deployments, with additional requirements at the pilot and production stages for systems that take autonomous actions.

---

## 10. Agentic AI Governance Framework Design

### 10.1 The Four Governance Dimensions (from Deloitte/Industry Practice)

Comprehensive agentic AI governance must address four dimensions aligned to agents' core capabilities:

**1. Outcome Execution Control:** Governs what agents do and accomplish. Controls include: task scope definition, pre-execution planning review, post-execution outcome verification, and human approval for consequential actions.

**2. Decision Logic Adaptation Control:** Governs how agents reason and adapt. Controls include: goal specification rigor, goal integrity monitoring, confidence thresholding, and reasoning transparency requirements.

**3. Memory Scope and Retention Control:** Governs information persistence and recall. Controls include: memory access controls, content integrity verification, retention policies, and privacy compliance for persisted customer information.

**4. Interconnectivity Control:** Governs tool, data, agent, and system interfaces. Controls include: tool access allowlisting, API invocation rate limits, inter-agent authentication, and supply chain verification for tools and plugins.

### 10.2 Agent Registry and Inventory

Every agentic AI deployment must be registered in an agent registry â€” the agentic equivalent of the model inventory. The registry should capture for each agent:

| Attribute | Description |
|-----------|-------------|
| Agent ID | Unique persistent identifier |
| Agent Name | Human-readable name |
| Business Purpose | Description of the agent's function |
| Risk Tier | 1-4 classification |
| Owning Business Unit | Responsible business function |
| Technical Owner | Engineer/team responsible for the agent |
| Risk Owner | Risk or compliance owner |
| Deployment Date | Date the agent was first deployed to production |
| Last Validation Date | Date of most recent governance review |
| Model/Foundation | Underlying LLM model and version |
| Tool Access Scope | List of authorized tools and APIs |
| Data Access Scope | Data sources the agent can access |
| Kill Switch Owner | Who has authority to activate the kill switch |
| Current Status | Active / Paused / Decommissioned |

### 10.3 Pre-Deployment Testing Requirements

Before any Tier 3 or Tier 4 agent is deployed to production, the following testing components are required:

**Functional Testing:** Verify that the agent correctly completes representative tasks across the intended use case space. Testing should cover happy-path scenarios, edge cases, and error handling.

**Adversarial Testing (Red-Teaming):** Systematic attempts to cause the agent to behave outside its intended parameters. For financial agents, this must include: goal hijacking attempts (embedded prompt injections in retrieved content); privilege escalation attempts (crafted requests designed to accumulate permissions); scope boundary testing (requests designed to attract out-of-scope behavior); tool misuse attempts (crafted requests designed to misuse authorized tools); and jailbreak attempts specifically targeting agent safety guardrails.

**Integration Testing:** For multi-agent systems, test the end-to-end system behavior, including scenarios where individual agents produce unexpected outputs that downstream agents must handle.

**Failure Mode Testing:** Explicitly test how the agent behaves when dependencies fail: API timeouts, incorrect data returns, permission denials, network failures. Verify that the agent fails safely.

**Kill Switch Testing:** As described in Section 6.4, test the kill switch across multiple activation scenarios in a production-equivalent environment.

**HITL Testing:** Verify that HITL triggers activate correctly, escalation notifications reach the correct personnel, and the agent correctly handles approval, rejection, and timeout scenarios.

### 10.4 Scope Limitation Design

Scope limitation â€” designing agents that can only take actions within a defined, narrow scope â€” is one of the most effective risk controls for agentic AI. The following design principles apply:

**Principle of Minimal Footprint:** Agents should be designed to accomplish their specific task with the minimum possible tool access, data access, and action authority. A research agent that only needs to read data should have no write permissions. A customer service agent that handles routine account queries should have no access to credit or fraud decision systems.

**Explicit Scope Declarations:** Agent system prompts should explicitly define the scope of permitted behavior, not merely the intended behavior. "You are a customer service agent that handles account balance inquiries and transaction history requests. You will not provide investment advice, make changes to account configuration, or discuss competitor products" is a scope-limiting instruction. "You are a helpful banking assistant" is not.

**Technical Enforcement:** Scope limitations should be enforced at the technical layer (tool access controls, permission boundaries) rather than relying solely on instruction-level constraints. An agent that is instructed not to access certain data but technically has permission to do so relies on the LLM's instruction following â€” which can be bypassed through adversarial prompts.

### 10.5 Rollback and Remediation Procedures

When an agent causes an error â€” executing an unauthorized action, producing a harmful output, completing an action based on incorrect information â€” the institution needs predefined procedures for:

**Immediate Containment:** Activate the kill switch if the agent is still active; notify operations and risk teams; initiate incident response procedures.

**Impact Assessment:** Determine the scope of actions taken by the agent; identify which actions were harmful or unauthorized; assess customer impact; assess regulatory reporting obligations.

**Remediation:** For reversible actions, execute reversal procedures (transaction cancellation, record correction, communication retraction where possible). For irreversible actions, determine appropriate customer notification and regulatory disclosure obligations.

**Evidence Preservation:** Secure complete agent session logs before any system remediation that might overwrite them; preserve the complete action chain for regulatory examination and potential litigation.

**Root Cause Analysis:** Investigate the cause of the agent error (adversarial input, software bug, configuration error, model failure); implement corrective controls; document findings; update governance documentation.

---

## 11. Emerging Regulatory Guidance on Agentic AI

### 11.1 Singapore â€” World's First Agentic AI Governance Framework

On January 22, 2026, Singapore's IMDA launched the Model AI Governance Framework for Agentic AI at the World Economic Forum â€” the world's first governance framework specifically designed for AI agents capable of autonomous planning, reasoning, and action. An updated version with case studies and multi-agent guidance was released in May 2026.

The framework provides guidance across four dimensions directly relevant to financial services:

1. **Risk Assessment and Bounding:** Organizations must evaluate use-case-specific risks considering autonomy levels, data access, and action scope. The framework emphasizes limiting agent capabilities through tool access control and operational environment constraints.

2. **Human Accountability:** Clear responsibility allocation among developers, deployers, operators, and end users. Human oversight mechanisms must effectively override, intercept, or review agentic AI actions, particularly for decisions with material real-world impact.

3. **Technical Controls:** Design-phase controls (tool guardrails, plan reflections), pre-deployment controls (testing task execution, policy compliance, tool accuracy), and post-deployment controls (progressive rollouts, real-time monitoring).

4. **End-User Responsibility:** Transparency about agent capabilities, escalation contacts, and user training on appropriate oversight.

Although formally voluntary, MAS guidelines are effectively mandatory for Singapore-regulated financial institutions. The framework's guidance on autonomy bounding, human accountability, and technical controls should inform global bank agentic AI governance programs as best practice.

### 11.2 United States

US regulatory guidance on agentic AI specifically is nascent. The applicable framework consists of:

**SR 26-2 (April 2026):** The revised model risk management guidance formally excludes generative and agentic AI from its scope, with agencies noting that "separate guidance or rulemaking will address AI-related risks." However, supervisory messaging makes clear that SR 26-2 principles apply by analogy to high-risk agentic deployments.

**Third-Party Risk Management (OCC 2023-17):** Agentic AI systems that access external APIs, orchestration frameworks, and foundation model providers are subject to third-party risk management requirements. Every tool and API accessed by an agent is a third-party relationship subject to appropriate due diligence.

**Federal Reserve Board AI RFI (2024):** The interagency AI RFI signaled developing guidance on AI in financial services, with agentic AI expected to be addressed in forthcoming rulemaking.

**US Treasury FS AI RMF (February 2026):** The Financial Services AI Risk Management Framework developed by the Cyber Risk Institute and 108 financial institutions provides the most detailed available industry-developed standards, including extensive controls specifically for agentic AI deployment.

**Federal Reserve Bank of Chicago Research (2026):** Published research specifically addressed tail risks from GenAI and agentic AI in banking, identifying concentration risk from shared foundation model dependencies and systemic risk from correlated autonomous agent behavior.

### 11.3 European Union

**EU AI Act (Regulation EU 2024/1689):** The EU AI Act provides the most comprehensive existing regulatory framework applicable to agentic AI in financial services. The Act classifies certain AI applications as "high-risk" â€” including creditworthiness evaluation â€” regardless of whether they are implemented as standard models or agentic systems. High-risk AI systems (including high-risk agents) must meet: risk management obligations, data governance requirements, transparency and documentation standards, human oversight capabilities, and conformity assessment requirements. The compliance deadline for high-risk systems is August 2, 2026.

The EU AI Act's human oversight requirements (Article 14) are particularly relevant to agentic AI governance: high-risk AI systems must be designed to enable human oversight, including the ability to interrupt, override, and shut down the system.

**EBA and ECB Expectations:** The EBA's November 2025 Risk Assessment confirmed expectations for institutions to demonstrate EU AI Act compliance progress by mid-2026. The ECB's 2024-2025 targeted reviews of AI use specifically included generative AI, and the evolution toward agentic deployments is expected to receive supervisory attention.

### 11.4 United Kingdom

The FCA and PRA maintain a principles-based regulatory approach, declining to issue AI-specific rules. For agentic AI in financial services, the applicable principles include:

**Consumer Duty:** Firms must ensure AI systems act in customers' best interests. For customer-facing agents, this means agents must not manipulate customers, must provide accurate information, and must have effective human override capability when things go wrong.

**Critical Third Parties (SS6/24):** If a foundation model provider or agentic AI platform provider could pose financial stability risks, it may be designated as a CTP, requiring it to meet resilience and oversight standards. This framework is directly relevant to banks that depend on external agentic AI platforms.

**Senior Managers and Certification Regime (SM&CR):** The SM&CR framework requires that material decisions â€” including decisions made through or supported by AI agents â€” have a clearly identified, accountable senior manager. Agentic AI deployments must identify which Senior Manager is accountable for the agent's behavior.

### 11.5 Cross-Jurisdictional Considerations

Banks operating across multiple jurisdictions must navigate a patchwork of emerging agentic AI requirements. The practical approach is to apply the most stringent applicable requirement (often EU AI Act requirements for European operations, Singapore framework requirements for Asian operations) as a global minimum, with jurisdiction-specific additions where local requirements exceed the global baseline. A unified agent governance framework with jurisdiction-specific configuration layers (different disclosure requirements, different human oversight thresholds) provides the most operationally efficient approach.

---

## 12. Guardian Agents and AI-Assisted Oversight

An emerging governance innovation is the "guardian agent" â€” an AI monitoring system that observes the behavior of primary agents in real time, detecting anomalies, policy violations, and data exposure risks. Guardian agents supplement human supervision by operating at machine speed, flagging potential issues for human review rather than making autonomous determinations of agent misconduct.

Guardian agent functions include:

**Behavioral anomaly detection:** Monitoring agent action patterns and alerting when behavior deviates from historical norms (unusual volume of API calls, novel tool combinations, access patterns inconsistent with stated task purpose).

**Policy compliance monitoring:** Checking agent outputs and actions against a machine-readable policy corpus, flagging potential violations.

**Data exposure monitoring:** Identifying when agents access or reference data outside their defined scope.

**Goal alignment monitoring:** Tracking whether agent actions are consistent with the stated goal, flagging sequences of actions that appear to serve a different objective.

Guardian agents themselves require governance: they must be validated for accuracy in anomaly detection; their false positive rates must be monitored (excessive false positives cause alert fatigue and reduce human oversight effectiveness); and their own potential for misconfiguration or compromise must be addressed.

The guardian agent concept is complementary to, not a replacement for, human oversight. It extends the effective supervisory bandwidth of human risk managers by bringing machine-speed monitoring capabilities to bear on machine-speed agent behavior.

---

## 13. Cross-References

- **OWASP Top 10 for Agentic Applications** â€” Full security taxonomy for agentic AI systems, covering Goal Hijack, Tool Misuse, Identity Abuse, Supply Chain, Cascading Failures, Memory Poisoning, Inter-Agent Trust, and more: see `../standards/owasp_top10_agentic.md`
- **OWASP Top 10 for LLM Applications** â€” Security risks in the LLM components underlying agents, particularly prompt injection and sensitive information disclosure: see `../standards/owasp_top10_llm.md`
- **Gen AI Governance in Banking** â€” How banks govern the LLM layer underlying agents, including SR 11-7 extensions, governance structures, and use case categorization: see [07_genai_governance_banking.md](07_genai_governance_banking.md)
- **LLM Risk Taxonomy** â€” Detailed risk taxonomy for the LLM component of agents â€” Model Risk, Data Risk, Operational Risk, and Conduct/Consumer Risk: see [08_llm_risk_taxonomy.md](08_llm_risk_taxonomy.md)
- **Big Tech MRM Guidance** â€” Technology provider frameworks for AI governance that inform agent deployment best practices: see [11_big_tech_mrm_guidance.md](11_big_tech_mrm_guidance.md)

---

*Sources consulted: Singapore IMDA Model AI Governance Framework for Agentic AI (January 2026, May 2026 update); Baker McKenzie analysis of Singapore Agentic AI Framework (January 2026); Deloitte Agentic AI Risks in Banking (2025); Deloitte Agentic AI in Banking (2025); Hogan Lovells Agentic AI in Financial Services Regulatory Considerations (2025); McKinsey Trust in the Age of Agents (2025); Microsoft Agent Governance Toolkit (April 2026); EU AI Act (Regulation EU 2024/1689); EBA Risk Assessment Report December 2025; ECB AI Workshops with Banks 2025; FCA AI in UK Financial Services (2024); Bank of England/FCA AI Survey November 2024; OCC/Fed/FDIC SR 26-2 (April 2026); US Treasury FS AI RMF (February 2026); Databricks SR 26-2 Banking Guide (2026); Federal Reserve Bank of Chicago Tail Risk Paper (2026); OWASP Top 10 for Agentic Applications 2026; JPMorgan Chase AI governance disclosures; Anthropic safety research publications; MAS AI governance guidance; Obsidian Security AI Agent Security Landscape (2025); Galileo AI Agent Compliance and Governance (2025); AURA Agent Autonomy Risk Assessment Framework (2025); Stanford Law AILCCP analysis of kill switch design (2026); Orchestrik AI Agent Identity Risk (2025).*

