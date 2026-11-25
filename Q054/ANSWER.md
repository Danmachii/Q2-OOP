# Q054 — Your answer

## (a) The eight lines

TODO(Q054): for each of the eight lines, say whether it compiles and why
(totalKg(shirts); totalKg(anything); addSpareTowels(basket, 2); addSpareTowels(bathTowels, 1);
transfer(bathTowels, towels); transfer(towels, shirts); List<Garment> g = shirts;
view.add(new Shirt("x"))).

1. `totalKg(shirts)` — **compiles**: `Shirt` extends `Garment`, and the `extends` wildcard accepts a list of a subtype for reading.
2. `totalKg(anything)` — **does not compile**: `Object` is not a subtype of `Garment`.
3. `addSpareTowels(basket, 2)` — **compiles**: `List<Garment>` can consume `Towel` values.
4. `addSpareTowels(bathTowels, 1)` — **does not compile**: a `List<BathTowel>` cannot accept an arbitrary `Towel`.
5. `transfer(bathTowels, towels)` — **compiles**: infer `T = Towel`; bath towels produce `Towel` values and `towels` consumes them.
6. `transfer(towels, shirts)` — **does not compile**: no safe `T` lets a `List<Towel>` source be copied into `List<Shirt>`.
7. `List<Garment> g = shirts` — **does not compile**: Java generic lists are invariant; `List<Shirt>` is not a subtype of `List<Garment>`.
8. `view.add(new Shirt("x"))` — **does not compile**: the captured element type behind `? extends Garment` is unknown, so adding a `Shirt` is unsafe.

## (c) The rule
TODO(Q054): state the PECS rule and apply it to `transfer`.

PECS means **Producer Extends, Consumer Super**. Use `? extends T` for a collection read from as a producer and `? super T` for a collection written to as a consumer. `transfer` reads `T` values from `src` and writes them to `dst`, so its source is `Collection<? extends T>` and destination is `Collection<? super T>`.

## (d) Python

TODO(Q054): which calls does mypy reject, and how do you express `? super Towel` in Python
(variance: covariant / contravariant / invariant)?

With the provided invariant `MutableSequence[Towel]` destination, mypy rejects passing a `List[Garment]` or `List[object]` directly. The `Sink[T_contra]` protocol in the template expresses a contravariant consumer: `Sink[Towel]` can be implemented by a sink that accepts `Garment` or `object`, which is the Python type-hint counterpart of `? super Towel`. `Sequence[Garment]` is covariant for read-only input, so `Sequence[Shirt]` is accepted, while `Sequence[object]` is not accepted where garments are required. Invariant mutable lists also reject assigning `List[Shirt]` where `List[Garment]` is expected. A `List[Shirt]` destination for towels is rejected by the generic `transfer` typing. Python type hints are checked by tools such as mypy; ordinary Python execution does not enforce these annotations.