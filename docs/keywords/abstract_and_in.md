# `abstract` and `in`
* `in` creates a subset
* subsets are ***not*** mutually disjoint
```
sig A{}
sig A1, A2 in A{}

fact {
  #(A1 & A2) > 0
}

check {
  #(A1 & A2) > 0
  some a1 : A1 | a1 in A2
}
```
* All subsets of an abstract signature `A` ***do not*** form a partition of `A`
```
abstract sig A{}
sig A1, A2 in A{}

fact {
  #(A - A1 - A2) > 0
}

check {
  #(A - A1 - A2) > 0  
}

run {} 
```
* All subsets of a non-abstract signature `A` ***do not*** form a partition of `A`
```
sig A{}
sig A1, A2 in A{}

fact {
  #(A - A1 - A2) > 0
}

check {
  #(A - A1 - A2) > 0  
}

run {} 
```
