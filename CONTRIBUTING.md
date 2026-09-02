# Contributing / Updating

Notes for maintaining this skill.

The design system is data-driven, so most changes are edits to [`design-system/system.json`](design-system/system.json) — the source of truth. Add a `spot_palettes` entry, an `elements` part, a `compositions` entry, or a headline voice there rather than in prose. `SKILL.md` holds the procedure (intake, Steering, assembly, compiler, self-check).

## Workflow — change → test → commit → push

```bash
cd ~/.claude/skills/collage-poster
# edit design-system/system.json and/or SKILL.md
git add -A
git commit -m "what changed and why"
git push
```

## Habits that keep it clean

- **One change per commit**, with a message that says what and why — the history stays legible and any change is easy to roll back (`git revert`).
- **Test before you push** — run the skill once and check the output before committing; don't push half-finished changes.
- **Validate the JSON** after editing `system.json` (a broken file breaks the skill):
  ```bash
  python3 -c "import json; json.load(open('design-system/system.json'))" && echo OK
  ```
- **Keep the docs in sync** — when you add a dimension (e.g. a 7th spot palette), update the design-system table in `README.md` and `style-system.svg` too.
- **Example images** go in `examples/` as web-sized PNGs (longest side ~1400px); full-res source files are gitignored.

## Don't edit the same repo from two places at once

Either edit on GitHub's web UI, or locally — not both between pushes. If you did edit on the web, run `git pull` before editing locally so history doesn't diverge.
