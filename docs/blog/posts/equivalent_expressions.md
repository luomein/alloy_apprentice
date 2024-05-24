---
draft: false
date: 2024-05-24
categories:
  - syntax
---

# Equivalent expressions

Use `<=>` to check whether two expressions are equivalent. 

<!-- more -->

## sample code #1, size constraints and their equivalences

```
sig A {}

assert equivalence{
 some A <=> #A > 0
 no A <=> #A = 0
 one A <=> #A = 1
 lone A <=> #A <= 1
}

check equivalence
```

## sample code #2, quantified constrains and their equivalences

Use comprehension (a kind of set builder) in the equivalences

```
sig A {
  relation:  set A
}
pred expr[a: A]{
  a in a.relation
}
assert equivalence{
  ( some a : A | expr[a] ) <=> ( #{ a : A | expr[a] } > 0 )
  ( no a : A | expr[a] ) <=> ( #{ a : A | expr[a] } = 0 )
  ( one a : A | expr[a] ) <=> ( #{ a : A | expr[a] } = 1 )
  ( lone a : A | expr[a] ) <=> ( #{ a : A | expr[a] } <= 1 )
  ( all a: A | expr[a]) <=> ( #{ a: A | expr[a] } = #A )
}

check equivalence
```

## sample code #3, none equivalent

This code will generate counterexample. So `(one a1, a2 : A | expr[a1 , a2] )` and `(one a1: A | one a2: A | expr[a1, a2])` are not equivalent.


```
sig A {
  relation:  set A
}
pred expr[a1: A, a2: A]{
  a2 in a1.relation
}
assert equivalence{
 (one a1, a2 : A | expr[a1 , a2] ) <=> (one a1: A | one a2: A | expr[a1, a2])
}
check equivalence

```

Let's construct a counterexample.

| Expression | Boolean |
| -- | -- |
| `a1 in A` | True |
| `a2 in A`| True |
| `a1 in a1.relation` | False |
| `a1 in a2.relation` | True
| `a2 in a1.relation` | True |
| `a2 in a2.relation` | True |
| `expr[a1 , a1]` | False |
| `expr[a1 , a2]` | True |
| `expr[a2 , a1]` | True |
| `expr[a2 , a2]` | True |
|  `(one a1, a2 : A | expr[a1 , a2] )` | False |
|  `(one a1: A | one a2: A | expr[a1, a2])` | True |

The reason for ` (one a1, a2 : A | expr[a1 , a2] ) ` to be false is because there are 3 pairs to make `expr` to be true, not one pair.

The reason for ` (one a1: A | one a2: A | expr[a1, a2]) ` to be true is because there is only one pair to meet this criteria. That happens to be, a1 = a1 and a2 = a2.
