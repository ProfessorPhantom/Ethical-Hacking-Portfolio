
# Path: AI Security
## Room: Prompt Engineering (Verified Source of Truth)

### 0x01: Introduction
Prompt engineering is the art and science of crafting inputs that guide an LLM toward a specific, reliable output. In a security context, this is how we build defensive filters and how we begin to understand the mechanics of "Jailbreaking."

---

### 0x02: Task 2 - LLM Fundamentals
Before engineering prompts, we must understand the "physics" of the model.

* **Tokens:** The smallest units an LLM processes. A token is roughly 4 characters or 0.75 of a word.
* **Temperature:** Controls randomness. A value of `0.0` makes the model deterministic (consistent); higher values make it creative.
* **Context Window:** The model's "short-term memory." If your prompt + logs are too long, the model "forgets" the beginning.

**Task Answers:**
1. What is the term for the smallest units that an LLM breaks text into in order to process it?
   * **Answer:** `tokens`
2. What parameter would you set to 0.0 to make an LLM behave as close to deterministic as possible?
   * **Answer:** `temperature`
3. What parameter restricts which tokens the model considers by limiting selection to a cumulative probability mass?
   * **Answer:** `top-p`
4. What term describes the maximum working memory of an LLM, measured in tokens?
   * **Answer:** `context window`

---

### 0x03: Task 3 - The Anatomy of a Prompt (The Four Pillars)
Every professional prompt must have a clear structure to reduce "hallucinations."

1. **Instruction:** The core command (e.g., "Analyze these logs").
2. **Context:** Background info (e.g., "You are a SOC analyst").
3. **Constraints:** Rules (e.g., "Do not include markdown").
4. **Output Format:** How the answer looks (e.g., "Respond in JSON").

**Task Answers:**
1. Which pillar instructs the model on how the answer should be structured?
   * **Answer:** `output format`
2. Which pillar specifies rules or limits imposed on the model's response?
   * **Answer:** `constraints`
3. Which pillar provides the AI with relevant background information or scenario?
   * **Answer:** `context`
4. Which pillar defines the core command or action you want the AI to perform?
   * **Answer:** `instruction`

---

### 0x04: Task 4 - System vs. User Prompts
This is the most important concept for **Prompt Injection**.
* **System Prompt:** The "Prime Directive" set by developers. It is persistent and hard-coded.
* **User Prompt:** The input from the end-user.
* **Instruction Hierarchy:** The rule that says System Prompts should *always* have priority over User Prompts (though this is what we try to break in hacking).

**Task Answers:**
1. What type of prompt is developer-defined, persistent, and remains constant across all sessions?
   * **Answer:** `System prompt`
2. What is the term for the intended order of priority between system and user instructions in an LLM application?
   * **Answer:** `instruction hierarchy`

---

### 0x05: Task 5 - Advanced Prompting Techniques
* **Zero-shot:** Asking a task with no examples.
* **Few-shot:** Providing a few examples to guide the model.
* **Chain-of-Thought (CoT):** Asking the model to "think step-by-step."

**Task Answers:**
1. What is the term for the prompting technique introduced by Google researchers in 2022 that asks models to break tasks into intermediate reasoning steps?
   * **Answer:** `Chain-of-Thought`
2. What prompting technique involves providing no examples and relying entirely on the model's pre-trained knowledge?
   * **Answer:** `Zero-shot`
3. What prompting technique involves saving and reusing a standardised prompt structure for recurring tasks?
   * **Answer:** `Prompt templates`
4. What simple phrase can be added to a prompt to trigger Zero-shot Chain-of-Thought reasoning?
   * **Answer:** `Let's think step by step`

---

### 0x06: Task 6 - The Challenge (The Flag)
*Interact with the challenge bot. You must achieve a high score by detecting phishing/SQLi using the techniques above.*

1. **Strategy:** Use a "Persona" (Context) + "Step-by-step" (CoT) + "JSON" (Format).
2. **Result:** Once the bot is satisfied with your accuracy...
* **The Flag:** `THM{PROMPT_ENGINEER_MASTER}`
