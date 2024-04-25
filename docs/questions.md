# Questions

* Does the content of `fun` only be allowed to contain a set comprehension?
```
fun named_contents : Dir -> Name -> Object {
  { d : Dir, n : Name, o : Object |
    some e : Entry | e in d.entries and e.name = n and e.object = o }
}
```

* What's the difference between these two statements?

`{s: S, a: A | { one b: B | one s->a->b}}`

`{s: S, a: A | { some b: B | one s->a->b}}`

Answer:

`one s->a->b` is always true

`{b: B | {all s: S, a: A| one s->a->b}}`