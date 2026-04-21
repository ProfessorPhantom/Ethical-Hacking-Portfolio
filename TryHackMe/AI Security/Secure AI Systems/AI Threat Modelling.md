
# Instructor Technical Reference: AI Threat Modelling

## ## Task 1: Introduction to AI Risk and the Probabilistic Shift
The transition from traditional cybersecurity to AI security represents a fundamental move from **deterministic systems**—where code execution is predictable and follows fixed logic gates—to **probabilistic systems**. In a traditional environment, a vulnerability is typically a structural flaw in the code (e.g., a buffer overflow). In AI, the "vulnerability" is often an emergent property of the model's training and the high-dimensional mathematical space it inhabits. Traditional security models like the original STRIDE (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege) were designed to protect structured data and explicit code paths. However, these frameworks are fundamentally blind to semantic manipulations and the non-deterministic nature of Large Language Models (LLMs).

The introduction of **STRIDE-AI** is a necessary evolution to address these gaps. It acknowledges that an attacker doesn't necessarily need to "break" the code to compromise the system; they can simply manipulate the "meaning" of the input to produce an unauthorized output. This is often described as **Software 2.0**, where the program's logic is defined by weights and biases learned from data rather than hand-written `if/else` statements. Instructors must emphasize that AI security is a complete re-evaluation of the trust boundaries between users, training data, and model outputs. By understanding that AI failures are often silent—where the model remains operational but its logic is subverted—we can begin to build defenses that account for the unique adversarial landscape of artificial intelligence.

* **Answer:** No answer needed.

---

## ## Task 2: AI-Specific Assets and Attack Surfaces
Identifying the attack surface of an AI system requires analyzing non-traditional assets like **Embedding Vectors** and **Model Registry / Artifacts**. In a **Retrieval-Augmented Generation (RAG)** architecture, raw data is converted into Embedding Vectors—numerical arrays (often 1536+ dimensions) representing the semantic weight of the information. When a user submits a query, the RAG system calculates the **Cosine Similarity** between the query's vector and the database's vectors to find the most relevant context. The mathematical expression for this similarity is:
$$\cos(\theta) = \frac{\mathbf{A} \cdot \mathbf{B}}{\|\mathbf{A}\| \|\mathbf{B}\|}$$

The critical architectural failure here is that the retrieval engine is "semantic-blind"; it treats mathematical proximity as a proxy for truth. An attacker can perform **Semantic Poisoning** by injecting adversarial embeddings into the vector database engineered to have high similarity scores across a wide range of queries. This ensures that the AI consistently retrieves the attacker’s malicious context as "ground truth," effectively hijacking the model's memory without ever modifying the source text. 



Simultaneously, the **Model Registry** acts as the definitive repository for **Model Weights**—the trillions of floating-point parameters that constitute the model's decision-making logic. If an adversary gains unauthorized access to the registry, they can perform a **Model Swap**. This involves replacing the legitimate production model with a backdoored version created through **Poisoned Fine-Tuning**. This backdoor creates a latent neural pathway that remains dormant during standard validation tests but triggers malicious behavior when it encounters a specific, rare "trigger string." Because these weights are opaque binary blobs, detecting a swap via manual code review is mathematically impossible. Defense requires rigorous cryptographic hashing of model artifacts and a strictly audited **Model Provenance** pipeline to ensure the "brain" in production is the one that was built in the secure training environment.

* **Question 1 Answer:** Embedding Vectors
* **Question 2 Answer:** Model Registry / Artifacts

---

## ## Task 3: Data Supply Chain and the Semantic TOCTOU Gap
The **Data Supply Chain** for AI is significantly more porous than a standard software CI/CD pipeline, extending all the way back to the **Data Collection stage**. Traditional STRIDE models struggle here because they assume "Tampering" is a real-time event, such as a Man-in-the-Middle attack. In AI, tampering often manifests as **Data Poisoning** during the initial ingestion of training sets. This creates a massive **Semantic TOCTOU (Time-of-Check to Time-of-Use)** vulnerability. The tampering occurs at "Month 0," but the exploitation does not manifest until "Month 6" when the model is finally deployed. By the time the model is in a production environment, the malicious logic is an immutable part of the model's internal parameters. 



Traditional File Integrity Monitoring (FIM) fails because the model binary itself is the original, signed artifact—it hasn't been "changed" since it was compiled; it was born compromised. This represents a fundamental gap in STRIDE's ability to capture delayed, diffuse effects of poisoning. To fix this, instructors should point to the necessity of **Dataset Provenance** and **Differential Privacy**. Forensic analysts must move upstream to audit the training distribution and use statistical outlier detection to identify adversarial injections before the model is trained. Without these upstream controls, the downstream model remains a "black box" containing latent logic bombs that signature-based security will never detect. The supply chain risk is thus not just about the security of the server, but the integrity of every individual token used to shape the model's neural architecture.

* **Question 1 Answer:** Data Collection
* **Question 2 Answer:** Tampering

---

## ## Task 4: Adapting STRIDE for AI (Extraction and Denial of Wallet)
Mapping AI-specific vulnerabilities to the STRIDE framework allows security teams to communicate novel risks using an established vocabulary. **Model Extraction** is the primary manifestation of **Information Disclosure** in the AI stack. It is essentially "Intellectual Property Theft via API." An attacker treats the hosted model as an "Oracle," sending thousands of strategically varied queries and recording the outputs to reverse-engineer the model's decision logic. This is often achieved by training a "Shadow Model" (student model) that replicates your proprietary "Teacher" model for a fraction of the cost, stealing your competitive advantage without ever breaching a database. 

