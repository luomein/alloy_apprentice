---
draft: false
date: 2024-05-15
categories:
  - truth table
---

#Assertion and Counterexample

The truth table corresponds to facts and assertion whether counterexample found or not.

<!-- more -->

!!! note "[Software Abstractions]({{process.env.READTHEDOCS_CANONICAL_URL}}/Reference/Software_Abstractions/#page-144-in-the-case-of-an-assertion-the-analysis-constraint-is-the-negation-of-the-assertions-constraint-conjoined-with-the-facts-of-the-model-an-in-stance-is-a-counterexample-a-scenario-in-which-the-facts-hold-but-the-assertion-does-not)"

    In the case of an assertion, the analysis constraint is the negation of the assertion’s constraint conjoined with the facts of the model. An in- stance is a counterexample: a scenario in which the facts hold but the assertion does not.


## No counterexample found
| facts | assertion | counterexample | sample code |
| -- | -- | -- | -- |
| True | True | No counterexample found | sample code #1 |
| False | True | No counterexample found | sample code #2 |
| False | False | No counterexample found | sample code #3 |

### sample code #1

```
some sig A {}

fact {
  #A >= 0 // always true
}

assert test{
  #A >= 0 //always true
}

check test
```

### sample code #2

```
some sig A {}

fact {
  #A = 0 // always false
}

assert test{
  #A >= 0 //always true
}

check test
```

### sample code #3

```
some sig A {}

fact {
  #A < 0 // always false
}

assert test{
  #A < 0 //always false
}

check test
```

## Counterexample found
| facts | assertion | counterexample | sample code |
| -- | -- | -- | -- |
| True | False | Counterexample found | sample code #4 |

### sample code #4

```
some sig A {}

fact {
  #A >= 0 // always true
}

assert test{
  #A < 0 //always false
}

check test
```

