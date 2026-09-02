---
name: collage-poster
description: Generate original contemporary editorial photo-collage posters — greyscale photographic fragments plus at most two flat spot colours, on near-white paper, with torn/taped edges, a faint modular grid, register marks, and mono edge annotations. A curated single-style generator (like mono-color, but for the cut-and-paste collage look), driven by design-system/system.json. Use when the user wants a collage poster, cut-out / cutout collage, zine cover, mixed-media key visual, "拼貼海報", "剪貼風", "zine 風格", or a poster in the torn-photo-plus-spot-colour editorial style — for any subject. Produces a final image-generation prompt (and the image when generation is available). For turning an arbitrary reference image into a poster, use poster-echo; for the multi-style house generator, use poster-lab.
---

# Collage Poster

One curated visual system: **contemporary editorial photo-collage**. Greyscale photographic fragments, at most two flat spot colours, torn-and-taped edges, a faint grid, register marks, and mono annotations — recombined onto any subject.

> pick the parts (spot palette + composition + elements) → assemble the collage → compile the prompt → self-check

The style is fixed; the subject, spot palette, composition and element mix vary. All parameters come from `design-system/system.json`, which is the source of truth — when its values differ from this prose, the JSON wins. Recombine into a new composition every time; never clone a specific existing poster.

## Inputs

Know these before composing; ask (single `AskUserQuestion`) only for what's missing.

1. **Subject** (header `主體`) — the recognizable subject the collage is about.
2. **Words** (header `文字`) — headline text (verbatim), and any small labels. Supporting annotations (dates, index, edge label, page number) may be generated as GENERIC editorial marks — never real brands, handles, or URLs.
3. **Intent / ratio** (header `用途`) — portfolio / social / zine / experiment; ratio follows the user, else 3:4.

## Steering the Recipe

After the inputs are known and the recipe is resolved to its defaults — but **before** writing the prompt — surface the meaningful forks as **one `AskUserQuestion` picker** so the user sees and steers the choices instead of getting a black box. Recommended option first, labelled `（推薦）`, pre-selected. Only include forks that branch; skip any with one sensible answer. Typical forks:

- **Spot palette** — which `spot_palettes` entry (house-warm set vs collage-bright set; or a specific pair).
- **Composition** — `central_stack` / `diagonal_cross` / `scattered_field`.
- **Substrate** — bright white / warm ivory / newsprint grey, when it matters.
- **Ratio** — always offer as a fork, with the presets: portrait (3:4 / 2:3), social (4:5 / 1:1 / 9:16), landscape (16:9 / 1.91:1), and **Substack cover (~1.4:1, 1456×1048)**. Recommend the intent's default (portfolio → 3:4; feed → 1:1 or 4:5; story/reel → 9:16; banner/slide → 16:9; Substack post → substack_cover). Adapt the composition to the chosen ratio per `ratios.note` — for landscape/Substack spread the collage horizontally and move the headline to a side; centre for square; stack vertically for 9:16.

If the user says "用推薦" / "just go", use the defaults and compile. Don't loop the picker.

## Assembly

Resolve from `system.json`:

- **Greyscale base is constant** — the photographs are always greyscale charcoal; colour lives only in flat spot shapes (`spot_rules`).
- **Spot palette** — at most two flat spot colours (circles, bands, blocks) behind or beside the greyscale fragments; never tint the photos.
- **Composition** — take the chosen entry's `subject_percent`, `empty_percent`, `anchor`, `title_relation`; keep 35-50% breathing paper.
- **Elements** — choose a mix from the `elements` kit within their `count` guidance: torn photo fragments (the subject), optional taped strips, one optional diagonal slab (the signature orientation event), flat spot circles/bands, a faint grid, a few register marks, optional outline rectangle, an optional large page number, optional rotated edge label. Don't overfill.
- **Typography** — bold condensed/wide grotesk uppercase display + small mono support (dates, index, one large page number, one rotated edge label); scale 5:1..8:1; one orientation event.
- **Annotations are generic** — dates, index, edge text and page numbers are editorial marks, never real brands/handles/URLs, never invented as fact.

## Prompt Compiler

Five compact paragraphs, visible outcomes only; never name artists, studios, or "in the style of".

1. **Canvas & system:** ratio, substrate hex, the greyscale-plus-two-spot palette with each hex role-assigned, the editorial-collage character, flat front-facing page.
2. **Composition:** the chosen composition's subject/empty balance and anchor, the element mix and where each sits, one focal event, one release zone of white, one diagonal/orientation disruption, 35-50% breathing paper.
3. **Subject & treatment:** the subject rendered as greyscale photographic collage — torn fragments, taped strips, overlapping layers, photocopy grain; flat spot shapes behind; white paper cutting between fragments as real negative shapes.
4. **Typography & words:** the display voice, the exact headline and any small labels, generic mono annotations (dates / index / rotated edge label / large page number), the scale jump.
5. **Material & avoids:** grain, torn/taped edges, faint grid, register marks — then a hard-negative list.

## Originality & Annotations

- Recombine into a new composition; never reproduce a specific existing poster's layout, lettering, or marks.
- All annotations are GENERIC — never a real brand, @handle, URL, or a fact invented as if true (no fake dates presented as real events).
- For portfolio publication, run the user's disclosure/verification gate at `200_Reference/templates/ai-disclosure.md`.

## Generation & Inspection

1. Generate when a tool is available; otherwise deliver prompt-only and say so.
2. Inspect full size + thumbnail. Regenerate once if: colour bled into the photos (they must stay greyscale), more than two spot colours appeared, the page is overfilled with no breathing white, there's no single focal event, the subject is unrecognizable, long text is garbled, or a real brand/URL leaked in.
3. If exact text renders wrong after one retry, deliver a text-light base and say to set type in a layout tool.

## Output Format

```markdown
**生成圖**（有生圖工具時）

![collage-poster](absolute-image-path)

**最終 Prompt**

​```text
[the compiled prompt]
​```

**本次配方**

- Spot palette: [id — hexes]
- Substrate: [name + hex]
- Composition: [id — subject/empty %, anchor]
- Elements: [the chosen mix]
- Type: [display voice + support, scale]
- Ratio: [ratio]
- Originality: [one line — the key structural choices]

[self-check line]
```

## Self-Check Gate

End every delivery with a one-line self-check; flag and fix anything that fails rather than reporting all-green by habit.

- Are the photographs greyscale, with colour only in at most two flat spot shapes?
- Is 35-50% of the page breathing white/paper — dense collage, calm margins?
- Is there one focal event and one orientation/diagonal event, not several competing angles?
- Are all annotations generic (no real brand / handle / URL / invented fact)?
- Is the subject preserved and any supplied headline verbatim?
- Traditional-Chinese conversation, no China-specific wording (this user is in Taiwan)?

## Extending

Edit `design-system/system.json`: add a `spot_palettes` entry (≤2 flat spots + hexes), an `elements` part (role + count), or a `compositions` entry (subject/empty % + anchor + title_relation). Keep entries shaped like their neighbours. Two spot sets ship: `house-warm` (from Sophie's ink library) and `collage-bright` (classic zine brights).
