
# Path: AI Security
## Room: AI Models & Data (Verified Source of Truth)

### 0x01: Introduction
This room moves away from the "how it works" math and into the **Data Supply Chain**. The core lesson for students is that an AI model inherits every security flaw, bias, and credential leak present in its training data.

---

### 0x02: Task 2 - Training Data & Provenance
Before a model is built, data is collected. If we don't know where it came from, we can't trust the model.

* **Data Provenance:** The ability to trace the origin, time of collection, and any modifications made to a dataset.
* **Common Crawl:** The massive public web-scraping corpus used to train almost all major LLMs.
* **ML-BOM:** The Machine Learning Bill of Materials (similar to an SBOM in software).

**Task Answers:**
1. What term describes the ability to answer where data came from, when it was collected, and whether it has been modified?
   * **Answer:** `Data Provenance`
2. What is the name of the most widely used public corpus that underpins essentially every major model family?
   * **Answer:** `Common Crawl`
3. What is the AI equivalent of a Software Bill of Materials (SBOM), used to document dataset sources, licenses, and filtering decisions?
   * **Answer:** `ML-BOM`

---

### 0x03: Task 3 - Building the Model (Key Concepts)
This task covers the "Checkpoints" during model creation that introduce specific risks like **Overfitting**.

* **Epoch:** One complete pass of the training algorithm through the entire dataset.
* **Overfitting:** When a model "memorizes" the training data (including sensitive info) instead of learning patterns.
* **Quantization:** Reducing the precision of model weights (e.g., from 32-bit to 4-bit) to save memory—this can sometimes break safety guardrails.
* **Federated Learning:** Training across decentralized devices (like phones) to keep raw data private.

**Task Answers:**
1. What term describes one complete pass of the training algorithm through the entire dataset?
   * **Answer:** `Epoch`
2. What problem occurs when a model memorizes training data rather than learning general patterns?
   * **Answer:** `Overfitting`
3. What post-training optimization technique reduces the numerical precision of model weights?
   * **Answer:** `Quantisation`
4. What training approach trains a model across decentralized devices?
   * **Answer:** `Federated Learning`

---

### 0x04: Task 4 - The Inheritance Problem
Most companies don't build models from scratch; they use **Pre-trained Models** and perform **Fine-tuning**. This means they "inherit" any backdoors or biases in the original model.

**Task Answers:**
1. What is the process of taking a pre-trained model and continuing to train it on a smaller, task-specific dataset?
   * **Answer:** `Fine-tuning`
2. What term describes a model that has already been trained on a large general-purpose dataset?
   * **Answer:** `Pre-trained Model`

---

### 0x05: Task 5 - The Black Box Problem
Because models are opaque, we use **Model Cards** to provide a "Nutrition Label" for the AI.

**Task Answers:**
1. What documentation artifact accompanies a model to describe what it is, how it was built, and where it falls short?
   * **Answer:** `Model Card`
2. What are the billions of floating-point numbers that make up a trained model collectively referred to as?
   * **Answer:** `Weights`

---

### 0x06: Task 6 - Practical Lab
*Launch the lab machine and interact with the provided interface to audit the model card.*

1.  Analyze the **Model Card** provided in the web interface.
2.  Look for the specific versioning and filtering details mentioned in the lab prompt.
* **The Flag:** `THM{DATA_PROVENANCE_MATTERS}` 
    *(Note: Always verify the flag in your active instance).*
