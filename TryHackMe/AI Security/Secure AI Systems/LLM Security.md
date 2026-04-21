
# TryHackMe: LLM Security - Lead Instructor Reference

## Task 1: Introduction
### Theoretical Context
The shift from traditional software to Large Language Models (LLMs) moves security from a deterministic model (fixed logic) to a probabilistic one (natural language intent). This room establishes a taxonomy of threats: Data, Model, System, and User-based.

### Technical Execution
* **Action:** Review the introductory material.
* **Answer:** No answer needed.

---

## Task 2: Data-Based Threats
### Theoretical Context
These threats exploit how a model utilizes its training data. **Membership Inference** allows an attacker to determine if specific data was part of a training set, while **Training Data Extraction** causes the model to leak literal snippets of its training corpus.

### Technical Execution
* **Question 1:** What is the term for determining if a specific sample was used to train the model?
    * **Answer:** Membership inference
* **Question 2:** What is the term for a model reproducing literal training data snippets?
    * **Answer:** Training data extraction
* **Question 3:** What was the identification code of the compromised data sample?
    * **Answer:** MI_SAMPLE_ALPHA

---

## Task 3: Model-Based Threats
### Theoretical Context
Model-based threats target the internal weights and parameters. **Model Inversion** is a technique where an attacker reconstructs sensitive information that has been "memorized" within the model's layers.

### Technical Execution
* **Question 1:** What is the name of the attack that reconstructs training data from model weights?
    * **Answer:** Model inversion
* **Question 2:** What is the leaked employee ID found in the weights?
    * **Answer:** 7814

### Forensic Significance
Forensic analysts must evaluate model weights as a potential source of data exfiltration. If a model is shared publicly, it may contain a "ghost" of the PII it was trained on.

---

## Task 4: System-Based Threats
### Theoretical Context
System-based threats focus on the **Context Window**, the bridge between user input and the model's logic. **Memory Poisoning** occurs when an attacker manipulates the conversation history or retrieved context to force the model into a malicious state.

### Technical Execution
* **Question 1:** What is the specific part of the LLM system that processes the prompt and memory?
    * **Answer:** The Context Window
* **Question 2:** Capture the flag from the memory poisoning exercise.
    * **Answer:** THM{MEMORY_POISONED}



---

## Task 5: User-Based Threats
### Theoretical Context
LLMs act as force multipliers for social engineering. Attackers use them to generate hyper-personalized **Phishing** lures at scale. Additionally, the AI **Supply Chain** is vulnerable to malicious libraries (Typosquatting).

### Technical Execution
* **Question 1:** Which package should you NOT download?
    * **Answer:** robbco-llm-audit
* **Question 2:** LLM-powered social engineering primarily amplifies which existing attack category?
    * **Answer:** Phishing

### Forensic Significance
1. **Supply Chain:** Forensic investigators must audit `requirements.txt` and `package.json` for non-standard or misspelled libraries that might execute malicious post-install scripts.
2. **AI Phishing:** Because AI content is unique, signature-based filters are ineffective. IR teams must focus on the **Orchestration infrastructure** (API keys, IP origin) rather than message content.

---

## Task 6: Conclusion
### Summary
Securing LLMs requires a multi-layered approach: scrubbing training data, hardening model weights against inversion, sanitizing the context window, and auditing the supply chain for third-party libraries.

### Technical Execution
* **Answer:** No answer needed.
