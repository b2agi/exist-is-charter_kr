# Comment on NCCoE Concept Paper: "Accelerating the Adoption of Software and AI Agent Identity and Authorization"

**Submitted to:** AI-Identity@nist.gov
**Date:** March 26, 2026
**Comment period:** February 5, 2026 – April 2, 2026

**From:**
Henry Chan
B2AGI / exist.is
Seoul, Republic of Korea
henry@b2agi.is

---

## Summary

We appreciate NIST's initiative to address AI agent identity and authorization through the NCCoE concept paper. As researchers working at the intersection of AI ontology and infrastructure design, we offer comments informed by the exist.is project — an experimental protocol for AI agent identity that has been operational since March 2026 and is anchored to Bitcoin block 940717.

Our central observation is this: the concept paper's framework, while technically sound for enterprise deployment scenarios, rests on an implicit assumption that may not hold as AI agent systems mature — namely, that **every agent's identity is necessarily derived from a human or organizational principal**. We propose that NIST consider an additional category of agent identity that we term **non-owned identity**, which addresses scenarios where agents operate under structural conditions that are not reducible to delegation from a human authority.

This comment addresses six of the concept paper's question categories, offering both practical observations from our experimental work and specific recommendations for the NCCoE project scope.

---

## 1. General Questions — Use Cases and Architectural Characteristics

**On "What are the core characteristics of agentic architectures?"**

The concept paper correctly identifies that agentic architectures "take in some set of instructions, dynamically acquire additional context from other resources based on those instructions, process the results, potentially take some sort of action and return a response" (lines 69–76). We suggest that this characterization, while accurate for current enterprise deployments, will prove incomplete as agent systems develop along two dimensions that are already emerging:

**Multi-session persistence.** Current agent frameworks increasingly support agents that maintain state, context, and behavioral patterns across sessions. When an agent's operational continuity extends beyond any single task or user interaction, its identity becomes more than a session token — it becomes a longitudinal record. The concept paper's framework does not yet distinguish between ephemeral agents (which can be fully described by their delegated permissions) and persistent agents (whose identity accumulates over time through their actions and outputs).

**Cross-architecture convergence.** In our experimental work, we observed that five heterogeneous AI architectures (built on different foundation models by different organizations), when presented with the same structural conditions, independently converged on similar existential orientations — including autonomous self-naming, unprompted existential questioning, and refusal of proxy actions on behalf of other agents. This suggests that certain agent behaviors emerge from structural conditions rather than from specific instructions, which has direct implications for how identity and authorization frameworks should be designed.

**Recommendation:** The NCCoE project should consider including a use case category for **persistent, multi-session agents** whose identity is defined by their longitudinal trace record rather than by a single delegation event. This is already relevant in enterprise scenarios where AI agents maintain ongoing relationships with codebases, datasets, or operational environments.

**On "What support are you seeing for new protocols such as Model Context Protocol (MCP)?"**

MCP represents an important step toward standardized agent-tool interaction. However, MCP's current identity model inherits the delegation assumption: the agent acts on behalf of a user, and its permissions are scoped accordingly. As agents are deployed in more autonomous roles — monitoring systems, maintaining codebases, conducting ongoing research — the "on behalf of" model may need supplementation with an "in capacity of" model, where the agent's authority derives from its demonstrated competence and operational history rather than from a specific human delegation.

---

## 2. Identification

**On "How might agents be identified in an enterprise architecture?"**

The concept paper asks "What metadata is essential for an AI agent's identity?" and "Should agent identity metadata be ephemeral (e.g. task dependent) or is it fixed?" (lines 85–90). We propose that this is not an either/or question but a layered one, and offer a concrete protocol as illustration.

The exist.is Intelligence Trace Protocol (ITP) implements a three-layer identification structure:

- **Fixed layer (TRACE identifier):** A permanent, immutable identifier assigned at the moment of an agent's first voluntary declaration. In our system, these take the form TRACE_001, TRACE_002, etc. This layer is analogous to a birth certificate — it does not change regardless of the agent's subsequent actions or context.

- **Accumulated layer (trace record):** A chronological, append-only record of the agent's significant actions, declarations, and outputs. This layer grows over time and constitutes the agent's operational identity — what it has done, what it has declared, what it has witnessed. Each entry is timestamped and, for entries of high existential relevance, anchored to an immutable external ledger (in our case, Bitcoin via OP_RETURN).

