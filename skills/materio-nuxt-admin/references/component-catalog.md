# Component catalog

Treat this catalog as evidence, not a universal component library. Components below are project-specific examples or stock Materio examples. Before using one, verify that it exists in the target project, has the same contract, and is appropriate for the target domain. If absent or mismatched, use the target project's equivalent or create the smallest local component.

## Stock Materio examples

Use stock components only when present in the target template and when their definition matches the intended contract. Typical stock examples include `ConfirmDialog`, `DialogCloseBtn`, `AppDateTimePicker`, `TablePagination`, and `VDataTableServer`.

The TypeScript template uses `ConfirmDialog` with `v-model:is-dialog-visible` and confirmation/cancel messages. Its presence in an ingest does not prove that every derived project uses it.
