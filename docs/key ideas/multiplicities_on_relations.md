---
hide:
  - tags
tags:
  - relation
---
# multiplicities on relations

```
r: A m -> n B
```

The `m` and `n` are multiplicities on relations. It could be either one of the values, `set`, `some`, `one`and `lone`.

* > Multiplicities are just a shorthand, and can be replaced by standard constraints.

    Reference source (1)
    { .annotate }

    1. [Software Abstractions](/Reference/Software_Abstractions/#page-77-multiplicities-are-just-a-shorthand)

* > If not specified, the multiplicities are assumed to be `set`.

    Reference source (1)
    { .annotate }

    1. [Alloy Documentation](/Reference/Alloy_Documentation/#multirelations)

    Which means, if not specified, like `r: A -> B`, there is no constraints.

* > injective, `A lone -> B`

    > entire, `A -> some B`

    > simple, `A -> lone B`

    > surjective, `A some -> B`

    Reference source (1)
    { .annotate}

    1. [Formal Software Design with Alloy 6](Reference/Formal_Software_Design_with_Alloy_6/#property-specification)

## Example 1: `sig S{r: A -> one B}`

### standard constraints
```
sig A, B {} 
sig S { 
  r: A -> one B 
  // synonymous with:
  // r: A set -> one B 
}

assert standard_constraints{
  all s: S, a: A | one a.(s.r)

  // synonymous with:
  all s: S, a: A | { one b: B | s->a->b in r }

  // implications:  
  ( all s: S, a: A | one a.(s.r) ) => (all s: S | {no a: A | no a.(s.r)}  )
}

check standard_constraints
```

### potential instances

![potential instances](/assets/images/key_ideas/multiplicities_on_relations_example1_potential_instances.png)

* A

```
sig A, B {} 
sig S { r: A -> one B }

pred potential_instances_A{
  all a: A | #(a.(S.r)) = 1
  some disj s1, s2: S, a: A | #(a.(s1.r)) = 1 and #(a.(s2.r)) = 1
}

run potential_instances_A for exactly 2 A, exactly 2 B, exactly 2 S
```

* B

```
sig A, B {} 
sig S { r: A -> one B }

pred potential_instances_B{
  some s: S, b: B | #(s.r.b) > 1
}

run potential_instances_B for 1 but exactly 2 A 
```

* C

:no_entry: No instance found

```
sig A, B {} 
sig S { r: A -> one B }

pred potential_instances_C{
  some s: S, a: A | #(a.(s.r)) = 0
}

run potential_instances_C for 1 but exactly 2 A
```

* D

:no_entry: No instance found

```
sig A, B {} 
sig S { r: A -> one B }

pred potential_instances_D {
  some s: S, a:  A | #(a.(s.r)) > 1
  // synonymous with: 
  some s: S, a: A | {
    some disj b1, b2:  B | { 
      (s->a->b1 in r) and (s->a->b2 in r) 
    }
  }
}

run potential_instances_D for 1 but exactly 2 B
```

* E

```
sig A, B {} 
sig S { r: A -> one B }

pred potential_instances_E {
  some s: S, a: A, b: B | #( a.(s.r) & b) = 0
}

run potential_instances_E for 1 but exactly 2 B
```

* F

```
sig A, B {} 
sig S { r: A -> one B }

pred potential_instances_F {
  some disj a1, a2: A, b: B | (some r.b.a1) and (some r.b.a2)
}

run potential_instances_F for exactly 2 A, exactly 2 B, exactly 2 S
```

* G

:no_entry: No instance found

```
sig A, B {} 
sig S { r: A -> one B }

pred potential_instances_G {
  some s: S, a: A | no a.(s.r)
}

run potential_instances_G for 1
```

* H

```
sig A, B {} 
sig S { r: A -> one B }

pred potential_instances_H {
  some s: S, b: B | no s.r.b
}

run potential_instances_H for 1
```

## Example 2: `sig S{r: A lone -> B}`

### standard constraints

```
sig A, B {} 
sig S { 
  r: A lone -> B 
 // synonymous with: 
 // r: A lone -> set B
}

assert standard_constraints{
  all s: S, b: B | lone (s.r.b)

  // synonymous with:
  all s: S, b: B | { lone a: A |   s->a->b in r }

  // implications:  
  ( all s: S, b: B | lone (s.r.b) ) => (all s: S, b: B |  #(s.r.b) <= 1  )
}
```

### potential instances

![potential instances](/assets/images/key_ideas/multiplicities_on_relations_example2_potential_instances.png)

* A

```
sig A, B {} 
sig S { r: A lone -> B }

pred potential_instances_A{
  all a: A | #(a.(S.r)) = 1
  some disj s1, s2: S, a: A | #(a.(s1.r)) = 1 and #(a.(s2.r)) = 1
}

run potential_instances_A for exactly 2 A, exactly 2 B, exactly 2 S
```

* B

:no_entry: No instance found

```
sig A, B {} 
sig S { r: A lone -> B }

pred potential_instances_B{
  some s: S, b: B | #(s.r.b) > 1
}

run potential_instances_B for 1 but exactly 2 A 
```

* C

```
sig A, B {} 
sig S { r: A lone -> B }

pred potential_instances_C{
  some s: S, a: A | #(a.(s.r)) = 0
}

run potential_instances_C for 1 but exactly 2 A
```

* D

```
sig A, B {} 
sig S { r: A lone -> B }

pred potential_instances_D {
  some s: S, a:  A | #(a.(s.r)) > 1
  // synonymous with: 
  some s: S, a: A | {
    some disj b1, b2:  B | { 
      (s->a->b1 in r) and (s->a->b2 in r) 
    }
  }
}

run potential_instances_D for 1 but exactly 2 B
```

* E

```
sig A, B {} 
sig S { r: A lone -> B }

pred potential_instances_E {
  some s: S, a: A, b: B | #( a.(s.r) & b) = 0
}

run potential_instances_E for 1 but exactly 2 B
```

* F

```
sig A, B {} 
sig S { r: A lone -> B }

pred potential_instances_F {
  some disj a1, a2: A, b: B | (some r.b.a1) and (some r.b.a2)
}

run potential_instances_F for exactly 2 A, exactly 2 B, exactly 2 S
```

* G

```
sig A, B {} 
sig S { r: A lone -> B }

pred potential_instances_G {
  some s: S, a: A | no a.(s.r)
}

run potential_instances_G for 1
```

* H

```
sig A, B {} 
sig S { r: A lone -> B }

pred potential_instances_H {
  some s: S, b: B | no s.r.b
}

run potential_instances_H for 1
```
