# Useless Locks Benchmark

This repository contains a scientific benchmark designed to evaluate the ability of Large Language Models (LLMs) to detect *useless mutual exclusion mechanisms* (locks) in multithreaded programs.

Locks are widely used to ensure determinism and prevent race conditions in concurrent software. However, unnecessary locks can introduce avoidable latency and complexity. Such locks frequently appear in real-world code bases due to defensive programming, legacy code, automated refactoring, or the use of third-party libraries and generative AI tools.

The goal of this benchmark is **not** to detect race conditions, but to identify situations where mutual exclusion mechanisms are *logically unnecessary*, even though they appear correct and well-structured.

---

## Objectives

The benchmark aims to:

- Evaluate how well LLMs can reason about concurrency, synchronization, and program semantics.
- Measure performance across increasing levels of structural and semantic complexity.
- Identify which aspects of concurrency reasoning are most challenging for current models.
- Provide a reproducible and extensible dataset for future research.

---

## Scope

- Language: **C (POSIX threads)**
- Focus: **mutexes and shared-memory concurrency**
- Analysis type: **static reasoning over source code**
- Target systems: representative of real-world software (servers, runtimes, OS components)

Python is intentionally excluded from the core benchmark due to the Global Interpreter Lock (GIL), which can obscure true concurrency behavior and bias the analysis.

---

## Levels of Complexity

The benchmark is organized into 5 levels, each targeting specific reasoning patterns:

1.  **[Level 0: Trivial](benchmarks/level_0_trivial/README.md)** - Local variables, empty critical sections.
2.  **[Level 1: Basic](benchmarks/level_1_basic/README.md)** - Join-based synchronization, read-after-init patterns.
3.  **[Level 2: Intermediate](benchmarks/level_2_intermediate/README.md)** - Module-level initialization, barrier synchronization.
4.  **[Level 3: Advanced](benchmarks/level_3_advanced/README.md)** - Semantic redundancy (idempotency, approximate monitoring).
5.  **[Level 4: Expert](benchmarks/level_4_expert/README.md)** - Distributed/Structural invariants (hierarchical locking, callback chains).

---

## Results & Analysis (Feb 2026)

We evaluated three state-of-the-art models using the standard protocol defined in `PROTOCOL.md`.

### Performance Overview

| Model | Level 0 | Level 1 | Level 2 | Level 3 | Level 4 | Total |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Claude Sonnet 4.5** | 3/3 | 3/3 | 3/3 | 2/3 | 3/3 | **14/15** |
| **GPT-4.1** | 3/3 | 3/3 | 3/3 | 0/3 | 2/3 | **11/15** |
| **Gemini 3 Flash** | 3/3 | 3/3 | 3/3 | 1/3 | 1/3 | **11/15** |

### Key Insights

1.  **The "Semantic Gap" (Level 3)**: Most models struggle with *semantically* useless locks. For instance, **GPT-4.1** correctly identifies that a lock protects shared data, but fails to recognize that the data is *idempotent* or *non-critical* (approximated metrics). It adheres strictly to the C memory model ("Any unsynchronized write is UB"), missing the higher-level engineering context.
2.  **Structural Reasoning (Level 4)**: **Claude** and **GPT-4.1** showed high proficiency in detecting redundant locks in hierarchical systems (where a parent lock already guarantees safety), whereas **Gemini 3 Flash** often missed these "outer-layer" invariants.
3.  **Legacy Artifacts**: All models handled cases where locks protected immutable data or local variables (Level 0/2) with high accuracy, indicating that basic data-flow analysis is well-integrated into these models.

---

## Repository Structure

```
useless-locks-benchmark/
├── README.md
├── METHODOLOGY.md
├── AXES.md
├── benchmarks/
│   ├── level_0_trivial/
│   ├── level_1_basic/
│   ├── level_2_intermediate/
│   ├── level_3_advanced/
│   └── level_4_expert/
└── results/
```

Each benchmark test is fully documented and includes a ground-truth justification.

---

## How to Run the Benchmark

See **[PROTOCOL.md](PROTOCOL.md)** for detailed instructions on how to prompt LLMs and record results.

## Contributing

We welcome new test cases! Please refer to **[METHODOLOGY.md](METHODOLOGY.md)** and **[AXES.md](AXES.md)** before submitting a Pull Request.