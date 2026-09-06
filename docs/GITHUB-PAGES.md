# Shared GitHub Pages theme

This repository also provides the shared dark Primer presentation used by GitHub Pages sites under `stef-k/*`.

## Use from a project

Keep the project's documentation in `docs/` and configure GitHub Pages to publish from `main` / `docs`.

Create `docs/_config.yml` with project-specific metadata and the shared remote theme:

```yaml
remote_theme: stef-k/.github@main

plugins:
  - jekyll-remote-theme

title: Project Name
description: Project description.
```

The shared theme supplies the default layout and dark styling. Project documentation remains in the project repository.

A project may override any shared theme file by adding the same path under its own `docs/` directory, for example `docs/_includes/head-custom.html`.

## Shared theme files

- `/_layouts/default.html` provides the common GitHub Pages layout.
- `/_includes/head-custom.html` is an intentionally minimal extension point that projects may override.
- `/assets/css/style.css` contains the shared dark-mode overrides.

The base presentation follows the official GitHub Pages Primer theme; the shared stylesheet applies the dark palette used by CogniRelay.
