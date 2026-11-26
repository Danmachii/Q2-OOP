# Q054 — Your answer

## (a) The eight lines

TODO(Q054): for each of the eight lines, say whether it compiles and why
(totalKg(shirts); totalKg(anything); addSpareTowels(basket, 2); addSpareTowels(bathTowels, 1);
transfer(bathTowels, towels); transfer(towels, shirts); List<Garment> g = shirts;
view.add(new Shirt("x"))).

1. `totalKg(shirts)` — **compiles**: `Shirt` extends `Garment`, and the `extends` wildcard accepts a list of a subtype for reading.
2. `totalKg(anything)` — **not compile**: `Object` is not a subtype of `Garment`.
3. `addSpareTowels(basket, 2)` — **compiles**: `List<Garment>` can consume `Towel` values.
4. `addSpareTowels(bathTowels, 1)` — **not compile**: a `List<BathTowel>` cannot accept an arbitrary `Towel`.
5. `transfer(bathTowels, towels)` — **compiles**: infer `T = Towel`; bath towels produce `Towel` values and `towels` consumes them.
6. `transfer(towels, shirts)` — **not compile**: no safe `T` lets a `List<Towel>` source be copied into a `List<Shirt>`.
7. `List<Garment> g = shirts` — **not compile**: Java generic lists are invariant; `List<Shirt>` is not a subtype of `List<Garment>`.
8. `view.add(new Shirt("x"))` — **not compile**: the captured element type behind `? extends Garment` is unknown, so adding a `Shirt` is unsafe.

## (c) The rule

TODO(Q054): state the PECS rule and apply it to `transfer`.

PECS means **Producer Extends, Consumer Super**. Use `? extends T` for a collection read from as a producer and `? super T` for a collection written to as a consumer. `transfer` reads `T` values from `src` and writes them to `dst`, so its source is `Collection<? extends T>` and destination is `Collection<? super T>`.

## (d) Python

TODO(Q054): which calls does mypy reject, and how do you express `? super Towel` in Python
(variance: covariant / contravariant / invariant)?

1. `total_kg(shirts)` — accepted: `Sequence` is covariant, so `Sequence[Shirt]` is usable as `Sequence[Garment]`.
2. `total_kg(anything)` with `anything: List[object]` — rejected: `Sequence[object]` is not a sequence of garments.
3. `add_spare_towels_anywhere(basket, 2)` — accepted: `Sink` is contravariant, so a sink of `Garment` can consume `Towel` values.
4. `add_spare_towels(bath_towels, 1)` — rejected by this Python signature because `MutableSequence` is invariant; a list of `BathTowel` cannot be treated as a mutable sequence of `Towel`.
5. `transfer(bath_towels, towels)` — accepted: the source is an `Iterable` producer and the destination is a `List` consumer, with `T` inferred as `Towel`.
6. `transfer(towels, shirts)` — rejected: a towel cannot safely be appended to a list of shirts.
7. `g: List[Garment] = shirts` — rejected because mutable `List` is invariant.
8. `view.add(Shirt("x"))` — rejected: the read-only `Sequence` interface has no `add` method (and adding through a covariant view would be unsafe).