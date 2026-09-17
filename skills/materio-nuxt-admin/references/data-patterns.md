# Data patterns

Follow the application pattern supported by the target project. The stock template and production example use different API layers; do not mix them without evidence.

## Template API pattern

The TypeScript Materio template uses `useApi` with `createUrl` for URL/query construction and reactive table state:

```ts
const { data: ordersData, execute: fetchOrders } = await useApi<any>(
  createUrl('/apps/ecommerce/orders', {
    query: { q: searchQuery, page, itemsPerPage, sortBy, orderBy },
  }),
)
```

Use `VDataTableServer` with `items-length`, reactive `itemsPerPage`/`page`, and `@update:options` for sorting.

## Production repository API pattern

Use `$api` from `useNuxtApp()` and the registered repository namespace. Modules are instantiated in `plugins/api.ts` and provided as `$api`.

Use the module's observed argument buckets:

- `params`: resource/workspace IDs such as `office_id`, `customer_id`.
- `query`: filters, pagination, and search.
- `body`: create/update payload.

```ts
const response = await $api.branchCustomer.getList({
  query: {
    search: query.value.filter.search,
    status: query.value.filter.status,
    group_id: query.value.filter.group_id,
    limit: query.value.limit,
    page: query.value.page,
  },
  params: { office_id: user.main_office_id },
})
```

Do not invent a repository method or endpoint. Inspect the matching module first. The server proxy separates `/api/sanctum/*` from `/api/*` backend routes.

## List state and loading

Keep list state local:

```ts
const customers = ref([])
const meta = ref({ total: 0, per_page: 0, current_page: 0 })
const query = ref({
  filter: { search: null, status: null, group_id: null },
  limit: 10,
  page: 1,
})
const isLoading = ref({ list: false })
```

Set the operation flag before the request and reset it in `finally`. Assign `response.data` and `response.meta` only when a response exists. Pass the flag to `VDataTable` via `:loading`.

Fetch independent initial data in parallel:

```ts
await Promise.all([fetchData(), fetchGroups()])
```

For reactive filters, reset `page` when filters change and debounce the list request .

## Forms and mutations

Use a local submit loading flag. Validate through the existing form component/ref, call the appropriate repository method with `body`, show the existing toast, close on success, emit/refetch parent data, and always reset loading in `finally`.

Observed create dialog pattern:

```ts
const formData = await refCustomerForm.value.setFormData()
if (formData) {
  const response = await $api.masterCustomer.create({ body: formData })
  if (response) {
    toast('Berhasil menambah data konsumen')
    isDialogAddVisible.value = false
    emit('refetchData')
  }
}
```

Observed update pattern uses success and failure toast plus `console.error`, with `finally` resetting submit loading .

## Errors

Existing pages commonly catch and log errors locally. Preserve this behavior, but use the established toast/error presentation when the operation is user-facing. Do not expose response bodies or secrets. The global toast store exposes `visible`, `messages`, and `variant`.

## Auth and permissions

Pages use `definePageMeta({ middleware: ['auth'] })`. Unauthenticated users navigate to `/login`; public routes include `/login` and `/unauthorized`.
Auth hydration loads `/api/auth/me` and `/api/auth/permission`, then stores user and permission state in Pinia. Use existing auth-store and permission helpers. Do not hardcode a bypass or role-based permission check in a new page.

Route permission metadata maps route names to permission strings. Navigation uses CASL-style `can(item.action, item.subject)` and `navItemRolePermissionCheck` . Add route/action permissions through the established permission map, not an ad-hoc local check.

## State boundaries

Use Pinia for auth, configuration, and intentionally persisted cross-page state. Use local refs for page query, table rows, dialogs, forms, and loading. The template config store handles theme/layout; Rubberman persists selected state with Pinia persisted-state.
