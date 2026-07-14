# One-time setup: live `/dev/` preview

This repo is set up so that:

- **`main`** is published at the site root — https://verify-agents-workshop.github.io/
- **`dev`** is published at **/dev/** — https://verify-agents-workshop.github.io/dev/ — an
  unlinked, hidden staging copy for previewing changes before they go live.

Making this work needs a GitHub Actions workflow. Workflow files can only be created
by a human with `workflow` scope (automation tokens are blocked from writing them), so
this is a **one-time manual step**. Once it's done, no further manual steps are needed.

## Step 1 — Create the workflow file

On GitHub: **Add file → Create new file**, name it exactly:

```
.github/workflows/pages.yml
```

Paste in the following, commit to `main`:

```yaml
name: Deploy site (production + dev preview)

# Builds the published GitHub Pages site from two branches:
#   - `main` is served at the site root  (https://verify-agents-workshop.github.io/)
#   - `dev`  is served at /dev/          (https://verify-agents-workshop.github.io/dev/)
#
# The /dev/ path is an unlinked, hidden staging copy for previewing changes
# before they are merged into `main` and published to the root.

on:
  push:
    branches: [main, dev]
  workflow_dispatch:

# Least-privilege permissions required by the Pages deployment.
permissions:
  contents: read
  pages: write
  id-token: write

# Never run two deployments at once; let an in-flight deploy finish.
concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout production (main)
        uses: actions/checkout@v4
        with:
          ref: main
          path: main

      - name: Checkout preview (dev)
        uses: actions/checkout@v4
        with:
          ref: dev
          path: dev

      - name: Assemble site (main at root, dev under /dev)
        run: |
          mkdir -p _site
          rsync -a --exclude='.git' --exclude='.github' main/ _site/
          mkdir -p _site/dev
          rsync -a --exclude='.git' --exclude='.github' dev/ _site/dev/
          # Ensure Jekyll processing stays disabled for the assembled output.
          touch _site/.nojekyll

      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: _site

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

## Step 2 — Switch the Pages source to GitHub Actions

**Settings → Pages → Build and deployment → Source → GitHub Actions.**

(This replaces the current "Deploy from a branch" setting. The root of the site stays
`main`, so production does not visibly change.)

## Step 3 — Trigger the first build

Pushing the workflow file in Step 1 already triggers a run. You can watch it under the
repo's **Actions** tab. When it finishes:

- https://verify-agents-workshop.github.io/ → `main`
- https://verify-agents-workshop.github.io/dev/ → `dev`

After this, every push to `dev` refreshes the `/dev/` preview automatically, and every
push (or merge) to `main` refreshes production.
