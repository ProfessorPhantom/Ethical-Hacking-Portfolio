
# 🛡️ Technical Reference: AI-Augmented Digital Forensics
**Course:** Ethical Hacking I-II (Rhodes State College)  
**Lab:** [TryHackMe: AI Forensics](https://tryhackme.com/room/aiforensics)  
**Instructor:** Joshua Smith  
**Focus:** High-Dimensional Data Correlation, Probabilistic Analysis, and Linux Post-Exploitation

---

## 0x01: Task 2 – The AI Forensics Landscape

### I. Theoretical Context: Probabilistic Modeling
In standard digital forensics (DFIR), tools are generally **Deterministic**—input A always leads to result B (e.g., a hash match). AI shifts the paradigm toward **Probabilistic** outcomes.
* **Pattern Recognition:** AI models utilize high-dimensional vector spaces to identify non-linear correlations across massive datasets (e.g., matching packet entropy with unusual system call timing).
* **Precision Metric:** Calculated as $TP / (TP + FP)$. In a forensic context, high precision is mandatory to ensure that an innocent user is not flagged by an automated system.

### II. Technical Execution: Metrics of Reliability
The lab focuses on identifying the specific terminology used to vet AI models in a forensic capacity:
* **Non-determinism:** The stochastic nature of Large Language Models (LLMs) where the "Temperature" setting can cause the model to provide different answers to the same query over multiple runs.

### III. Forensic Significance
If an investigator uses a **non-deterministic** tool to generate a report, that evidence may be inadmissible because it lacks "Repeatability." A forensic result must be reproducible by an independent third party to maintain the Chain of Custody.

### IV. Edge Cases
* **Failure (Overfitting):** The AI may identify a "pattern" that is actually just environmental noise, leading to a high False Positive rate.
* **Detection:** Attackers can use **Adversarial Perturbations**—adding minor, invisible "noise" to a file—to force an AI to misclassify malware as a benign system file.

**Task 2 Answers:**
* What ability of AI helps turn a DFIR investigator into a "super-analyst"? **Answer: Pattern Recognition**
* Which metric tells you the proportion of positively flagged results that were correct? **Answer: Precision**
* What term describes AI yielding different outputs for the same input? **Answer: non-determinism**

---

## 0x02: Task 3 – AI & DFIR (Technical Integration)

### I. Theoretical Context: Architecture Specialization
Forensic artifacts vary in structure, requiring specific AI neural architectures:
* **CNNs (Convolutional Neural Networks):** These use mathematical "kernels" to scan spatial data (pixels) for geometric patterns.
* **RNNs/Transformers:** Used for sequential data, such as system logs or network traffic, to understand the relationship between events over time.



[Image of Convolutional Neural Network architecture for image recognition]


### II. Technical Execution: Dynamic vs. Static Analysis
* **Dynamic Analysis:** Instead of scanning a static binary (which can be packed or obfuscated), the AI observes the **Sequence of API Calls** (e.g., `OpenProcess` -> `VirtualAllocEx` -> `WriteProcessMemory`).
* **Sentiment Analysis:** Applying Natural Language Processing (NLP) to chat logs to identify emotional shifts or malicious intent in insider threat investigations.

### III. Forensic Significance
AI-driven **Time-Sequenced** analysis allows for "Automatic Timeline Reconstruction." In a breach involving thousands of endpoints, AI can correlate the exact millisecond a phishing email was opened with a lateral movement attempt on a different subnet.

### IV. Edge Cases
* **Failure:** CNNs can be bypassed by steganography where malicious payloads are hidden within the "Least Significant Bits" (LSB) of an image, which may not trigger a standard visual pattern filter.
* **Detection:** Sophisticated attackers monitor "Timing Side Channels." If an AI-EDR takes longer to analyze a specific type of encrypted packet, the attacker can adapt their exfiltration speed to blend in.

**Task 3 Answers:**
* What neural network is used for spatial patterns in visual data? **Answer: Convolutional Neural Network**
* What analysis assesses the emotional tone of messages? **Answer: Sentiment Analysis**
* What data do AI systems correlate to reconstruct timelines? **Answer: Time-Sequenced**
* What analysis observes program behavior (API calls)? **Answer: Dynamic Analysis**

---

## 0x03: Task 4 – Legal and Ethical Implications

### I. Theoretical Context: The Daubert Standard
The **Daubert Standard** is the U.S. legal baseline for admitting scientific evidence.
1.  **Testability:** Has the model been empirically tested?
2.  **Error Rate:** Is the False Positive/Negative rate known?
3.  **Peer Review:** Has the model been vetted by the scientific community?



### II. Technical Execution: Solving the Black Box
AI is often a "Black Box"—it provides an answer but not a reason. To solve this, forensics uses **Explainable AI (XAI)** like **SHAP** (SHapley Additive exPlanations) to identify which features (e.g., a specific port or file extension) led to the classification.

### III. Forensic Significance
If an analyst cannot explain the "How" behind an AI's decision during cross-examination, the defense can move to suppress the evidence as "unreliable."

### IV. Edge Cases
* **Failure:** Facial recognition models often demonstrate racial bias due to skewed training data, leading to ethical and legal failures in identification.
* **Detection:** Attackers can perform **Model Poisoning** if they gain access to the training pipeline, "teaching" the AI that their C2 (Command and Control) traffic patterns are actually "Normal System Updates."

**Task 4 Answers:**
* What U.S. legal test assesses if scientific testimony is admissible? **Answer: Daubert**
* What term describes AI processes that are hard for humans to interpret? **Answer: Black Box**
* What technology has shown racially biased results? **Answer: Facial Recognition**
* What technique allows ML without transferring sensitive data? **Answer: Federated Learning**

---

## 0x04: Task 5 – Practical: The Digital Trail

### I. Theoretical Context: Persistence and Volatility
This lab focuses on "Living off the Land" (LotL) techniques where the attacker uses legitimate system binaries to maintain access.

### II. Technical Execution: Command Analysis
The primary persistence mechanism discovered was the modification of SSH keys.

**Command Breakdown:**
`sudo nano /home/r.house/.ssh/authorized_keys`
* **`sudo`**: Execution with root privileges (indicating a prior privilege escalation or misconfiguration).
* **`nano`**: A lightweight text editor used to avoid the complexity of `vi` and minimize the terminal footprint.
* **`authorized_keys`**: The target file for SSH persistence. Appending a public key here allows the attacker to bypass password authentication entirely.

### III. Forensic Significance: Memory Staging
The exfiltration archive was located at: `/dev/shm/.core_dump_2025.tgz.enc`
* **Forensic Significance of `/dev/shm`:** This is a **tmpfs** (Shared Memory) filesystem. It exists in **RAM**, not on the physical disk.
* **The "Why":** Most traditional antivirus and forensic scanners do not index `/dev/shm`. Because it is volatile, the evidence is automatically wiped if the system reboots, making real-time AI memory forensics essential.
* **Masquerading:** The file was named `.core_dump` to mimic a legitimate system crash file, which is often ignored by system administrators.

### IV. Edge Cases
* **Failure:** If the machine was hard-rebooted before the memory dump was taken, all evidence in `/dev/shm` would be lost.
* **Detection:** Modern EDR tools monitor for "unusual sudo executions" or any modifications to the `.ssh` directory, which should rarely change for a standard user.

**Investigation Answers:**
* Successful login time for `j. morgan`: **Answer: 03:01:02**
* Initial access method: **Answer: Phishing**
* Attacker email address: **Answer: akeane@poseidonenergy.net**
* Command to access `r. house`: **Answer: sudo nano /home/r.house/.ssh/authorized_keys**
* Path of the stolen source code archive: **Answer: /dev/shm/.core_dump_2025.tgz.enc**
* Final Flag: **Answer: THM{AI_THE_ULTIMATE_DETECTIVE}**

---

## 0x05: Final Artifact Summary

| Artifact | Forensic Value | Technical Domain |
| :--- | :--- | :--- |
| **03:01:02** | Temporal Anomaly | Login outside of business hours |
| **Phishing** | Initial Access Vector | Social Engineering / ODS file execution |
| **`/dev/shm`** | Anti-Forensics | Volatile RAM-based staging area |
| **`authorized_keys`** | Persistence | Lateral movement to `r.house` account |
| **`.enc` Extension** | Exfiltration | Encrypted tarball to bypass DPI |
