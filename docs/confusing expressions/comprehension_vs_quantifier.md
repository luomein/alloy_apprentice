---
hide:
  - tags
tags:
  - comprehension
  - quantifier
---
# comprehension vs. quantifier

## Comparison

|             | comprehension  |  quantifier                          |
| ----------- | -----------------|------------------- |
| Expression       | `{ a: A | #(a.b) > 0 }`  | `( all a: A | #(a.b) > 0 )` |
| Output      | Set| Boolean |

## Combination

Example:

* [Formal Software Design with Alloy 6](https://haslab.github.io/formal-software-design/modelling-tips/index.html?highlight=comprehension)
```
fun named_contents : Dir -> Name -> Object {
  { d : Dir, n : Name, o : Object |
    some e : Entry | e in d.entries and e.name = n and e.object = o }
}
```
Or put it more clearly,
```
fun named_contents : Dir -> Name -> Object {
  { d : Dir, n : Name, o : Object |
    ( some e : Entry | e in d.entries and e.name = n and e.object = o )
  }
}
```