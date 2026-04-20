
# Path: AI Security
## Room: AI Forensics (Verified Source of Truth)

### 0x01: Introduction
This room demonstrates how AI scales human intuition to manage the massive data volumes found in Digital Forensics and Incident Response (DFIR). We move from manual log hunting to using AI for anomaly detection and timeline reconstruction.

---

### 0x02: Task 2 - The AI Forensics Landscape
AI is a probabilistic tool, not a deterministic one. We must use specific metrics to verify its reliability in a forensic context.

* **Pattern Recognition:** AI's ability to see connections in data that exceed human comprehension.
* **Precision:** The proportion of positive identifications (e.g., "this is a threat") that were actually correct.
* **Non-determinism:** The characteristic where an AI might give different answers to the same input across different runs.

**Task Answers:**
1. What ability of AI helps turn a DFIR investigator into a "super-analyst" by recognizing patterns they might not have been able to comprehend?
   * **Answer:** `Pattern Recognition`
2. Which metric tells you the proportion of positively flagged results (e.g., "this is malware") that were actually correct?
   * **Answer:** `Precision`
3. What term describes the AI characteristic where the same input may yield different outputs across different runs?
   * **Answer:** `non-determinism`

---

### 0x03: Task 3 - AI & DFIR (Technical Integration)
This section outlines how specific AI architectures handle different forensic data types.



[Image of Convolutional Neural Network architecture for image recognition]


* **CNNs:** Essential for spatial patterns in image and video forensics.
* **Sentiment Analysis:** Used on chat/email logs to assess emotional tone or malicious intent.
* **Dynamic Analysis:** Observing program behavior (like API calls) rather than just static code.

**Task Answers:**
1. What type of neural network is commonly used in image and video forensics due to its ability to learn spatial patterns in visual data?
   * **Answer:** `Convolutional Neural Network`
2. What kind of analysis can be performed on social media or chat logs to assess the emotional tone of messages?
   * **Answer:** `Sentiment Analysis`
3. What type of data do AI systems correlate to reconstruct the timeline of an incident automatically?
   * **Answer:** `Time-Sequenced`
4. What type of analysis observes how a program behaves (e.g., its API call sequence) to determine whether it is malicious?
   * **Answer:** `Dynamic Analysis`

---

### 0x04: Task 4 - Legal and Ethical Implications
If AI identifies the suspect, can that evidence hold up in court? This task introduces the legal standards for scientific evidence.

* **Daubert Standard:** The U.S. legal test for whether expert/scientific testimony is admissible.
* **Black Box Problem:** The lack of interpretability in AI decision-making.

**Task Answers:**
1. What legal test used in the U.S. assesses whether expert or scientific testimony is admissible in court?
   * **Answer:** `Daubert`
2. What term describes AI models whose internal decision-making processes are difficult for humans to interpret?
   * **Answer:** `Black Box`
3. What real-world technology used by law enforcement has been shown to produce racially biased results in identifying suspects?
   * **Answer:** `Facial Recognition`
4. What technique allows machine learning to be performed without transferring sensitive data to a central server?
   * **Answer:** `Federated Learning`

---

### 0x05: Task 5 - Practical: The Digital Trail
*Deploy the lab machine and analyze the log fragments using the provided AI-assisted tools.*

**Investigation Answers:**
1. At what time does the attacker successfully log in as j. morgan?
   * **Answer:** `03:01:02`
2. What attack method was used to gain initial access?
   * **Answer:** `Phishing`
3. Can you find the attacker's email address?
   * **Answer:** `akeane@poseidonenergy.net`
4. What command did the attacker run as j. morgan to gain access to the r. house account?
   * **Answer:** `sudo nano /home/r.house/.ssh/authorized_keys`
5. What is the full path of the archive used to steal RobbCo's source code?
   * **Answer:** `/dev/shm/.core_dump_2025.tgz.enc`

**The Final Flag:**
* **Flag:** `THM{AI_THE_ULTIMATE_DETECTIVE}`
