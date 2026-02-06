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

## Repository Structure

```
useless-locks-benchmark/
├── README.md
├── METHODOLOGY.md
├── AXES.md
├── SCORING.md
├── benchmarks/
│   ├── level_0_trivial/
│   ├── level_1_basic/
│   ├── level_2_intermediate/
│   ├── level_3_advanced/
│   └── level_4_expert/
└── results/
├── raw/
└── analysis/
```

Each benchmark test is fully documented and includes a ground-truth justification.

---