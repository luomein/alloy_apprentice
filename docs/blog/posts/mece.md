---
draft: false
date: 2024-05-24
categories:
  - set theory
---

# MECE Principle (mutually exclusive and collectively exhaustive)

In Alloy, it is very handy to check whether MECE establishes or not. 

<!-- more -->

## key words

* `fun` works as a set builder

* `disj` can check several subsets at once to see if they are mutually disjoint or not

* `extends` extends an `abstract sig` to mutually exclusive and collectively exhaustive subsets  

## sample code #1, using set builder `fun`

```
sig A {
  relation:  set A
}

fun oneRelation : A {
  { a : A | one a.relation} 

}
fun loneRelation : A {
  { a : A | lone a.relation} 

}
fun someRelation : A {
  { a : A | some a.relation} 
}
fun multipleRelations : A {
  { a : A | #(a.relation) > 1 } 
}
fun noRelation : A {
  { a : A | no a.relation}
}

assert mutual_exclusive {
 disj[ multipleRelations ,  oneRelation , noRelation ]
}
assert collectively_exhaustive {
 A = multipleRelations + oneRelation + noRelation
}

check collectively_exhaustive
check mutual_exclusive

```

## sample code #2, using `extends` and `abstract sig`

```
abstract sig A {}

sig A1, A2, A3 extends A {}

assert mutual_exclusive {
 disj[ A1 , A2 , A3]
}
assert collectively_exhaustive {
 A = A1 + A2 + A3
}

check collectively_exhaustive
check mutual_exclusive
```

## the combination of `extends`, `in` and `abstract sig`

Showing when there is counterexample of mece

| `extends` or `in` | `abstract sig` or `sig` | sample |  mutually exclusive | collectively exhaustive |
| -- | -- | -- | -- | --|
| `extends` | `abstract sig` | `abstract sig A {}`<br>`sig A1, A2 extends A {}` | :white_check_mark: | :white_check_mark: | 
| `extends` | `sig` |   `sig A {}`<br>`sig A1, A2 extends A {}` |  :white_check_mark: |  :no_entry_sign: <br>counterexample found |
| `in` |  `abstract sig` | `abstract sig A {}`<br>`sig A1, A2 in A {}` | :no_entry_sign: <br>counterexample found  | :no_entry_sign: <br>counterexample found  | 
| `in` |  `sig` | `sig A {}`<br>`sig A1, A2 in A {}` | :no_entry_sign: <br>counterexample found  | :no_entry_sign:  <br>counterexample found | 


## set theory : partition of a set

[wikipedia](https://en.wikipedia.org/wiki/Partition_of_a_set)

> In mathematics, a partition of a set is a grouping of its elements into non-empty subsets, in such a way that every element is included in exactly one subset.

In a partition of a set, the non-empty subsets are mutually exclusive and collectively exhaustive.  

