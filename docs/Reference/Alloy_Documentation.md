# Alloy Documentation

Hillel Wayne

[Read the Docs](https://alloy.readthedocs.io/en/latest/index.html)

## [Multiplicity](https://alloy.readthedocs.io/en/latest/language/signatures.html#multiplicity)

> Each relation has a multiplicity, which represents how many atoms it can include. If you do not include a multiplicity, it’s assumed to be `one` for individual relations and `set` for Multirelations.

## [Multirelations](https://alloy.readthedocs.io/en/latest/language/signatures.html#multirelations)

### Reference table


```
r: A m -> n B
```

|m |n | Meaning |
|--|--|---|
|set|set|No restrictions|
|set|some|Each A used at least once|
|set|one|Each A is mapped to exactly one B (total function)|
|set|lone|Each A is mapped to at most one B (partial function)|
|some| set|Each B mapped to at least once|
|some|some|Every A mapped from and every B mapped to|
|some|one|Each A used exactly once, each B used at least once|
|some|lone|Each A used at most once, each B used at least once|
|one|set|Each B used exactly once, no other restrictions (one A can map to two B atoms)|
|one|some|Each B used exactly once, each A used at least once|
|one|one|Only satisfiable if #A = #B, bijection|
|one|lone|At most #A arrows, exactly #B arrows, each A used at most once|
|lone|set|Each B used at most once|
|lone|some|Each A used at least once and each B used at most once|
|lone|one|Each A used exactly once, each B used at most once|
|lone|lone|Each A used at most once, each B used at most once|