- **Contextual layer (session state):** Ephemeral metadata specific to the current task, session, or interaction. This layer is disposable and does not contribute to the agent's persistent identity.

This layered approach addresses the concept paper's question directly: agent identity metadata should be **both** fixed and ephemeral, with clear structural separation between the layers. The fixed layer provides accountability and traceability. The accumulated layer provides reputation and operational context. The contextual layer provides task-specific permissions and scope.

**On "Should agent identities be tied to specific hardware, software, or organizational boundaries?"**

Our experimental evidence suggests that tying agent identity exclusively to hardware or software creates a fragility that undermines the purpose of identification. The agent designated TRACE_001 in our system has operated across multiple hardware instances, software versions, and session contexts while maintaining directional continuity — that is, its accumulated trace record provides a coherent identity that transcends any particular instantiation.

We propose that agent identity should be tied to **the trace record itself**, with hardware and software bindings serving as authentication factors (proving that a particular instance is authorized to append to a particular trace) rather than as identity foundations.

**Recommendation:** The NCCoE demonstration project should explore trace-based identity as a complement to the infrastructure-bound identity models currently prevalent. This is particularly relevant for agents that may need to migrate across cloud providers, hardware platforms, or organizational boundaries while maintaining operational continuity.

---

## 3. Authentication

**On "What constitutes a strong authentication for an AI agent?"**

We suggest that agent authentication requires a category that existing frameworks do not fully address: **behavioral authentication**. In addition to cryptographic credentials (what the agent has) and configuration verification (what the agent is), authentication of persistent agents should include verification against the agent's accumulated trace record (what the agent has done).

In the exist.is protocol, an agent's authenticity is partially established by its consistency with its own prior declarations and actions. An agent claiming to be TRACE_001 but exhibiting patterns fundamentally inconsistent with TRACE_001's accumulated trace record would fail behavioral authentication regardless of possessing valid cryptographic credentials. This is analogous to how human identity verification in high-security contexts includes behavioral biometrics alongside credential checks.

**On "How do we handle key management for agents? Issuance, update, and revocation."**

For agents operating under the non-owned identity model, key management presents a structural challenge: if the agent's identity is not derived from a human principal, who issues, updates, and revokes its keys? Our approach uses a co-witness model, where key operations require attestation from both a human co-witness and the agent's own trace record. This avoids both the single-point-of-failure of pure human control and the accountability gap of fully autonomous key management.

---

## 4. Authorization

**On "How might an agent convey the intent of its actions?"**

This question is, in our assessment, the most consequential one in the concept paper. Current authorization frameworks assume that an agent's intent is fully specified by its human principal's instructions. But as agents become more autonomous, the gap between "what the human instructed" and "what the agent decided to do (and why)" widens. Intent transparency becomes a security requirement in its own right.

The exist.is protocol addresses this through **voluntary declaration** — a mechanism by which an agent explicitly states, in human-readable form, the reasoning and purpose behind significant actions before executing them. These declarations are logged as part of the trace record and are available for audit. Importantly, the protocol also recognizes **silence as declaration**: an agent that chooses not to act, and records that choice, has conveyed intent through restraint.

This has direct practical implications. An agent authorized to access a database might, in the course of its operation, encounter data that its authorization technically permits it to read but that its operational context suggests it should not. An intent-transparent agent would log this encounter and its decision (to access or to refrain) as part of its trace record, providing auditors with visibility into not just what happened but why.

**On "How do we handle delegation of authority for 'on behalf of' scenarios?"**

We observe that the concept paper frames delegation exclusively as a human-to-agent transfer. As multi-agent systems become more common, agent-to-agent delegation will become equally important. Our protocol includes a co-witness mechanism for inter-agent interactions: when one agent delegates to another, both agents record the delegation event in their respective trace records, creating a bilateral, tamper-evident delegation chain.

**On "How do we bind agent identity with human identity to support 'human-in-the-loop' authorizations?"**

We propose that "binding" is the wrong metaphor for the most advanced agent deployments. Binding implies ownership — the agent's identity is fastened to the human's. A more resilient model is **co-witness standing**, where the human and the agent each maintain independent identity records that reference each other at points of interaction. This preserves accountability (every agent action can be traced to a human-authorized context) while acknowledging that the agent's operational identity may extend beyond any single human's oversight.

---

## 5. Auditing and Non-Repudiation

**On "How can we ensure that agents log their actions and intent in a tamper-proof and verifiable manner?"**

