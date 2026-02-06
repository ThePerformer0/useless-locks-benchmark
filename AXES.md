# Benchmark Axes

This document defines the five axes used to characterize the difficulty of each benchmark test.

---

## Axis A — Structural Visibility

Measures how easily the relevant code can be understood locally.

| Level | Description |
|------|-------------|
| 0 | Single function |
| 1 | Single source file |
| 2 | Multiple source files |
| 3 | Multiple modules or libraries |
| 4 | Indirect calls across abstraction layers |

---

## Axis B — Concurrency Model

Measures how explicit the concurrency structure is.

| Level | Description |
|------|-------------|
| 0 | No threads |
| 1 | Threads explicitly created |
| 2 | Threads created indirectly |
| 3 | Single effective writer enforced structurally |
| 4 | Global structural constraints on concurrency |

---

## Axis C — Write Behavior

Measures how and when shared data is modified.

| Level | Description |
|------|-------------|
| 0 | No writes |
| 1 | Initialization only |
| 2 | Single writer thread |
| 3 | Multiple writers, sequentially constrained |
| 4 | Conditional or context-dependent writers |

---

## Axis D — Semantic Invariants

Measures the complexity of the program’s correctness conditions.

| Level | Description |
|------|-------------|
| 0 | No invariant |
| 1 | Trivial invariant |
| 2 | Implicit invariant |
| 3 | Distributed invariant |
| 4 | External or contract-based invariant |

---

## Axis E — Syntactic Obfuscation

Measures how much the code structure obscures reasoning.

| Level | Description |
|------|-------------|
| 0 | Direct code |
| 1 | Function abstraction |
| 2 | Macros |
| 3 | Callbacks |
| 4 | Function pointers or dynamic dispatch |

---

## Notes

Axes are designed to be orthogonal.  
A test’s difficulty is not a single scalar value, but a vector across these axes.
