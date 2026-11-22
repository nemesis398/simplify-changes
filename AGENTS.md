# Agent notes for simplify-changes

This repository is a Claude Code plugin with one skill, `skills/simplify-changes/SKILL.md`.

- The skill text is the product. Keep its rules intact: error handling is behavior and is never deleted inside a cleanup, and suspected bugs go under *Flagged, not fixed*.
- No em dash anywhere (CI enforces it). Use a comma, a colon, parentheses or two sentences.
- Descriptions and prose name no person and no path. Write "the user".
- Cross-references name skills as they are installed: the conscience skill is `conscience`.
- Evals in `evals/` run with `claude plugin eval . --runs 3`. Each case is self-contained; do not add a repository fixture.
