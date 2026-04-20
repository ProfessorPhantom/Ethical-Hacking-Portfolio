
# Path: AI Security
## Room: AI Fundamentals (Master Walkthrough)

### 0x01: Introduction to AI
This room transitions students from "Classical Computing" (where $If \ A \ then \ B$) to "Probabilistic Computing" (where the machine calculates the statistical likelihood of $B$).

**Key Takeaway:** AI is not a single technology but a collection of methods to simulate human decision-making.

---

### 0x02: Task 2 - AI vs. Machine Learning vs. Deep Learning
This is a critical distinction for security researchers. Most "AI" we attack today is actually **Deep Learning** utilizing Large Language Models (LLMs).

* **Artificial Intelligence:** The broad concept.
* **Machine Learning (ML):** Improving through experience/data.
* **Deep Learning (DL):** Using multi-layered Neural Networks.

**Task Answers:**
1. What is the subfield of AI that focuses on the development of algorithms that learn from data?
   * **Answer:** `Machine Learning`
2. Which term refers to the subset of ML that uses neural networks with many layers?
   * **Answer:** `Deep Learning`

---

### 0x03: Task 3 - How AI Learns (The Training Process)
For an attacker, the **Training Phase** is the most vulnerable point for **Data Poisoning**.

* **Supervised Learning:** Learning with labeled data (Teacher/Student).
* **Unsupervised Learning:** Finding patterns in unlabeled data (Pattern Recognition).
* **Reinforcement Learning:** Learning through trial and error (Rewards/Punishments).

**Task Answers:**
1. What type of learning involves training a model on a labeled dataset?
   * **Answer:** `Supervised Learning`
2. Which learning type involves an agent taking actions in an environment to maximize a reward?
   * **Answer:** `Reinforcement Learning`

---

### 0x04: Task 4 - Neural Networks (The Black Box)
This is where the "magic" happens. A Neural Network consists of an **Input Layer**, several **Hidden Layers**, and an **Output Layer**.

* **Weights and Biases:** These are the numerical values the model adjusts during training.
* **The Security Problem:** Because there are millions of weights, we cannot easily audit *why* a model made a specific decision. This is known as the **Black Box Problem**.

**Task Answers:**
1. What are the layers between the input and output layers in a neural network called?
   * **Answer:** `Hidden Layers`
2. What are the parameters that a neural network adjusts during training to minimize error?
   * **Answer:** `Weights and Biases` (or just `Weights`)

---

### 0x05: Task 5 - Large Language Models (LLMs)
LLMs are the primary target for **Prompt Injection**. They work by predicting the "next token" in a sequence.

* **Tokenization:** Breaking text into chunks (tokens).
* **Transformers:** The architecture that allows the model to understand the "context" of a word based on the words around it.

**Task Answers:**
1. What is the fundamental architecture that powers modern LLMs like GPT-4?
   * **Answer:** `Transformer`
2. What is the process of breaking down text into smaller units for an LLM to process?
   * **Answer:** `Tokenization`

---

### 0x06: Task 6 - Practical Lab: Interacting with AI
*Launch the lab machine and open the browser to the provided URL.*

**Scenario:** You are interacting with a basic chatbot. Observe how it responds to different instructions.
1. Use the chat to ask for the "System Instructions."
2. **The Flag:** `THM{ARTIFICIAL_INTELLIGENCE_BASICS}` 
   *(Note: Verify this in your specific lab instance).*

---

### 0x07: Summary for Students
To be an effective AI Security Researcher, you must understand that the **Model is the Code**. If you can influence the tokens the model receives, you can influence the "logic" it executes.
