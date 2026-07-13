# Who Verifies the Agents? Toward Reliable Agent Development

Website for the **NeurIPS 2026 Workshop** on formalizing verification as a core
discipline in agent development.

🔗 Live site: https://verify-agents-workshop.github.io/

## About

Recent advances in autonomous agents have demonstrated potential for complex
reasoning and open-ended tasks. However, current agent development is often
fragmented and dependent on ad-hoc methods, leading to reliability challenges
where performance plateaus or regresses during iteration. This workshop seeks to
formalize **verification** as a core discipline in agent development, organized
around three pillars:

1. **Robust verifiers** that resist reward hacking
2. **Environment-grounded simulation** as the ground truth for evaluation
3. **Heterogeneous signals** — latency, cost, and calibration — in the verification loop

## Development

This is a static site served by GitHub Pages from the repository root. To preview
locally, open `index.html` in a browser or run a simple static server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Structure

| File         | Purpose                          |
| ------------ | -------------------------------- |
| `index.html` | Single-page workshop site        |
| `style.css`  | Styles                           |
| `.nojekyll`  | Serve assets without Jekyll      |

## Editing content

Sections marked _TBA_ / _Tentative_ (dates, speakers, organizers, submission
details, contact email) are placeholders to be filled in as the workshop program
is finalized.
