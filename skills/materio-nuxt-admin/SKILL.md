---
name: materio-nuxt-admin
description: Build Materio-based Nuxt admin pages following this repository's established production conventions. Use when creating a new admin page, CRUD workflow, form, data table, dashboard widget, dialog, workspace route, or permission-controlled UI, or when wiring API calls, loading/error states, auth checks, or theme customization. Covers file-based routing, workspace page structure, reusable component reuse, repository API modules, Pinia auth, and Materio theming.
---

# Materio Nuxt Admin

Build pages using the target project's established conventions, using the ingested Materio template only for stock implementation patterns. All rules here are mandatory unless the user explicitly overrides them.

## Workflow

1. Read `references/conventions.md` before choosing file locations, route names, or component names.
2. Read `references/component-catalog.md` before creating any component. Reuse an existing catalog component when it matches the requirement.
3. Read `references/data-patterns.md` before wiring API calls, loading state, error handling, auth, permissions, or workspace behavior.
4. Use `examples/crud-page/` as a framework-neutral CRUD checklist and adapt its API, component, route, and state details to the target project profile.
5. Cross-check stock-vs-custom guidance before extending or wrapping Materio components.
6. Preserve the target project's naming, casing, prefixes, and route hierarchy; never copy project-specific conventions from the example catalog blindly.
7. Keep loading state local to the page operation unless an existing shared pattern clearly applies.
8. Do not invent delete behavior, API methods, permission names, or component props without repository evidence.
9. If the repository contains conflicting patterns, stop and ask which convention is authoritative.

## Page implementation

- Use Nuxt file-based routing under the appropriate workspace folder in `pages/`.
- Keep domain-specific UI in the matching `components/pages/{workspace}/{domain}/` area.
- Keep shared UI in `components/global/`.
- Use the target project's verified data-access layer: `useApi`/`createUrl`, `$api` repository modules, or another existing abstraction. Do not mix patterns without evidence.
- Represent list, form, and submit loading states explicitly via the `isLoading` ref pattern.
- Pass list loading state to `VDataTable` via `:loading`.
- Preserve the target project's existing query, pagination, and response shapes; do not assume `filter`, `limit`, `page`, or `meta` names.
- Use the target project's existing auth middleware, permission system, and auth-store helpers; template CASL and project-specific checks are not interchangeable.
- Follow the vertical-nav layout and existing theme customization; only add deltas to stock Materio theming.

## Definition of done

- [ ] Page lives in the correct workspace folder and produces the intended file-based route.
- [ ] All UI components come from the component catalog, or new domain components are justified and placed in the correct folder.
- [ ] Data access uses the target project's verified API abstraction; no new competing fetch pattern was introduced.
- [ ] List loading state is explicit and wired to `VDataTable`; form/submit loading follows the `isLoading` ref pattern.
- [ ] Filters, pagination, and response handling match the target project; `examples/crud-page/` was used only as an adaptable checklist.
- [ ] Permission checks use the target project's existing authorization system; no hardcoded role or permission behavior was copied from an example project.
- [ ] Naming, casing, and folder placement match `references/conventions.md`.
- [ ] No invented API methods, permission names, or props  everything traceable to repository evidence or user instruction.
