---
draft: false
date: 2024-05-18
categories:
  - syntax
---

#Substitutable Syntax

`|`, `{ }` and `( )` when they are substitutable and when not.

<!-- more -->

## Quantified Constraint

The output is `True` or `False`.

Quantifiers are `all`, `some`, `no`, `one` and `lone`.

| | :white_check_mark: correct syntax | :no_entry_sign: wrong syntax |
| -- | -- | -- |
| basic form | `all a : A | F` | |
| substituted form | `all a : A { F }` | |
| substituted form | `all a : A | { F }` | |
| substituted form | `all a : A | ( F )` | |
| substituted form | `{all a : A | F}` | |
| substituted form | `{all a : A { F } }`
| substituted form | `(all a: A | F)` | |
| substituted form | `(all a: A { F } )` | |
| substituted form | `(all a: A { ( F ) } )` | |
| substituted form | | `all a: A (F)` |

### Sample Code #1

```
sig A {
  relation:  lone A
}

run {
  some a : A | #(a.relation) = 1 
  some a : A { #(a.relation) = 0 }
  no a : A | { #(a.relation) < 0 }
  (all a: A | (#a.relation) >= 0 )
}
```


## `let` Expression

The output is an expression or a constraint.

!!! question "my assumption"

    A `constraint` is just a kind of `expression` whose value is `True` or `False`.

!!! info "answer"

    > [Expressions are anything that returns a number, boolean, or set. Boolean expressions are also called Constraints.](https://alloy.readthedocs.io/en/latest/language/expressions-and-constraints.html#expressions)

| | :white_check_mark: correct syntax | :no_entry_sign: wrong syntax |
| -- | -- | -- |
| basic form | `let a = A | F` | |
| substituted form | `let a = A { F }` | |
| substituted form | `let a = A | { F }` | |
| substituted form | `let a = A | ( F )` | |
| substituted form | `{let a = A | F}` | |
| substituted form | `{let a = A { F } }`
| substituted form | `(let a = A | F)` | |
| substituted form | `(let a = A { F } )` | |
| substituted form | `(let a = A { ( F ) } )` | |
| substituted form | | `let a = A (F)` |

### Sample Code #2, `let` expression returns an expression

```
sig A {
  relation:  one A
}

run {
  some a : A | a.relation = ( let aa = a.relation.relation | aa )
}
```

### Sample Code #3, `let` expression returns an constraint

```
sig A {
  relation:  lone A
}

run {
  let AA = A {  some a : AA | some a.relation } 
  let AA = A |  some a : AA | no a.relation 
}
```


## Comprehension

Comprehension is a set builder. The output is a set.

| | :white_check_mark: correct syntax | :no_entry_sign: wrong syntax |
| -- | -- | -- |
| basic form | `{a : A | F}` | |
| substituted form | `{a : A {F}}`
| substituted form | `({a : A {F}})`
| substituted form | | `a: A | F` |
| substituted form | | `(a: A | F)` |
| substituted form | | `{a: A (F)}` |

### Sample Code #4, comprehension used in fun

```
sig A {
  relation:  lone A
}

fun hasRelation : A {
  { a : A | one a.relation} 
  //substituted form
  //{ a : A { one a.relation} }
}

fun noRelation : A {
  { a : A | no a.relation} 
  //substituted form
  //{ a : A { no a.relation} }
}

run {
  #hasRelation > 0
  #noRelation > 0
}
```

### Sample Code #5, comprehension used in expression

```
sig A {
  relation:  lone A
}

run {
  some { a : A | one a.relation} 
  some { a : A | no a.relation} 
}
```