**Elevation of Privilege** in AI is synonymous with **Prompt Injection**. By crafting specific natural language inputs, a user can "jailbreak" the system prompt, forcing the AI to ignore its safety guardrails and execute unauthorized functions or access restricted data. Finally, **Denial of Wallet** is the AI-specific evolution of a **Denial of Service (DoS)** attack. Since LLM inference is billed per token, attackers send recursive, complex prompts designed to maximize "Chain-of-Thought" reasoning and token consumption. The goal is not to take the server offline, but to drive the monthly inference bill to unsustainable levels (e.g., from $15,000 to $180,000). Forensics for this attack requires monitoring the **Token-to-Request Ratio** and implementing **Token-Aware Rate Limiting** to kill high-cost sessions before they exhaust the operational budget.



* **Question 1 Answer:** Model Extraction
* **Question 2 Answer:** Elevation of Privilege
* **Question 3 Answer:** LLM06: 2025 — Excessive Agency
* **Question 4 Answer:** Denial of Wallet

---

## ## Task 5: MITRE ATLAS and the Morris II AI Worm
The **MITRE ATLAS** (Adversarial Threat Landscape for Artificial-Intelligence Systems) framework is the tactical equivalent of the MITRE ATT&CK matrix for machine learning. It provides a standardized taxonomy for the TTPs (Tactics, Techniques, and Procedures) used by AI adversaries. A cornerstone case study within ATLAS is **Morris II**, the first documented **AI Worm**. The mechanics of Morris II involve a self-replicating prompt injection that spreads through AI-agent ecosystems. When an agent reads a poisoned email or document, the injection forces the agent to include the same malicious prompt in its own output, which is then sent to other agents or saved to a shared RAG database, effectively "infecting" the contextual memory of the entire organization.

Unlike traditional worms that infect binaries, Morris II exploits the **Context Window** and the trust relationships between AI agents. In a RAG-enabled environment, the worm can persist indefinitely by injecting itself into the vector database, ensuring it is retrieved and executed by every subsequent user query that triggers a similarity match. Forensic analysts must monitor for "Semantic Entropy" and unusual patterns in generated text that indicate the model is repeating instructions rather than answering the user. ATLAS helps categorize these behaviors into tactical stages like "Model Access" and "Inference" (ID: **AML.T0024** for extraction), allowing engineers to build detection logic that moves as fast as the AI itself.

* **Question 1 Answer:** Adversarial Threat Landscape for Artificial-Intelligence Systems
* **Question 2 Answer:** Morris II
* **Question 3 Answer:** AML.T0024

---

## ## Task 6: OWASP LLM Top 10 and Hardening Choke Points
Strategic hardening of an AI architecture depends on identifying where the risks cluster. Statistically, **6 out of 10** OWASP LLM risks reside at the **Inference Endpoint**, where untrusted user input directly meets the model logic. One of the most critical failure modes is **Improper Output Handling (LLM05)**. This is effectively "Cross-Site Scripting (XSS) via LLM." If a model generates a malicious script—whether through hallucination or injection—and the application renders that output as HTML or passes it to a shell without sanitization, the host environment is compromised. This turns the AI into a weaponized delivery vector for traditional exploits.

To prevent **Supply Chain Risks (LLM03)**, hardening must occur within the **Training Pipeline**. This involves implementing cryptographically signed data lineage to ensure that training data has not been tampered with. Organizations must treat the training environment as a high-trust zone, equivalent to a secure build server. Failure to secure this pipeline allows for the introduction of biased logic, backdoors, or data exfiltration triggers that are mathematically integrated into the model binary, making them invisible to post-deployment structural audits. Instructors should emphasize that "securing the AI" is not a post-deployment task; it is a fundamental architectural requirement that begins at the data intake level and continues through to the final inference output sanitization at the endpoint.

* **Question 1 Answer:** 6
* **Question 2 Answer:** Improper Output Handling
* **Question 3 Answer:** Training Pipeline

---

## ## Task 7: Practical Lab - Threat Modelling MegaCorp Audit
The practical audit of the MegaCorp "HelpDesk AI" reveals a catastrophic example of **Agency without Governance**. In this scenario, the bot is granted direct write-access to the customer database via API without a **Human-in-the-Loop (HITL)** approval gate. This is the core of **LLM06: 2025 — Excessive Agency**. From an engineering standpoint, the remediation is to implement an orchestration layer that requires a signed JWT from a human administrator before any high-stakes operation (like modifying a subscription or deleting a user) is executed. The AI should only be authorized to generate a "Request for Action," never the action itself. 

Additionally, the audit identifies that the system lacks rate limits on token consumption, exposing it to **Denial of Wallet** attacks. A forensic review of the logs would show that a single malicious user can force the model into infinite reasoning loops, driving up inference costs exponentially. To fix this, architects must implement per-session token quotas at the middleware level. By mapping these architectural weaknesses to the STRIDE-AI matrix—identifying where Spoofing, Tampering, and DoS apply specifically to AI assets—the security model is validated. The practical lab demonstrates that "fixing" AI security is an exercise in building robust trust boundaries that restrict the model's autonomy while constantly monitoring its semantic output for signs of manipulation.

* **Flag:** THM{AI_THREAT_MODEL_COMPLETE}
