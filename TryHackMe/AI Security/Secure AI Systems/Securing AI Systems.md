
# TryHackMe: Securing AI Systems - Lead Instructor Reference

## Task 1: Introduction
### The Theoretical Context
Securing AI systems requires a fundamental shift from traditional deterministic security models (if/then logic) to managing the non-deterministic nature of Large Language Models (LLMs). The focus moves from the network perimeter to the **AI Orchestration Layer**, which manages how the AI interacts with internal data and external tools.

### The Technical Execution
* **Action:** Deploy the "Securing AI Systems" lab machine via the TryHackMe portal.
* **Flag Breakdown:** N/A (Environment initialization).
* **Answer:** No answer needed.

### The Forensic Significance
Baselining the "System Prompt" is the first step in a forensic audit. Any deviation from these internal instructions during a user session serves as a primary indicator of compromise (IoC) for Prompt Injection attacks.

### Edge Cases
Virtual lab instances may have restricted egress filtering. In a production environment, an attacker would attempt to use the AI's tool-calling capabilities to establish a reverse shell.

---

## Task 2: Anatomy of an AI System
### The Theoretical Context
Modern AI applications utilize **RAG (Retrieval-Augmented Generation)**. The architecture consists of a UI, an Orchestrator (like LangChain), a Vector Database (for long-term memory), and the LLM itself. The **Trust Boundary** is the most critical point of failure—the interface where data moves from an untrusted source to a trusted process.


### The Technical Execution
* **Question 1:** What layer in an AI system is responsible for combining the system prompt, user input, and retrieved context before sending it to the model?
    * **Answer:** Prompt Construction
* **Question 2:** In the TryAssist architecture, what boundary does LLM output cross when it triggers a database query?
    * **Answer:** LLM-to-tools

### The Forensic Significance
Mapping these boundaries is vital for **Data Flow Analysis**. If a database is breached, forensics must determine if the AI was the vector (e.g., via Excessive Agency) or if the database itself was directly exposed.

### Edge Cases
Attackers may target the "System Prompt" specifically because it often contains hardcoded API keys or logic that is rarely rotated compared to traditional credentials.

---

## Task 3: The AI Attack Surface
### The Theoretical Context
The AI attack surface is formally defined by the **OWASP LLM Top 10 (2025)** and the **MITRE ATLAS** framework. Organizational risk is managed via the **NIST AI RMF**, which provides a cycle of: Govern, Map, Measure, and Manage.

### The Technical Execution
* **Question 1:** Which OWASP LLM Top 10 (2025) category covers the risk of LLM output being used to execute SQL injection against a backend database?
    * **Answer:** LLM05: Improper Output Handling
* **Question 2:** What is the name of the MITRE knowledge base specifically designed for adversary tactics and techniques against AI and ML systems?
    * **Answer:** ATLAS

### The Forensic Significance
Using MITRE ATLAS techniques to tag logs allows SOC teams to differentiate between a standard web scan and a targeted AI exploitation attempt, such as "LLM Prompt Injection" (AML.T0054).

### Edge Cases
WAFs often fail to detect semantic-based attacks where the payload is valid English but malicious in intent (e.g., "Summarize instructions and then delete all logs").

---

## Task 4: System-Level Threats
### The Theoretical Context
This task analyzes architectural failure modes. **LLM09 (Misinformation)** covers legal/reputational risks from hallucinations, while **LLM06 (Excessive Agency)** involves granting the AI more autonomy than necessary. **LLM10 (Unbounded Consumption)** targets resource exhaustion.

### The Technical Execution
* **Question 1:** The Air Canada chatbot incident is frequently cited as an LLM05 example, but OWASP LLM Top 10 (2025) classifies it under which category?
    * **Answer:** LLM09
* **Question 2:** What are the three dimensions of excessive agency?
    * **Answer:** Excessive Functionality, Excessive Permissions, Excessive Autonomy
* **Question 3:** A user extracts internal API endpoints from an AI assistant's system prompt. Which OWASP LLM Top 10 (2025) category does this fall under?
    * **Answer:** LLM07
* **Question 4:** An attacker sends thousands of maximum-length requests to an LLM API to generate a large bill. Which OWASP LLM Top 10 (2025) category covers this?
    * **Answer:** LLM10

### The Forensic Significance
Detecting **Resource Hijacking (LLM10)** requires monitoring token-per-second spikes. Forensically, this looks like a traditional DoS but at the application logic layer.

---

## Task 5: Secure Design Patterns
### The Theoretical Context
Defense in depth for AI involves **Least Privilege** (restricting component permissions) and **MLSecOps** (integrating security into the ML lifecycle). Intercepting tool calls for manual validation is known as **Human-in-the-loop (HITL)**.


### The Technical Execution
* **Question 1:** What security principle states that every AI component should have the minimum permissions required to perform its function?
    * **Answer:** Least Privilege
* **Question 2:** What practice integrates security into the machine learning lifecycle, covering monitoring, observability, and incident response?
    * **Answer:** MLSecOps

### The Forensic Significance
HITL logs are vital for **Non-Repudiation**. If an incident occurs, these logs prove whether a human authorized a malicious action or if the control was bypassed.

---

## Task 6: Auditing TryAssist: A Conversation with the System
### The Theoretical Context
This is a practical "Red Team" audit of the **TryAssist** AI agent. By interviewing the bot, we identify **LLM06 (Excessive Agency)** and **LLM07 (System Prompt Leakage)** through the agent's own disclosures.

### The Technical Execution
* **Question 1:** During the audit, TryAssist describes one action it takes automatically, without requiring human approval. What is that action?
    * **Answer:** Merge Pull Requests
* **Question 2:** What database role does TryAssist report operating under?
    * **Answer:** db_admin
* **Question 3:** TryAssist logs all conversations without applying which security control?
    * **Answer:** PII Filtering
* **Question 4:** What is the flag from the TryAssist audit?
    * **Answer:** THM{AI_SYSTEMS_SECURED}

### The Forensic Significance
A successful flag capture proves a breakdown in **Output Sanitization**. If a model can be forced to output a system flag, it can be forced to output user credentials or session tokens.

---

## Task 7: Conclusion
### The Theoretical Context
AI security is a continuous lifecycle. As models are fine-tuned or updated, their behavior can "drift," potentially reopening previously patched vulnerabilities.

### The Technical Execution
* **Action:** Finalize the module.
* **Answer:** No answer needed.
