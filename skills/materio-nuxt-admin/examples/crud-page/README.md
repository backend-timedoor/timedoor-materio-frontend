# CRUD page pattern

Use this as an adaptable checklist, not a copyable project implementation. First identify the target project's route, component, API, state, validation, and authorization conventions. The ingests provide two concrete profiles: the stock TypeScript Materio pattern and a repository-module production pattern.

## 1. Route

Create list, create, detail, and edit files according to the target project's existing Nuxt file-based route structure. Do not assume workspace names, page prefixes, or whether create/edit use pages or dialogs.

## 2. List state

Keep table state local unless the target project already centralizes it:

```ts
const rows = ref([])
const isLoading = ref(false)
const page = ref(1)
const itemsPerPage = ref(10)
const filters = ref({ search: '' })
```

Use the target project's actual response fields and loading shape. The template uses `searchQuery`, `itemsPerPage`, `page`, `sortBy`, and `orderBy`; the production example uses nested `query.filter`, `limit`, `page`, and `meta`.

## 3. Data access

Inspect the target project before implementing:

- Template profile: `useApi(createUrl(...))`, commonly paired with `VDataTableServer`.
- Repository profile: `useNuxtApp().$api.<module>.<method>({ params, query, body })`, commonly paired with local `isLoading` and `VDataTable`.

Use only the abstraction already used by the target project. Verify method names and payload shape in its repository/module or composable.

## 4. Loading and errors

Set loading before each request, disable relevant controls during mutations, and reset loading in `finally`. Preserve the target project's error surface: toast, snackbar, error state, or established logging. Never expose secrets or raw response bodies.

## 5. List and filters

Use the target project's existing table component and pagination contract. Common Materio building blocks are `VTextField`, `VSelect`, `VAutocomplete`, `VDataTable`, and `VDataTableServer`; their use does not imply identical query or response semantics.

Debounce search only when the target project already does so. Reset page on filter changes only when pagination is server-controlled.

## 6. Create/edit

Reuse a target-project dialog/form component if one exists. Otherwise follow the local form convention:

- validate at the form boundary;
- use the verified create/update API method;
- show the established success/error feedback;
- prevent duplicate submission;
- close or navigate only after confirmed success;
- refresh or invalidate the list through the target project's existing mechanism.

Do not infer that a list page supports delete. Confirm the mutation method and authorization first.

## 7. Authorization

Apply the target project's existing page middleware, route metadata, ability checks, or permission map. Template CASL metadata and project-specific permission maps are alternatives, not a combined recipe.

## 8. Definition-of-done adaptation

- Correct target-project route and folder.
- Existing target-project components reused where applicable.
- Verified target-project data layer used.
- Correct target-project table, pagination, response, loading, validation, and error contracts.
- Existing authorization path preserved.
- No project-specific component, API method, permission, naming convention, or delete flow copied without evidence.
