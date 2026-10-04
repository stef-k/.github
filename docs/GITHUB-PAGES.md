# Shared GitHub Pages theme

This repository provides the shared dark Primer presentation used by GitHub Pages sites under `stef-k/*`.

## Use from a project

Keep the project's documentation in `docs/` and configure GitHub Pages to publish from the repository's documentation branch and `/docs` folder.

Create `docs/_config.yml` with project-specific metadata and the shared remote theme:

```yaml
remote_theme: stef-k/.github@main

plugins:
  - jekyll-remote-theme

title: Project Name
description: Project description.
url: https://stef-k.github.io
baseurl: /ProjectName
repository: stef-k/ProjectName

defaults:
  - scope:
      path: ""
    values:
      layout: documentation
```

The shared theme supplies the default layout and dark styling. Project documentation remains in the project repository.

A project may override any shared theme file by adding the same path under its own `docs/` directory, for example `docs/_includes/head-custom.html`.

## Optional documentation sidebar

Projects with several documentation pages can opt into the shared responsive sidebar by creating:

`docs/_data/navigation.yml`

Projects without this file keep the existing single-column layout.

Project documentation owns the navigation content; the shared theme owns rendering and responsive behavior.

### Navigation schema

Use top-level sections with ordered page items:

```yaml
sections:
  - title: Users
    items:
      - title: Getting started
        url: /user/
      - title: Timeline
        url: /user/timeline.html
      - title: Trips
        url: /user/trips.html

  - title: Development
    items:
      - title: Developer guide
        url: /development/
      - title: Architecture
        url: /development/architecture.html
```

Each section requires:

- `title`
- `items`

Each item requires:

- `title`
- `url`

One optional child level is supported:

```yaml
sections:
  - title: Development
    items:
      - title: API
        url: /development/api.html
        children:
          - title: Authentication
            url: /development/api.html#authentication
```

Keep navigation intentionally shallow. Prefer another page or section over deeply nested menu structures.

### URLs and repository base paths

Navigation URLs are relative to the documentation site root and are passed through Jekyll's `relative_url` filter.

For a project configured with:

```yaml
baseurl: /ProjectName
```

this navigation entry:

```yaml
url: /user/trips.html
```

renders beneath `/ProjectName/user/trips.html`.

Do not include the repository `baseurl` inside each navigation entry.

Anchors are allowed, for example:

```yaml
url: /development/api.html#authentication
```

The sidebar marks exact page links as the current page with `aria-current="page"`. Anchor-only destinations do not create additional current-page states.

## Sidebar behavior

### Desktop

When navigation data exists:

- the sidebar is displayed beside the article;
- it remains sticky while the article scrolls;
- an oversized sidebar scrolls within the viewport;
- the current page receives a visible and semantic active state;
- the article keeps an independent readable content column.

### Mobile

At narrow widths, the permanent sidebar is replaced by a native `<details>` control labelled **Documentation navigation**.

This keeps the navigation keyboard-accessible without a front-end framework or project-specific JavaScript.

## Shared theme files

- `/_layouts/default.html` provides the common GitHub Pages layout and optional sidebar shell.
- `/_includes/documentation-sidebar.html` renders project-owned navigation data.
- `/_includes/head-custom.html` is an intentionally minimal extension point that projects may override.
- `/assets/css/style.css` contains the shared dark-mode and responsive sidebar styles.

The base presentation follows the official GitHub Pages Primer theme; the shared stylesheet applies the shared dark palette.

## Adoption guidance

Adding the shared sidebar does not require changing documentation content.

A project can adopt it independently by:

1. ensuring it uses the shared `documentation` layout;
2. adding `docs/_data/navigation.yml`;
3. validating that every listed destination exists under its configured `baseurl`;
4. keeping the navigation hierarchy in sync as pages are added, moved, or removed.

Sites that do not provide navigation data continue to use the original one-column presentation.
