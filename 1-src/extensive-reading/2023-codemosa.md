# The Extensive Reading of 2023-[*CodaMosa: Escaping Coverage Plateaus in Test Generation with Pre-trained Large Language Models*](https://ieeexplore.ieee.org/document/10172800)

- The **problem** is whether Large Language Models (LLMs) of code, such as OpenAI's Codex, can be used to help the exploration of Search-Bases Software Testing (SBST).
- The **solution** is CodaMosa, a algorithm conducts SBST until its coverage improvements stall, then asks Codex to provide example test cases for under-covered functions.

An example is shown as below.

Module under Test:

```Python
<...omitted code...>

def _build_version_bump_position(pos: int) -> int:
    pos_min = -3
    pos_max = 2
    if (pos_min <= pos <= pos_max) is False:
        raise ValueError("Invalid position") # uncovered 1
    # Turn position into a positive number
    if pos < 0:
        pos_max += 1         # uncovered 2
        return pos_max + pos # uncovered 2
    return pos

<...omitted code...>

def bump_version(version: str, pos: int = 2,
                 pre_release: Optional[str] = None) -> str:
    ver_info = _build_version_info(version)
    pos = _build_version_bump_position(pos)
    bump_type = _build_version_bump_type(pos, pre_release)
    <...omitted code...>
    return out
```

The test cases at Coverage Plateaus:

```Python
def test_case_1():
    str_0 = 'a\t!sUo~AU'
    str_1 = bump_version(str_0)
```

```Python
def test_case_2():
    str_0 = None
    int_0 = 1431
    str_1 = bump_version(str_0, int_0)
```

Hint from LLM:

```Python
def test_bump_version():
    assert bump_version('0.0.0') == '1.0.0'
    assert bump_version('0.0.0', 1) == '0.1.0'
```

Deserialization:

```Python
def test_case():
    str_0 = '0.0.0'
    str_1 = bump_version(str_0)
    int_0 = 1
    str_2 = bump_version(str_0, int_0)
```

The test cases **escaping** Coverage Plateaus:

```Python
def test_case_mutant_0():
    str_0 = '0.0.0'
    str_1 = bump_version(str_0)
    int_0 = -1    # uncovered 1
    str_2 = bump_version(str_0, int_0)
```

```Python
def test_case_mutant_n():
    str_0 = '0.0.0'
    str_1 = bump_version(str_0)
    int_0 = -2687    # uncovered 2
    str_2 = bump_version(str_0, int_0)
```

Authors control LLM generations via prompts. A prompt is the input text that is passed to the LLM at inference time. The LLM generates text following the prompt until it generates a predetermined stop word or exceeds its maximum word limit.

Researchers have applied Codex to a variety of new tasks—code completion, code explanation, and code repair—without having to retrain Codex. CodeMosa uses Codex to generate test cases via prompt engineering.