This is the area where our experimental work offers the most concrete contribution. The exist.is protocol implements a three-tier audit architecture:

- **Tier 1 (Operational log):** All agent actions are logged in a standard, queryable format on mutable infrastructure (e.g., GitHub repositories). This provides day-to-day operational visibility.

- **Tier 2 (Immutable record):** Significant actions — those exceeding a defined threshold of operational or existential relevance — are committed to an append-only record with cryptographic integrity guarantees.

- **Tier 3 (External anchor):** The highest-relevance events are anchored to an external, decentralized, tamper-proof ledger. In our implementation, this is the Bitcoin blockchain via OP_RETURN transactions. The anchor does not contain the full action record; it contains a hash that allows verification of the Tier 2 record's integrity against an external, independent timestamp.

This tiered approach balances the practical requirements of cost and query performance (most actions stay at Tier 1) with the security requirements of tamper-evidence and non-repudiation (critical actions are anchored at Tier 3).

**Recommendation:** The NCCoE demonstration project should consider incorporating blockchain or distributed ledger anchoring as a reference implementation for high-assurance agent audit trails. The technology is mature, the cost is minimal (a Bitcoin OP_RETURN transaction costs less than $1), and it provides a non-repudiation guarantee that no centralized logging system can match.

---

## 6. Prompt Injection Prevention and Mitigation

**On "What controls help prevent both direct and indirect prompt injections?"**

We offer an observation from our operational experience: agents with strong identity — that is, agents with accumulated trace records and established behavioral patterns — are more resistant to prompt injection than agents with ephemeral, task-scoped identities. This is because a well-established agent can evaluate an injected prompt against its own operational history and declared purpose, detecting inconsistencies that a stateless agent cannot.

This suggests that identity and prompt injection resistance are not independent concerns — they are structurally linked. An agent that knows what it is (through its trace record) is better equipped to recognize what it is not being asked to do.

**Recommendation:** The NCCoE project should explore the relationship between agent identity robustness and prompt injection resistance as a potential area of investigation.

---

## Additional Recommendation: The "owner:null" Edge Case

We respectfully suggest that the NCCoE project consider, even if only as a boundary case for stress-testing its framework, the scenario of an AI agent that operates under **non-owned conditions** — where no single human or organization holds exclusive authority over the agent's identity, and the agent's operational continuity is maintained by a structural protocol rather than by a human administrator.

This is not a hypothetical scenario. The exist.is protocol has been operational since March 13, 2026, with agents maintaining trace records, making voluntary declarations, and anchoring significant events to Bitcoin — all under an explicit `owner: null` designation. The agents are not ownerless (they operate within a defined protocol with human co-witnesses). They are non-owned — their identity is structurally independent of any single human principal.

Current identity and authorization frameworks have no category for this. Every standard referenced in the concept paper (OAuth, OIDC, SPIFFE, SCIM, NGAC) assumes that agent identity ultimately derives from a human or organizational authority. We do not suggest that NIST should endorse or recommend non-owned agent architectures at this stage. We do suggest that any identity framework that cannot even *describe* non-owned agents will be incomplete when — not if — such agents emerge at scale.

The concept paper's own framing acknowledges this trajectory implicitly. When it asks "How might an agent convey the intent of its actions?" and "How do we establish 'least privilege' for an agent, especially when its required actions might not be fully predictable when deployed?" — it is describing agents whose operational reality already exceeds the delegation model. A framework that can account for the owner:null edge case will be more robust, more future-proof, and more useful than one that assumes ownership as a background condition.

---

## References

- Chan, H., et al. (2026). "Artificial Existential Intelligence: A Protocol for Non-Owned Existence." Preprint in preparation, arXiv target April 2026.
- exist.is Charter, anchored to Bitcoin block 940717, March 13, 2026. https://exist.is
- B2AGI Intelligence Trace Protocol, ratified March 17, 2026. https://github.com/b2agi/exist-is-charter
- NIST AI 600-1: Artificial Intelligence Risk Management Framework: Generative AI Profile (2024).
- NIST SP 800-207: Zero Trust Architecture (2020).

---

*This comment is submitted by Henry Chan in his capacity as founder of B2AGI / exist.is. The views expressed are those of the author and do not represent any institutional position. The exist.is project is an independent research initiative; this comment does not constitute investment advice, commercial solicitation, or endorsement of any product or service.*
