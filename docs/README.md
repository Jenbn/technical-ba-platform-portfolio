# Jekyll website folder

GitHub Pages source: **main /docs**.

## What the files do
- `_config.yml`: global site name and project URL (`baseurl`).
- `_layouts/default.html`: shared header, navigation, footer, and `{{ content }}` insertion point.
- `index.md`: homepage, using YAML front matter and Markdown.
- `projects/*.md`: navigable project landing pages.
- `assets/style.css`: reusable styling.

## Publish
1. Add this `docs/` folder to the existing repository, preserving the `docs/` path.
2. GitHub repository → Settings → Pages → Build and deployment → Deploy from a branch.
3. Branch `main`, folder `/docs`, then Save.
4. Visit https://jenbn.github.io/technical-ba-platform-portfolio/ after GitHub reports successful deployment.

The website starter links to the full original case studies in GitHub. We can migrate those Markdown documents into Jekyll pages in the next step.
