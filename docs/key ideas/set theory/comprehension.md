---
hide:
  - tags
tags:
  - comprehension
---
# comprehension
## Background
### [Set-builder notation](https://en.wikipedia.org/wiki/Set-builder_notation)

$\{ x \in E \mid Φ(x) \}$

This notation represents the set of all values of x that belong to some given set E for which the predicate $Φ(x)$ is true .

* The $\in$ symbol denotes set membership and $E$ is the domain.
* The formula $Φ(x)$ is said to be the rule or the predicate. 
* It is equivalent to $\{ x \mid x \in E \land Φ(x) \}$. It is sometimes written $\{ x \mid x \in E , Φ(x) \}$, using a comma instead of the symbol $\land$.

### [More complex set-builder notation](https://en.wikipedia.org/wiki/Set-builder_notation)

Instead of $\{ x \mid Φ(x) \}$, we may have $\{ f(x) \mid Φ(x) \}$.

Instead of $\{ x \mid x \in E , Φ(x) \}$, we may have $\{ f(x) \mid x \in E , Φ(x) \}$.

For example:

* $\{2n \mid n \in N\}$
* $\{p/q \mid p,q \in N , q \neq 0 \}$

### [List comprehension in programming language](https://en.wikipedia.org/wiki/List_comprehension)
* It is for creating a list based on existing lists.
* It follows the form of the mathematical set-builder notation (set comprehension).

## Alloy examples

* [Alloy Documentation](https://alloy.readthedocs.io/en/latest/language/sets-and-relations.html#set-comprehensions)

Set comprehensions are written as
```
{x: Set1 | expr[x]}
```
Set comprehensions can use multiple inputs.
```
{x: Set1, y: Set2, ... | expr[x,y]}
```
In this case this comprehension will return relations in `Set1 -> Set2`.

* [Formal Software Design with Alloy 6](https://haslab.github.io/formal-software-design/modelling-tips/index.html?highlight=comprehension)
```
fun named_contents : Dir -> Name -> Object {
  { d : Dir, n : Name, o : Object |
    some e : Entry | e in d.entries and e.name = n and e.object = o 
  }
}
```