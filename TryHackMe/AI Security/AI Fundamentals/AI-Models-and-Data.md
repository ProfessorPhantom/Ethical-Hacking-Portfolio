
# 🧪 Technical Reference: AI Models & Data (Data Supply Chain)
**Course:** Ethical Hacking I-II (Rhodes State College)  
**Lab:** [TryHackMe: AI Models & Data](https://tryhackme.com/room/aimodelsdata)  
**Instructor:** Joshua Smith  
**Focus:** Data Provenance, Model Inheritance, and the ML Bill of Materials (ML-BOM)

---

## 0x01: Task 2 – Training Data & Provenance

### I. Theoretical Context: Data Lineage
In AI security, **Data Provenance** is the equivalent of a "Chain of Custody" in digital forensics. It is the record that documents the inputs, entities, and processes involved in producing a data artifact. 
* **Common Crawl:** A massive, petabyte-scale dataset of web-scraped data. Because it is uncurated, it often contains PII (Personally Identifiable Information), credential leaks, and toxic content that models "learn" by default.



### II. Technical Execution
This section focuses on the documentation standards required to verify a dataset's integrity:
* **ML-BOM (Machine Learning Bill of Materials):** A structured inventory of all datasets, models, and dependencies used. This is a critical artifact for auditing whether a model was trained on "poisoned" or unlicensed data.

### III. Forensic Significance
From an investigative standpoint, if an AI model starts leaking sensitive corporate data (Data Exfiltration), the **ML-BOM** and **Provenance** records are the first places a forensic analyst looks to determine if the data was ingested during the training phase.

### IV. Edge Cases
* **Data Poisoning:** An attacker can inject malicious "trigger" samples into public datasets like Common Crawl. If a model ingests these, it can develop a backdoor (e.g., specific keywords that bypass all safety filters).

**Task 2 Answers:**
* Ability to answer where data came from and if it was modified? **Answer: Data Provenance**
* The most widely used public corpus underpinning major models? **Answer: Common Crawl**
* The AI equivalent of an SBOM for documenting datasets? **Answer: ML-BOM**

---

## 0x02: Task 3 – Building the Model (Key Concepts)

### I. Theoretical Context: The Training Lifecycle
Model training is a mathematical optimization process that introduces specific security vulnerabilities:
* **Overfitting:** When a model is trained for too many **Epochs** (passes), it begins to "memorize" the training data rather than learning general concepts. 
* **Quantization:** The process of converting model weights from high precision (e.g., FP32) to low precision (e.g., INT4). While this saves memory, it can lead to "Model Drift" where security guardrails become numerically unstable and fail.



[Image of overfitting vs underfitting in machine learning]


### II. Technical Execution: Training Architectures
* **Federated Learning:** A privacy-preserving technique where the model is trained on local devices (e.g., mobile phones). Only the **Weights** (mathematical updates) are sent to a central server, never the raw data.



[Image of federated learning architecture]


### III. Forensic Significance
**Overfitting** is a major privacy risk. In a "Training Data Extraction Attack," an adversary can query an overfitted model to retrieve verbatim copies of the training data—potentially revealing the PII or passwords it memorized during training.

### IV. Edge Cases
* **Catastrophic Forgetting:** During fine-tuning, a model might "forget" its original safety alignment while learning a new task, making it more susceptible to jailbreaking.

**Task 3 Answers:**
* One complete pass of the algorithm through the dataset? **Answer: Epoch**
* Problem where a model memorizes data rather than learning patterns? **Answer: Overfitting**
* Optimization technique that reduces numerical precision of weights? **Answer: Quantisation**
* Training approach across decentralized devices? **Answer: Federated Learning**

---

## 0x03: Task 4 – The Inheritance Problem

### I. Theoretical Context: Pre-trained Model Security
Most organizations perform **Fine-tuning** on **Pre-trained Models** (like Llama or Mistral) found on platforms like Hugging Face. Security vulnerabilities are "inherited"—if the base model has a bias or a backdoor, the fine-tuned version will almost certainly have it as well.



### II. Technical Execution
* **Pre-trained Model:** A model already trained on a massive, general-purpose dataset.
* **Fine-tuning:** The act of taking that pre-trained model and giving it a "finishing school" on a smaller, niche dataset (e.g., medical records or legal text).

### III. Forensic Significance
In a "Supply Chain Attack," an adversary can upload a "Backdoored" model to a public repository. If a company uses that model as their base, the attacker can trigger malicious behavior (like leaking prompts) regardless of how much fine-tuning the company does.

### IV. Edge Cases
* **Weight Hijacking:** A specialized attack where small changes are made to the model's weights that don't affect general performance but create a "trigger" for specific malicious outputs.

**Task 4 Answers:**
* Continuing training a pre-trained model on a task-specific dataset? **Answer: Fine-tuning**
* A model already trained on a large general-purpose dataset? **Answer: Pre-trained Model**

---

## 0x04: Task 5 – The Black Box Problem

### I. Theoretical Context: Model Interpretability
AI models are composed of billions of **Weights** (floating-point numbers). To make these "Black Boxes" understandable for security audits, we use **Model Cards**. 



### II. Technical Execution
A **Model Card** serves as the "Nutrition Label" for AI. It outlines:
1. Intended Use Cases.
2. Training Data Sources.
3. Known Biases and Limitations.
4. Performance Metrics (Precision, Recall).

### III. Forensic Significance
When conducting a post-incident audit, the **Model Card** is essential for determining if a model was used outside of its intended "Safety Envelope." If a model card warns that it is not for "Clinical Use" but was used for medical triage, it establishes a clear failure in governance.

### IV. Edge Cases
* **Stale Documentation:** Model cards are often static. If the model undergoes "RLHF" (Reinforcement Learning from Human Feedback), the original model card may no longer accurately reflect its security posture.

**Task 5 Answers:**
* Artifact that describes what a model is and its shortcomings? **Answer: Model Card**
* The billions of numbers making up a trained model? **Answer: Weights**

---

## 0x05: Task 6 – Practical Lab (Model Card Audit)

### I. Theoretical Context: Technical Auditing
The lab requires an active audit of a model's documentation to find evidence of data filtering and provenance.

### II. Technical Execution
1. Launch the lab instance.
2. Navigate to the provided web interface.
3. Identify the **Version 1.0.2** metadata and notice the "Unfiltered" data source flag.

### III. Forensic Significance
Auditing these cards in a real-world SOC (Security Operations Center) allows analysts to identify if a model is "High Risk" based on the lack of data filtering documented in the provenance section.

### IV. Edge Cases
* **Intentional Omission:** Companies may omit specific "Shadow Data" sources from their model cards to protect trade secrets, creating a blind spot for security auditors.

**Practical Answer:**
* The Final Flag: **Answer: THM{DATA_PROVENANCE_MATTERS}**

---

### 💡 Instructor's Final Note
For the **PenTest+**, remember that "Social Engineering" now applies to models. If you know a model was trained on **Common Crawl**, you can guess it has a high likelihood of "memorizing" GitHub code snippets or StackOverflow answers, which can be extracted via prompt injection.
