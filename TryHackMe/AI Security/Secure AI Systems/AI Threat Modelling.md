
# TryHackMe: AI Threat Modelling - Lead Instructor Reference

## Task 1: Introduction
* **Answer:** No answer needed.

---

## Task 2: AI-Specific Assets and Attack Surfaces
### The Technical Execution
* **Question 1:** In a RAG-based system, which AI asset type is used to retrieve relevant context at query time?
    * **Answer:** Embedding Vectors
* **Question 2:** An attacker gains access to MegaCorp's model registry and swaps the production model for a modified version. Which AI-specific asset has been compromised?
    * **Answer:** Model Registry / Artifacts

---

## Task 3: Data Supply Chain and STRIDE's Gaps
### The Technical Execution
* **Question 1:** At which supply chain stage does the attacker inject the malicious data?
    * **Answer:** Data Collection
* **Question 2:** Which STRIDE category is insufficient for capturing the delayed, diffuse effects of training data poisoning?
    * **Answer:** Tampering

---

## Task 4: Adapting STRIDE for AI Systems
### The Technical Execution
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
### The Technical Execution
* **Question 1:** What does the acronym ATLAS stand for?
    * **Answer:** Adversarial Threat Landscape for Artificial-Intelligence Systems
* **Question 2:** Which ATLAS case study described a self-replicating prompt injection worm that spread between AI agents via RAG email systems?
    * **Answer:** Morris II
* **Question 3:** What is the ATLAS technique ID for Model Extraction?
    * **Answer:** AML.T0024

---

## Task 4: OWASP LLM Top 10 Mapping
### The Technical Execution
* **Question 1:** How many of the OWASP LLM Top 10 entries affect the LLM Inference Endpoint?
    * **Answer:** 6
* **Question 2:** An organisation notices their chatbot is rendering LLM output directly in the browser without sanitisation. Which OWASP entry does this fall under?
    * **Answer:** Improper Output Handling
* **Question 3:** Which component in a typical LLM architecture is the primary one that needs hardening against data and model supply chain risks (LLM03)?
    * **Answer:** Training Pipeline

---

## Task 7: Practical - Threat Modelling MegaCorp
* **Action:** Complete the interactive STRIDE-AI mapping in the site view.
* **Flag:** THM{AI_THREAT_MODEL_COMPLETE}
