# timedoor-materio-frontend

Claude Code skills for building admin frontends on the [Materio](https://themeselection.com/item/materio-vuetify-vuejs-admin-template/) Nuxt + Vuetify template, following Timedoor's established production conventions.

## Overview

This repository contains the **`materio-nuxt-admin`** skill, which guides Claude Code when creating admin pages, CRUD workflows, forms, data tables, dashboards, dialogs, and permission-controlled UI on Materio-based Nuxt projects. It encodes the repository's conventions for:

- Nuxt file-based routing and workspace page structure
- Reusable component reuse (component catalog)
- Repository API modules, loading/error states, and data patterns
- Pinia auth, permission checks, and Materio theming

### Repository structure

```
skills/
└── materio-nuxt-admin/
    ├── SKILL.md                     # Skill entrypoint and workflow
    ├── references/
    │   ├── conventions.md           # Naming, casing, folder placement
    │   ├── component-catalog.md     # Reusable components
    │   └── data-patterns.md         # API, loading, error, auth patterns
    └── examples/
        └── crud-page/               # Adaptable CRUD checklist
```

## Installation

### Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) CLI installed

There are 2 ways you can install this skill: 

### Install the skill

Clone the repository and copy (or symlink) the skill into your project's skills directory:

```bash
# Clone
git clone <repository-url>
cd timedoor-materio-frontend

# Install into a target project (project-level)
cp -r skills/materio-nuxt-admin /path/to/your-project/.claude/skills/

# Or install globally (user-level)
cp -r skills/materio-nuxt-admin ~/.claude/skills/
```

Using a symlink instead of copying keeps the skill updated with `git pull`:

```bash
ln -s /path/to/timedoor-materio-frontend/skills/materio-nuxt-admin \
      /path/to/your-project/.claude/skills/materio-nuxt-admin
```

### Install as a Claude Code plugin

The repository includes a Claude Code plugin and marketplace manifest. Install it from the Claude Code interactive prompt:

```text
/plugin marketplace add backend-timedoor/timedoor-materio-frontend
/plugin install timedoor-materio-nuxt
```

```text
/plugin
```

For local development, load the plugin without installing it:

```bash
claude --plugin-dir /path/to/timedoor-materio-frontend
```

## Usage

Once installed, the skill triggers automatically when you ask Claude Code to build Materio-based admin UI, e.g.:

> "Create a CRUD page for managing products with a data table and form dialog."

To invoke it explicitly, reference the skill in your prompt:

> "Use the materio-nuxt-admin skill to add a users list page under the admin workspace."

## License

Distributed under the [MIT License](LICENSE).
