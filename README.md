# collage-poster

A curated skill that generates **contemporary editorial photo-collage posters** — greyscale photographic fragments with up to two flat spot colours on near-white paper, torn-and-taped edges, a faint modular grid, register marks, and mono annotations. Pick a spot palette, composition, and ratio; it composes an original poster prompt for any subject.

A **single-style, parametric generator**: the style is fixed, while the subject, palette, composition, elements, and ratio vary — so the look reproduces reliably across briefs.

## What it makes

- Greyscale photographic collage — torn fragments, taped strips, overlapping layers, photocopy grain.
- **At most two flat spot colours** as shapes (circles, bands) behind the fragments — never tinting the photos.
- Faint modular grid, small "x" register marks, thin outline rectangles, a large page-style number.
- Bold condensed grotesk headline + small monospaced annotations (dates, index, a rotated edge label).

It produces a final image-generation prompt (and the image itself when an image tool is available). It does **not** clone any specific existing poster.

## Install

Place the folder where your agent's skills live:

```
~/.claude/skills/collage-poster/
├── SKILL.md
└── design-system/system.json
```

Then just ask for a collage poster (e.g. "做一張拼貼海報，主題是…", "collage poster of…"), or invoke `/collage-poster`.

## Design system

All parameters live in [`design-system/system.json`](design-system/system.json) — the source of truth.

| Dimension | What's in it |
|---|---|
| **Substrates** (3) | Bright White · Warm Ivory · Newsprint Grey |
| **Spot palettes** (6) | *house-warm*: cobalt+terracotta, aubergine+gold, terracotta-mono · *collage-bright*: mustard+brick, cobalt+coral, mustard+cobalt |
| **Elements** (10) | torn photo fragment, taped strip, diagonal slab, flat spot circle, flat spot band, faint grid, register marks, outline rectangle, page number, rotated edge text |
| **Compositions** (3) | central stack · diagonal cross · scattered field |
| **Ratios** (8) | 3:4, 2:3, 4:5, 1:1, 9:16, 16:9, 1.91:1, and a Substack cover (~1.4:1, 1456×1048) |

The greyscale photographic base is a **constant**; colour lives only in the flat spot shapes.

## How it works

1. **Inputs** — subject, headline/labels, intent/ratio.
2. **Steering** — before composing, the skill surfaces the meaningful choices (spot palette, composition, substrate, **ratio**) as a picker with a recommended default, so you steer instead of getting a black box.
3. **Assembly** — resolves the palette, composition ratios, and element mix from `system.json`; keeps 35–50% breathing paper and one orientation event.
4. **Prompt compiler** — five compact paragraphs describing only visible outcomes.
5. **Self-check** — a one-line gate (greyscale photos, ≤2 spots, breathing white, generic annotations, verbatim headline).

## Originality & annotations

- Recombines into a new composition every time; never reproduces a specific poster's layout, lettering, or marks.
- All annotations (dates, index, edge labels, page numbers) are **generic** editorial marks — never a real brand, handle, URL, or a fact invented as if true.

## Related skills

- **poster-lab** — multi-style house generator (pick a whole style).
- **poster-echo** — reference-driven: extract a reference image's system and apply it to your own subject.

## License

Released under the [MIT License](LICENSE) — use, modify, and share freely, keeping the copyright notice.
