# valid
> [In logic, specifically in deductive reasoning, an argument is valid if and only if it takes a form that makes it impossible for the premises to be true and the conclusion nevertheless to be false. It is not required for a valid argument to have premises that are actually true, but to have premises that, if they were true, would guarantee the truth of the argument's conclusion.](https://en.wikipedia.org/wiki/Validity_(logic))
P->Q
Table
## `assert` and `check`
In Alloy, `fact` is the premises, `assert` is the conclusion and `check` is to check the validity between the premises and the conclusion.

If the `fact` is false, `check` would always return valid. It will show, 
>  No counterexample found. Assertion may be valid. 
```
fact {
  1 = 2
}
assert any_assertion {
  1 = 2
  1 != 2
}
check  any_assertion
```
## `all`
`all a : A | =>`