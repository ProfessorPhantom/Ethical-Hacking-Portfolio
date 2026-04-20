
# Path: AI Security 
## Room: AI Fundamentals

### 0x01: Executive Summary
The goal of this room is to establish a baseline understanding of how Artificial Intelligence (AI) and Machine Learning (ML) differ from traditional rule-based programming. From a security perspective, understanding the **inference process** and **data training** is critical for identifying future attack vectors like Model Inversion.

### 0x02: Technical Architecture
To understand the security risks, we must distinguish between the layers of the technology:

* **Artificial Intelligence (AI):** The umbrella term for machines mimicking cognitive functions.
* **Machine Learning (ML):** Systems that improve performance by identifying patterns in data without being explicitly programmed for every scenario.
* **Deep Learning (DL):** A subset of ML utilizing multi-layered Neural Networks to process complex data.



[Image of Artificial Intelligence vs Machine Learning vs Deep Learning diagram]


### 0x03: The "Aha!" Moment for Security
In traditional software, we audit **Code**. In AI/ML, we must audit **Data and Weights**. 
* **The Risk:** If the training data is biased or "poisoned," the model’s output becomes a vulnerability itself.
* **Key Concept:** Neural Networks function as "Black Boxes"—even the developers often cannot explain *why* a specific neuron fired. This lack of transparency is a major security challenge.

### 0x04: Conclusion
Before moving to active exploits (like Prompt Injection), a researcher must understand that the "vulnerability" often lies in the model's fundamental training, not just its code.
