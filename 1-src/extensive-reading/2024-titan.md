# The Extensive Reading of 2024-[*Titan: Efficient Multi-target Directed Greybox Fuzzing*](https://www.computer.org/csdl/proceedings-article/sp/2024/313000a059/1RjEaxqvmQ8)

- The **problem** is that modern directed fuzzing often faces scalability issues when analyzing multiple targets in a program simultaneously.
- The **solution** is Titan, which enables fuzzers to distinguish correlations among various targets.

Potential correlations among the targets:

- Overlapping: Target 1 (a > 5) && Target 2 (a > 5)
- Conflicting: Target 1 (a > 1) && Target 2 (a <= 1)
- Independent: Target 1 (a > 5) && Target 2 (b > 3)

At a high level, Titan consists of 2 stages:

1. **Static analyzer** infers the correlations among multiple targets based on their path conditions.
2. **Synergy-aware fuzzer** generates inputs for multiple targets.

These correlations are leveraged for seed scheduling and mutation.
