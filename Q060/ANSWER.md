# Q060 — Your answer

## (a) The trace

TODO(Q060): give the label and `handled` after each of the nine steps.

Steps 0 (start) and 1 (type `4.2`) stay at `handled=0` with `(no quote yet)` since typing fires no event, then clicking Quote (step 2), ticking Express (step 3), and choosing WDI (step 4) raise `handled` to `1`, `2`, and `3` with labels `WF 4.5 kg: Rp31,500, ready in 48 h`, `WF 4.5 kg express: Rp47,250, ready in 12 h`, and `WDI 4.5 kg express: Rp67,500, ready in 18 h`. Typing `abc` (step 5) fires nothing (`handled=3`, label unchanged), pressing Enter (step 6), unticking Express (step 7), and choosing IR (step 8) increment `handled` to `4`, `5`, and `6` with `Invalid weight`, and finally typing `0.4` and clicking Quote (step 9) reaches `handled=7` with `IR 2.0 kg: Rp10,000, ready in 24 h`.

## (b) The stale label

TODO(Q060): why does step 5 leave a label that contradicts the field, and what event would
you listen to in order to fix it?

Step 5 leaves a stale label because typing `"abc"` into the weight field does not fire an `ActionEvent` (Swing) or `<Return>` event (Tkinter), so `refresh` never runs and the previous quote remains displayed. To fix this, listen to text-change events using a `DocumentListener` (`DocumentEvent`) on `kg.getDocument()` in Swing, or `kg.trace_add("write", ...)` (or `<KeyRelease>`) in Tkinter so the label updates immediately as the text changes.
