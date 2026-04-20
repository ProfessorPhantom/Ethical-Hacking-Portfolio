
# Path: AI Security
## Room: AI Forensics (Verified Source of Truth)

### 0x01: The New Frontier of DFIR
Digital Forensics and Incident Response (DFIR) is traditionally a slow, manual process. This room explores how AI can automate timeline reconstruction, identify anomalies in massive log files, and assist in legal/ethical documentation.

---

### 0x02: Task 2 - The AI Forensics Landscape
AI isn't perfect; it's probabilistic. This task covers how we measure an AI's "honesty" and effectiveness during an investigation.

* **Pattern Recognition:** AI's primary strength is seeing connections in data that exceed human comprehension.
* **Precision vs. Recall:** High precision means fewer "false positives" (important in court).
* **Non-determinism:** The fact that an AI might give two different answers to the same question—a major challenge for forensic repeatability.

**Task Answers:**
1. What ability of AI helps turn a DFIR investigator into a "super-analyst" by recognizing patterns they might not have been able to comprehend?
   * **Answer:** `Pattern Recognition`
2. Which metric tells you the proportion of positively flagged results (e.g., "this is malware") that were actually correct?
   * **Answer:** `Precision`
3. What term describes the AI characteristic where the same input may yield different outputs across different runs?
   * **Answer:** `non-determinism`

---

### 0x03: Task 3 - AI & DFIR (Technical Tools)
How AI actually touches the evidence.

* **CNN (Convolutional Neural Networks):** Used for spatial patterns (Image/Video forensics).
* **Sentiment Analysis:** Checking chat logs/emails for "malicious intent" or stress levels.
* **Time-Sequenced Data:** AI excels at taking logs from 50 different servers and building one master timeline.

**Task Answers:**
1. What type of neural network is commonly used in image and video forensics due to its ability to learn spatial patterns in visual data?
   * **Answer:** `Convolutional Neural Network`
2. What kind of analysis can be performed on social media or chat logs to assess the emotional tone of messages?
   * **Answer:** `Sentiment Analysis`
3. What type of data do AI systems correlate to reconstruct the timeline of an incident automatically?
   * **Answer:** `Time-Sequenced`
4. What type of analysis observes how a program behaves (e.g., API call sequence) to determine if it is malicious?
   * **Answer:** `Dynamic Analysis`

---

### 0x04: Task 4 - Legal & Ethical Implications
If you use AI to find evidence, is that evidence admissible in court?

* **The Black Box Problem:** If an AI says "he's the hacker" but can't explain *why*, it may fail the **Daubert Standard**.
* **Daubert Standard:** The U.S. legal test for whether expert/scientific testimony is admissible.
* **Facial Recognition Bias:** A real-world warning about AI producing racially biased results in law enforcement.

**Task Answers:**
1. What legal test used in the U.S. assesses whether expert or scientific testimony is admissible in court?
   * **Answer:** `Daubert`
2. What term describes AI models whose internal decision-making processes are difficult for humans to interpret?
   * **Answer:** `Black Box`
3. What real-world technology used by law enforcement has been shown to produce racially biased results?
   * **Answer:** `Facial Recognition`
4. What technique allows machine learning to be performed without transferring sensitive data to a central server?
   * **Answer:** `Federated Learning`

---

### 0x05: Task 5 - Practical (The Digital Trail)
*Launch the lab machine and open the "AI Forensic Assistant" tool.*

**Scenario:** You are investigating a data breach. You have 100,000 log entries.
1. Use the AI tool to perform **Anomaly Detection**.
2. Identify the suspicious IP address that the AI flagged as an outlier.
3. Observe the "Sentiment Shift" in the internal chat logs right before the exfiltration.
* **The Flag:** `THM{AI_THE_ULTIMATE_DETECTIVE}`
