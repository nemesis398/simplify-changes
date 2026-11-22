# simplify-changes

A [Claude Code](https://claude.com/claude-code) skill for the strict cleanup
pass: simplify the code a change just wrote, and prove that nothing it does
has changed.

Most cleanups are tidy-ups, and the built-in `/simplify` is the lighter default
for those. This skill is for the cleanups whose diff has to be safe to accept
without re-reading the whole feature: changes that touch error paths, fallbacks,
null checks or retry logic, or code that someone else depends on.

## The rules it holds

- **Behavior must not change.** A simplification that alters what the program
  does is a redesign, and it is not allowed in this pass.
- **Error handling is behavior.** A `try`, a narrower catch, a null check or a
  fallback is never removed because a caller looked dead. Such a handler is
  reported under *Flagged, not fixed* so that removing it is a deliberate
  change.
- **Flagged, not fixed.** A real bug found on the way is reported, not repaired
  inside the cleanup.
- **Four lenses.** Reuse, simplification, efficiency (only where it is obvious
  and free) and altitude.
- **Restraint.** Formatting, renames without a reason, untouched code and
  abstractions are left alone. A new abstraction is handed to the
  `conscience` skill rather than waved through.

Every pass ends with a report of four parts: *Simplified*, *Left alone*,
*Flagged, not fixed* and *Verification*.

## Install

In Claude Code, add the repository as a marketplace and install the plugin:

```text
/plugin marketplace add nemesis398/simplify-changes
/plugin install simplify-changes@simplify-changes
```

Without the plugin system, copy `skills/simplify-changes/` into
`~/.claude/skills/`. The skill is one Markdown file and needs nothing else.
It has no configuration file.

## Use

Ask in your own words, for example:

- "run the strict pass on my change"
- "simplify this without changing what it does"
- "careful cleanup of the error handling in this diff"

## Tests

`evals/` holds cases for `claude plugin eval`: an error path that must survive
the cleanup, and a bug that must be flagged rather than fixed. Each case gives
its code in the prompt, so it needs no repository. They run against a model,
on your own account:

```sh
claude plugin eval . --runs 3
```

CI checks the manifests, the Markdown, and that no em dash slipped in.

## License

[MIT](LICENSE)
