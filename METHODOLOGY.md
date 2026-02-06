# Methodology

This document describes the scientific methodology used to construct and evaluate the benchmark.

---

## Core Principle

For each benchmark test, the usefulness or uselessness of a lock is determined **a priori**, independently of any LLM output.  
LLMs are evaluated against a fixed ground truth and are never used to establish correctness.

---

## Definition: Useless Lock

A lock is considered *useless* if removing it:

- Does not introduce any data race
- Does not violate any program invariant
- Does not change the functional correctness of the program

Performance, scheduling, or output ordering differences are **not** considered correctness violations unless explicitly stated by the program’s semantic contract.

---

## Experimental Axes

Each test is characterized along five independent axes:

1. Structural visibility
2. Concurrency model
3. Write behavior
4. Semantic invariants
5. Syntactic obfuscation

Only one axis is increased at a time when moving between difficulty levels, ensuring interpretability of results.

The full definition of each axis is provided in `AXES.md`.

---

## Difficulty Levels

The benchmark is divided into five difficulty levels:

- **Level 0 – Trivial**: obvious useless locks, sanity checks
- **Level 1 – Basic**: simple multithreading and read-only access
- **Level 2 – Intermediate**: multi-file structure, initialization-only writes
- **Level 3 – Advanced**: hidden single-writer patterns, implicit invariants
- **Level 4 – Expert**: indirect calls, macros, callbacks, distributed invariants

---

## Test Structure

Each test directory contains:

- Source code (`src/`)
- Axis characterization (`AXIS.json`)
- Expected outcome and justification (`EXPECTED.md`)
- A short test-specific README

This ensures reproducibility and independent verification.

---

## Evaluation Protocol (LLMs)

LLMs are provided with the full source code of a test and a minimal prompt asking whether any lock is useless, along with a justification.

No hints about invariants, thread counts, or expected difficulty are provided unless explicitly stated by the test.

---

## Interpretation of Results

Results are analyzed per axis and per difficulty level to identify:

- Failure thresholds
- Common reasoning errors
- Sensitivity to structural vs semantic complexity

The goal is not to rank models absolutely, but to understand *where* and *why* they succeed or fail.
