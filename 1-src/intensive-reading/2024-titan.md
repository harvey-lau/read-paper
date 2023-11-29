# The Intensive Reading of 2024-[*Titan: Efficient Multi-target Directed Greybox Fuzzing*](https://www.computer.org/csdl/proceedings-article/sp/2024/313000a059/1RjEaxqvmQ8)

## 0x01 Background

**Directed grey-box fuzzing**: Grey-box fuzzing is a popular automated vulnerability detecting technique. It takes improving code coverage as the goal and performs a *breadth-first search* on PUT. Because the more code coverage, the higher the possibility of discovering bugs. However, the proportion of code containing bugs is very small. This means that lots of computing resource used to improve code coverage are wasted. To solve this problem, directed grey-box fuzzing appeared. Directed grey-box fuzzer focuses on the target of PUT and tilts computing resource towards it, which performs *depth-first search* on PUT. From the perspective of *state space*, the *states* of coverage grey-box fuzzing is all paths while the *states* of directed grey-box fuzzing is some specific paths.

The **synergy ignorance** problem exists in multi-target directed grey-box fuzzing.

> **Synergy**: the interaction or cooperation of two or more organizations, substances, or other agents to produce a combined effect greater than the sum of their separate effects.

## 0x02 Motivating Example

```C
int foo() {
    unsigned a, b, c, d = parse_input();
    int flag;

    if (a > 5) {
        if (b > 1) {
            flag = 0;
        }
        else {
            flag = 1;
            if (...) {
                ...     // target-irrelevant
            }
        }
        ...
        if (flag) {
            target1();
        }
        else if (c > 2) {
            target2();  // contradict to flag == 1
        }
    }

    if (d > 3) {
        target3();
    }
}
```

- Reaching `target1()`: a > 5 && b <= 1 && any c && any d
- Reaching `target2()`: a > 5 && b > 1  && c > 2 && any d
- Reaching `target3()`: any a && any b  && any c && d > 3

Suppose there are 3 seeds:

- `A`: a, b, c, d = 6, 3, 1, 1
- `B`: a, b, c, d = 5, 0, 1, 1
- `C`: a, b, c, d = 3, 3, 3, 1

Based on the seed priority of existing approaches, `A` is the best seed. However, for each target:

- A: 2, 1, and 1 mutation(s)
- B: 1, 3, and 1 mutations(s)
- C: 2, 0, and 1 mutations(s)

`C` is better than `A`.

The main problem is that directed grey-box fuzzers don't distinguish the correlations between different targets.

Correlations among the targets:

- Overlapping: Target 1 (a > 5) && Target 2 (a > 5)
- Conflicting: Target 1 (a > 1) && Target 2 (a <= 1)
- Independent: Target 1 (a > 5) && Target 2 (b > 3)

## 0x03 Titan

### 1. Static Synergy Inference

- Precondition inference (refer to [Beacon](https://ieeexplore.ieee.org/abstract/document/9833751))
- Correlation inference

### 2. Synergy-aware Seed Scheduling

- Determine the targets influenced by seeds
- Determine the **potential** to reach the influenced targets

For target `t`:

$$
potential(t) =
\begin{cases}
    0, & \text{if }t \text{ has been triggered;} \\
    \dfrac {n(t)} {N(t)}, & \text{otherwise.}
\end{cases}
$$

where $n(t)$ is the number of satisfied preconditions for `t` observed when executing a seed, and $N(t)$ is the total number of preconditions inferred statically for `t`.

For seed `s`:

$$
potential(s) = \sum_{t \in T} potential(t)
$$

### 3. Multi-target-oriented Mutation

- Inferring the influenced bytes
- Mutating bytes for multiple targets

For byte `b` of seed `s`, the probability of choosing it:

$$
p(b) = \dfrac {inf(b)} {\sum_{b_i \in s} inf(b_i)}
$$

where $inf(b)$ is the number of its influenced targets that have not been triggered.

## 0x04 Evaluation

### 1. Reproducing Vulnerabilities

RQ1: how efficiently can Titan reproduce the vulnerabilities compared with other fuzzer?

See Table 4 and Table 5.

### 2. Detecting Incomplete Fix

See Table 6.

### 3. Correlation Inference

RQ2: how effectively do the correlations inferred by Titan help reproduce the vulnerabilities?

See Figure 5.

- Synergy-aware seed scheduling: see Table 7 and Figure 6.
- Multi-target-oriented mutation: see Figure 7.
- The precision of static analysis: see Figure 8.

### 4. Multiple Targets

RQ3: how effectively can Titan help other directed fuzzing for multiple targets?

See Figure 9.

### 5. Runtime Overhead

RQ4: what is the runtime overhead brought by Titan?

See Table 8.
