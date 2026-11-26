# Q075 — Your answer

## (a) The trace

TODO(Q075): for each of the ten events, the rows shown, or "no update".

At event 0 (`0. attach`), all six orders are shown sorted by ready hour: `[A2 Budi WDI READY 11:00, A4 Dewi WF READY 12:00, A5 Rahmat WDI WASHING 13:00, A1 Sari WF WASHING 14:00, A6 Citra WF DRYING 15:00, A3 Ayu IR RECEIVED 16:00]` (update 1). Event 1 (`1. filter 'ra'`) narrows the list to `[A5 Rahmat WDI WASHING 13:00, A6 Citra WF DRYING 15:00]` (update 2), and event 2 (`2. sort by customer`) reorders them alphabetically to `[A6 Citra WF DRYING 15:00, A5 Rahmat WDI WASHING 13:00]` (update 3).

Event 3 (`3. add A7 Budi`) produces `(no update)` because `"Budi"` does not match the `"ra"` filter, whereas event 4 (`4. advance A5`) changes A5's status and updates the view to `[A6 Citra WF DRYING 15:00, A5 Rahmat WDI DRYING 13:00]` (update 4). Events 5 (`5. filter 'RA'`) and 6 (`6. only DRYING`) both produce `(no update)` because the filter is case-insensitive and both visible orders are already `DRYING`.

Event 7 (`7. advance A6`) moves A6 to `READY` so it drops out of the `DRYING` view, leaving `[A5 Rahmat WDI DRYING 13:00]` (update 5), while event 8 (`8. filter ''`) produces `(no update)` since A5 is still the only `DRYING` order in the book. Finally, event 9 (`9. only READY`) shows all `READY` orders sorted by customer name: `[A2 Budi WDI READY 11:00, A6 Citra WF READY 15:00, A4 Dewi WF READY 12:00]` (update 6), giving 6 view updates across 10 events.

## (c) Why compare

TODO(Q075): why compare the new rows with the old ones, and why is the view-model easy to
test?

Comparing `rows` with `shown` avoids redundant UI repaints and unnecessary listener cascades when a model change is hidden by the active filter (such as adding `A7 Budi` while filtering `"ra"`) or when a setting change leaves the visible output identical (such as changing `"ra"` to `"RA"`). The view-model is easy to test because it has zero dependency on Swing or Tkinter widgets—it communicates through a simple callback (`Consumer<List<String>>` in Java or a plain function in Python) and plain strings, allowing headless unit tests to assert the exact rendered rows and update counts directly.

## (d) Chapter 9 ideas

TODO(Q075): which collection and generics ideas of Chapter 9 does the design use?

The design uses core Chapter 9 collection and generics ideas: parameterized collection types (`List<Order>`, `List<String>`, `List<Runnable>`) for compile-time type safety, defensive unmodifiable snapshots via `List.copyOf(orders)` so callers cannot mutate internal model state, and composable `Comparator<Order>` chains (`Comparator.comparingInt`, `Comparator.comparing` with `String.CASE_INSENSITIVE_ORDER`, and `thenComparing` for tie-breaking). It also uses the generic functional interface `Consumer<List<String>>` to decouple the view callback from any concrete widget class.
