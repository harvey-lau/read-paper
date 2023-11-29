# The Extensive Reading of 2023-[*SelectFuzz: Efficient Directed Fuzzing with Selective Path Exploration*](https://ieeexplore.ieee.org/abstract/document/10179296)

- The **problem** is that existing directed fuzzers favor the inputs discovering new code regardless whether the newly uncovered code is relevant to the target code or not.
- The **solution** is SelectFuzz, a new directed fuzzer that selectively explores relevant program paths. It identifies 2 types of relevant code—path-divergent code and data-dependent code, that respectively captures the control- and data- dependency with the target code.

There are 2 main design details of SelectFuzz:

- **Distance metric** (refer to Algorithm 2 and Figure 3): it estimates the probability of reaching the target code.
- **Selective path exploration**: it selectively instruments and explores only code that is relevant to the fuzzing targets.
