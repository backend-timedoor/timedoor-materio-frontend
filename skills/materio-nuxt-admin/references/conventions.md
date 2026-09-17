# Conventions

Follow these conventions unless the user explicitly overrides them.

## Base template

The TypeScript Materio template uses Nuxt file-based routing, `script setup lang="ts"`, Vuetify components, Pinia, and configured aliases. `App.vue` initializes core/theme stores, wraps content in `VLocaleProvider` and `VApp`, then renders `NuxtLayout` and `NuxtPage`.

Configured aliases include `@core`, `@layouts`, `@images`, `@styles`, `@validators`, `@db`, and `@api-utils`. Core components and global components are auto-imported; use imports only when the component is outside configured auto-import directories.

## Folders

Use:

- `pages/` for route components.
- `components/global/` for cross-domain application components.
- `components/pages/{workspace}/{domain}/` for domain-specific components.
- `composables/` for application composables.
- `stores/` for Pinia stores.
- `repository/modules/{workspace}/{domain}/` for API modules.
- `plugins/` for Nuxt plugins.
- `layouts/` and `@layouts/` for layout implementation.
- `@core/` for Materio core code; do not modify stock core for a page feature.
- `assets/styles/` for application styling deltas.

## Naming

Use PascalCase for Vue component files and component tags: `DialogConfirm.vue`, `CustomerTabs.vue`, `UploadSingleImage.vue`. Use kebab-case for route folders/files: `balance-history.vue`, `material-request/`. Use lowercase workspace/domain folders: `branch/customer/`.

Use `useX` for composables (`useDebounce`, `useStatus`, `useFormatDate`, `useNumber`). Use camelCase API properties (`branchCustomer`, `masterCustomerGroup`). Use `isLoading` objects keyed by operation (`list`, `submit`, `detail`).

## Routes

Nuxt maps files directly to routes:

- `pages/branch/dashboard.vue` → `/branch/dashboard`
- `pages/branch/customer/index.vue` → `/branch/customer`
- `pages/branch/customer/[id]/index.vue` → `/branch/customer/:id`
- `pages/master/customer/[id]/edit.vue` → `/master/customer/:id/edit`


Keep workspace prefixes (`branch`,  `master`) in both page paths and repository module names. Landing redirects are workspace-specific.

## Layout and theme deltas

The application uses the Materio vertical navigation layout and bordered skin. Keep theme/layout changes in configuration and application style overrides, not copied stock demo files. 

Do not treat stock template structure as application behavior. 