
# Instructor Technical Reference: AI Threat Modelling

## Task 2: AI-Specific Assets and Attack Surfaces
The fundamental shift in AI security begins with identifying assets that do not exist in the traditional IT stack. **Embedding Vectors** represent the primary data asset in Retrieval-Augmented Generation (RAG) systems. Unlike structured SQL records, these vectors are high-dimensional numerical arrays that encode the semantic "meaning" of a data fragment. When a user submits a query, the system calculates the **Cosine Similarity** between the query's vector and the stored database vectors to retrieve the most relevant context. The architectural failure point here is that the retrieval mechanism is "semantic-blind"; it prioritizes mathematical proximity over data integrity. An attacker can execute **Semantic Poisoning** by injecting adversarial embeddings engineered to be "closest" to a wide range of common queries, effectively hijacking the AI's retrieved context to deliver malicious payloads or misinformation without ever altering the source text.

Secondarily, the **Model Registry** serves as the "kernel image" repository for the AI system, housing the **Model Weights**. These weights are the trillions of parameters that define the model's decision-making logic. The forensic risk is that model weights are essentially "black boxes." If an adversary gains registry access and performs a **Model Swap**, they can replace a legitimate model with one that has undergone "Poisoned Fine-Tuning." This creates a latent backdoor—a hidden neural pathway that remains dormant during standard validation but triggers malicious behavior when it encounters a specific, rare string. Detecting this requires rigorous model provenance and cryptographic verification of weights, as standard code review is ineffective against binary neural parameters.



* **Question 1:** In a RAG-based system, which AI asset type is used to retrieve relevant context at query time?
    * **Answer:** Embedding Vectors
* **Question 2:** An attacker gains access to MegaCorp's model registry and swaps the production model for a modified version. Which AI-specific asset has been compromised?
    * **Answer:** Model Registry / Artifacts

---

## Task 3: Data Supply Chain and STRIDE's Gaps
The AI supply chain introduces a critical vulnerability window that traditional STRIDE models fail to capture: **Supply Chain Latency**. While traditional security focuses on real-time tampering of data in transit, AI systems are vulnerable to **Data Poisoning** during the **Data Collection** phase, often months before a model is trained or deployed. This is a **Semantic TOCTOU (Time-of-Check to Time-of-Use)** vulnerability. The tampering occurs at "Month 0" when malicious records are ingested into the training set. Because this data appears as valid natural language, it bypasses structural validation filters.

The mechanical failure manifests during the training phase, where the model "compresses" this malicious logic into its internal weights. When the model is deployed at "Month 6," it passes all standard File Integrity Monitoring (FIM) and code signing checks because the binary artifact itself is original and "valid" by its own definition. The vulnerability is no longer a bug in the code, but an inherent property of the model's personality. Forensic analysts cannot rely on network intrusion detection (NIDS) to find these triggers, as they look like harmless user input. Instead, security teams must implement **Dataset Provenance** and use differential privacy techniques to ensure no single data point (or small cluster of poisoned points) can disproportionately influence the model's decision boundaries.



* **Question 1:** At which supply chain stage does the attacker inject the malicious data?
    * **Answer:** Data Collection
* **Question 2:** Which STRIDE category is insufficient for capturing the delayed, diffuse effects of training data poisoning?
    * **Answer:** Tampering

---

## Task 4: Adapting STRIDE for AI Systems
To align AI threats with the SOC's operational reality, we map adversarial techniques to the STRIDE framework. **Model Extraction** is the AI manifestation of Information Disclosure. It is a "Black-Box" attack where an adversary treats your API as an "Oracle." By submitting a high volume of strategically varied queries (Query Fingerprinting), the attacker records the outputs to train a "Student" model that replicates your proprietary "Teacher" model's logic. This results in the theft of high-value Intellectual Property without a single unauthorized database access event.

**Elevation of Privilege** in the AI context occurs through **Indirect Prompt Injection**. This happens when an AI agent is granted "Agency"—the ability to interact with external tools or data. An attacker can place a hidden natural language payload in an external source (like a public webpage). When the AI fetches that data to summarize it for a user, the payload instructs the AI to ignore its system prompt and instead execute a privileged tool call, such as deleting a user record or exfiltrating data. Finally, **Denial of Wallet** is the AI-specific evolution of a DoS. Since inference is billed per token, attackers craft "Recursive Reasoning Loops" or prompts that trigger maximum "Chain-of-Thought" expansion. The forensic signature is a spike in the **Token-to-Request Ratio**, where a low volume of traffic causes a catastrophic spike in compute costs, aiming to make the service financially unsustainable.



* **Question 1:** What is the primary AI-specific manifestation of Information Disclosure in the STRIDE-AI mapping?
    * **Answer:** Model Extraction
