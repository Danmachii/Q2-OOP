# Q051 — Your answer

## (d) HashMap order vs Python dict order

TODO(Q051): explain why printing `map.keySet()` from a `HashMap` may come out in a
different order on another machine or Java version, and what the Python `dict`
guarantees instead (and whether that guarantee is alphabetical).

`HashMap` does not promise an iteration order. Its key iteration follows its internal
hash-table layout, which can vary with implementation details, capacity, and runtime
conditions, so code must not treat one observed order as stable. Use `TreeMap` for
sorted keys or `LinkedHashMap` for insertion order. Python's built-in `dict` guarantees
insertion order (as a language guarantee since Python 3.7); that is the order keys were
first inserted, not alphabetical order.