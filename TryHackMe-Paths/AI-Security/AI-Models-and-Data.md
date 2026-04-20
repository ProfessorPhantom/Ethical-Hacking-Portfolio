
# Path: AI Security
## Room: AI Models & Data

### 0x01: Understanding the "Model"
A "model" is essentially a mathematical function. In this room, we learn that a model isn't a piece of software in the traditional sense; it is a massive file of **parameters** (weights and biases) that has been "frozen" after training.

### 0x02: Task 3 - Data Representation (Tensors)
In AI, everything—text, images, and audio—must be converted into numbers. 
* **Scalar:** A single number.
* **Vector:** A list of numbers.
* **Matrix:** A grid of numbers.
* **Tensor:** A multi-dimensional array of numbers (the "DNA" of modern AI).

**Task Answers:**
1. What is a multi-dimensional array used to represent data in deep learning?
   * **Answer:** `Tensor`
2. Which term refers to a 1D array of numbers?
   * **Answer:** `Vector`

---

### 0x03: Task 4 - Feature Engineering & Vectorization
This is how we turn "Hello" into something a computer can calculate. **Word Embeddings** map words into a multi-dimensional space where words with similar meanings are mathematically "close" to each other.



* **Key Concept:** If "King" - "Man" + "Woman" = "Queen", the model has successfully mapped the relationship between those features.

**Task Answers:**
1. What is the process of converting raw data into a numerical format suitable for a model?
   * **Answer:** `Vectorization` (or `Encoding`)
2. What do we call the numerical representation of words where similar words are closer in distance?
   * **Answer:** `Word Embeddings`

---

### 0x04: Task 5 - Weights, Biases, and Parameters
When we "hack" a model's logic, we are essentially fighting against its **Weights**. 
* **Weights:** Determine the strength of the connection between neurons.
* **Biases:** Allow the model to shift the activation function to better fit the data.

**Task Answers:**
1. What are the adjustable values within a neural network that are optimized during training?
   * **Answer:** `Parameters`
2. Which specific parameter is added to the weighted sum of inputs to adjust the output?
   * **Answer:** `Bias`

---

### 0x05: Task 6 - Model Architectures (CNNs vs RNNs)
Different "brains" for different tasks:
* **CNN (Convolutional Neural Network):** Best for **Images** (Spatial data).
* **RNN (Recurrent Neural Network):** Best for **Sequences** (Text/Audio).

**Task Answers:**
1. Which type of neural network is primarily used for image recognition tasks?
   * **Answer:** `CNN` (Convolutional Neural Network)
2. What type of model architecture is designed to handle sequential data?
   * **Answer:** `RNN` (Recurrent Neural Network)

---

### 0x06: Lab Flag (The Data Analysis)
*Open the Jupyter Notebook or Lab Environment provided in the room.*
1. Follow the instructions to load the dataset.
2. Run the provided Python script to visualize the model's performance.
3. Observe the output of the final cell.
* **The Flag:** `THM{DATAFRAMES_AND_TENSORS}`
   *(Note: Double-check the flag in your specific lab instance).*
