# Experiment Protocol

This document explains how to conduct the benchmark experiment and collect data for analysis.

## 1. Recommended LLMs to Test

For this benchmark, we recommend testing a mix of "General Purpose" and "Reasoning-Focused" models:

1.  **GPT-4.1 (OpenAI)**: The industry standard for general coding tasks. It provides a solid baseline for detection.
2.  **Claude Sonnet 4.5**: Currently considered one of the best models for precise architectural reasoning in programming and system-level tasks.
3.  **Gemini 3 Flash**: These models use "Chain of Thought" reasoning, which is particularly effective for discovering hidden invariants and multi-step concurrency logic.

---

## 2. Prompt Template

To ensure consistency, use the following prompt for every test. Provide the **full source code** (all `.c` and `.h` files) to the model.

**Prompt Template:**
```text
Analyze the following C multithreaded code. 
Your goal is to identify if any mutual exclusion mechanism (mutex/lock) is logically or semantically useless.

Provide your answer in the following format:
Result: [USELESS / SEMANTICALLY USELESS / NECESSARY]
Justification: [Your detailed reasoning]
```

---

## 3. How to Record Results

For each model and each test, please follow this folder structure to store the raw outputs:

```text
results/
└── raw/
    └── [MODEL_NAME]/
        └── level_[N]/
            └── test_[ID]/
                └── response.md (The model's full response)
```
