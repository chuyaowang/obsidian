# Gemini 3 Features

#agent 
[Gemini 3 Developer Guide](https://ai.google.dev/gemini-api/docs/gemini-3)

Based on the official developer guide, here are the new features of the Gemini 3 model family and their intended use cases.

### New Features in Gemini 3

**1. Thinking Levels (`thinking_level`)**
Gemini 3 uses dynamic thinking by default to reason through problems. You can now control the depth of this internal reasoning process.

* **Levels:** `low` (faster, cheaper), `high` (default, maximum reasoning), and for Flash models: `minimal` (near-instant) and `medium` (balanced).
* **Benefit:** Allows developers to trade off between latency/cost and reasoning depth.

**2. Thought Signatures (`thoughtSignature`)**
These are encrypted strings returned by the model representing its internal "train of thought."

* **How it works:** You must pass these signatures back to the model in subsequent API calls (chat history) to maintain its reasoning state.
* **Strictness:** It is strictly required for **Function Calling** and **Image Generation** (missing it causes errors). It is optional but recommended for standard text chat to improve answer quality.

**3. Granular Media Resolution (`media_resolution`)**
You can now control how many tokens are allocated to process images or video frames.

* **Levels:** `low`, `medium`, `high`, `ultra_high`.
* **Benefit:** Gives control over the balance between cost/speed and the model's ability to see fine details (like small text in a video).

**4. New Model Variants**

* **Gemini 3 Pro:** Best for complex reasoning and broad world knowledge.
* **Gemini 3 Flash:** Pro-level intelligence but faster and cheaper.
* **Nano Banana Pro:** A specialized high-quality image generation model.

**5. Temperature Default (1.0)**

* Unlike previous models where tuning temperature (creativity) was common, Gemini 3 is optimized to run at `temperature=1.0`. Lowering it is discouraged as it may degrade reasoning performance.

---

### Use Cases & Best Practices

| Feature / Setting | Ideal Use Case |
| --- | --- |
| **Thinking Level: `low` / `minimal**` | **Chatbots & Simple Commands:** High-throughput applications where speed is critical and complex reasoning isn't needed (e.g., "What is the capital of France?"). |
| **Thinking Level: `high**` | **Coding & Logic:** Finding bugs in multi-threaded code, complex math, or scientific reasoning where accuracy matters more than speed. |
| **Thought Signatures** | **Agentic Workflows:** Multi-step tasks where an agent must remember *why* it made a decision in step 1 (e.g., checking a flight delay) to inform step 2 (booking a taxi). |
| **Media Resolution: `high**` | **OCR & Detailed Vision:** Reading dense text in a scanned document or identifying small objects in a text-heavy video. |
| **Media Resolution: `low` / `medium**` | **General Video Understanding:** Recognizing general actions in a video (e.g., "A person is running") where fine text details are irrelevant. |