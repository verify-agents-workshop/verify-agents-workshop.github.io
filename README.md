# Who Verifies the Agents? Toward Reliable Agent Development

Website for the **NeurIPS 2026 Workshop** on tackling verification as a first-class
research problem for reliable agent development.

🔗 Live site: https://verify-agents-workshop.github.io/
📄 OpenReview: https://openreview.net/group?id=NeurIPS.cc/2026/Workshop/Verify-Agents
🐦 X: [@veri_agents](https://x.com/veri_agents)

## How the site deploys

GitHub Pages builds via the Actions workflow in `.github/workflows/pages.yml`:

- **`main`** publishes to the site root: https://verify-agents-workshop.github.io/
- **`dev`** publishes to a hidden staging path: https://verify-agents-workshop.github.io/dev/

Changes are developed on `dev`, previewed at `/dev/`, and merged into `main` to go
public. Pushes to `main` trigger a deploy automatically; after pushing to `dev` only,
manually dispatch the "Deploy site" workflow (the workflow file lives on `main`, so
`dev` pushes don't self-trigger). The `variants/` folder is excluded from the
production root and only ever renders under `/dev/variants/`.

## Structure

| Path             | Purpose                                             |
| ---------------- | --------------------------------------------------- |
| `index.html`     | Single-page workshop site                           |
| `style.css`      | Styles (cache-busted via `?v=N` query in the link)  |
| `assets/`        | Speaker/organizer photos, favicons, social card     |
| `variants/`      | Design mockups, staged only at `/dev/variants/`     |
| `.nojekyll`      | Serve assets without Jekyll                         |

To preview locally: `python3 -m http.server 8000` and open http://localhost:8000.

## Contact

verify-agents-workshop@googlegroups.com
