---
type: pr
target_repo: emilk/egui
base: main
head: xc4pr:fix/3647-dangling-labelled-by
commit: bca3ef2
draft: true
title: "Don't panic AccessKit on `labelled_by` an unknown widget"
---

* Closes <https://github.com/emilk/egui/issues/3647>
* [ ] I have followed the instructions in the PR template

`Response::labelled_by` with an `Id` that is not in the AccessKit tree (not a widget, or an invisible one) made `accesskit_consumer` panic. `flatten_labelled_by` now drops such targets (with a `log::debug!`), so the widget just ends up without that label.

I also moved the doc comment of `flatten_labelled_by` back onto it; it had ended up on `is_accesskit_visible`.

Test: `labelled_by_unknown_id_is_ignored` in `egui_kittest/tests/accessibility_check.rs` panics on `main` and passes with this change.