* **Question 2:** An attacker crafts prompts that cause an LLM to bypass its safety guidelines and content restrictions. Which STRIDE category does this map to?
    * **Answer:** Elevation of Privilege
* **Question 3:** Which OWASP LLM Top 10 (2025) entry addresses the risks of AI systems being granted too many permissions or too much autonomy?
    * **Answer:** LLM06: 2025 — Excessive Agency
* **Question 4:** An attacker drives your monthly inference bill from $15,000 to $180,000 without taking your service offline. What is this type of attack commonly called?
    * **Answer:** Denial of Wallet

---

## Task 5: MITRE ATLAS
The **MITRE ATLAS** (Adversarial Threat Landscape for Artificial-Intelligence Systems) framework provides the tactical matrix required for AI red-teaming and incident response. A foundational case study within ATLAS is **Morris II**, the first documented "AI Worm." The mechanics of this attack involve a self-replicating prompt injection that spreads through AI-agent ecosystems. When an agent reads a poisoned email or document, the injection forces the agent to include the same malicious prompt in its own generated output, which is then sent to other agents or saved to a shared RAG database.

This demonstrates that the AI's **Context Window** acts as a new type of memory buffer that is susceptible to injection. In a RAG-enabled environment, the "Worm" can persist by injecting itself into the vector database, ensuring it is retrieved and executed by every subsequent user query that triggers a similarity match. Forensically, this requires monitoring for "Semantic Entropy"—unusual patterns in the generated text that indicate the model is repeating instructions rather than answering the user. ATLAS helps engineers categorize these behaviors into Tactics, Techniques, and Procedures (TTPs) that can be mapped to traditional SIEM alerts.

* **Question 1:** What does the acronym ATLAS stand for?
    * **Answer:** Adversarial Threat Landscape for Artificial-Intelligence Systems
* **Question 2:** Which ATLAS case study described a self-replicating prompt injection worm that spread between AI agents?
    * **Answer:** Morris II
* **Question 3:** What is the ATLAS technique ID for Model Extraction?
    * **Answer:** AML.T0024

---

## Task 6: OWASP LLM Top 10 Mapping
Defensive prioritization relies on identifying "Architectural Choke Points." Statistically, **6 out of 10** OWASP LLM risks reside at the **Inference Endpoint**—the boundary where untrusted user input meets the model. One of the most critical failures is **Improper Output Handling (LLM05)**. This is the AI equivalent of a Cross-Site Scripting (XSS) or Command Injection attack. If a model generates a malicious script (either through hallucination or injection) and the application renders that output as HTML or passes it to a shell without sanitization, the security of the host environment is compromised.

To mitigate **Supply Chain Risks (LLM03)**, hardening must occur within the **Training Pipeline**. This involves implementing cryptographically signed data lineage to ensure that training data has not been tampered with. Organizations must treat the training environment as a high-trust zone, equivalent to a secure build server. Failure to secure this pipeline allows for the introduction of biased logic, backdoors, or data exfiltration triggers that are mathematically integrated into the model binary, making them invisible to all post-deployment structural audits.

* **Question 1:** How many of the OWASP LLM Top 10 entries affect the LLM Inference Endpoint?
    * **Answer:** 6
* **Question 2:** An organisation notices their chatbot is rendering LLM output directly in the browser without sanitisation. Which OWASP entry does this fall under?
    * **Answer:** Improper Output Handling
* **Question 3:** Which component in a typical LLM architecture is the primary one that needs hardening against data and model supply chain risks (LLM03)?
    * **Answer:** Training Pipeline

---

## Task 7: Practical - Threat Modelling MegaCorp
The practical audit of the MegaCorp "HelpDesk AI" reveals the catastrophic failure of "Agency without Governance." In this scenario, the bot is granted direct write-access to the customer database via API without a **Human-in-the-Loop (HITL)** approval gate. This is the core of **Excessive Agency (LLM06)**. From an engineering standpoint, the remediation is to implement an orchestration layer that requires a signed JWT from a human administrator before any "POST" or "DELETE" operation is executed. The AI should only be authorized to generate a "Request for Action," never the action itself.

Furthermore, the system lacks **Token-Aware Rate Limiting**, exposing it to **Denial of Wallet**. A forensic review of the billing logic shows that a single malicious user can force the model into infinite reasoning loops, driving up the inference cost exponentially. To fix this, architects must implement per-session token quotas at the middleware level. By mapping these architectural weaknesses to the STRIDE-AI matrix (identifying where Spoofing, Tampering, and DoS apply specifically to the LLM assets), the security model is validated, and the audit is complete.

* **Flag:** THM{AI_THREAT_MODEL_COMPLETE}
