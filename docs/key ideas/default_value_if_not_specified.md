---
hide:
  - tags
tags:
  - relation
---
# default value if not specified

## Multiplicity

> Each relation has a multiplicity, which represents how many atoms it can include. If you do not include a multiplicity, it’s assumed to be `one` for individual relations and `set` for Multirelations.

Reference source (1)
{ .annotate }

1. [Alloy Documentation](/Reference/Alloy_Documentation/#multirelations)

```
sig Key {}

sig Lock {
  key: Key
  // synonymous with: 
  // key: one Key 
}
```

```
sig A, B {}

sig S {
  r: A -> B
  // synonymous with: 
  // r: A set -> set B
}
```