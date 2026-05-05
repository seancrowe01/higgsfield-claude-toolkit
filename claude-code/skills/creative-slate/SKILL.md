---
name: creative-slate
description: Weekly Sunday ideation routine. Reads past generation performance, ideates 30-50 new ad variations across products, writes them to the project Google Sheet ready for Monday batch generation. Use on Sunday or when the user asks for the weekly creative slate.
---

# Creative Slate

Weekly creative ideation, automated.

## When to invoke

- Sunday evenings (manual or scheduled via Claude routines)
- User says "build the creative slate", "weekly ideation", "what should we test next week"

## What this skill does

1. Pulls the project's Google Sheet generation log (all past prompts + their performance)
2. Reads the project `CLAUDE.md` for brand defaults and product list
3. Reads `briefs/advertising-masterclass.md` if present (for best-practice ideation)
4. Generates 30-50 fresh ad variations spanning multiple angles, hooks, formats
5. Writes them to the sheet's `creative-slate` tab with status `Ideated`, ready for Monday batch run

## Inputs the skill needs

- `GOOGLE_SHEET_ID` — set in project `.env` or passed at invoke time
- Product list — read from `CLAUDE.md` or `briefs/products.md`
- Past performance — pulled from sheet's `generations` tab

## Output structure

Each row in the sheet has:

| Column | Example |
|---|---|
| `id` | `slate-2026-w19-001` |
| `priority` | `high` / `med` / `low` |
| `product` | `90-day boxing program` |
| `format` | `static` / `carousel` / `video` |
| `model` | `nano_banana_2` |
| `angle` | `time-pressed-pro` |
| `headline` | `30 MINS. NO CHITCHAT. JUST TRAINING.` |
| `subtext` | `Built around your schedule. Built around results.` |
| `prompt` | (full Higgsfield prompt) |
| `status` | `Ideated` |
| `job_id` | (filled in after generation) |
| `result_url` | (filled in after generation) |

## Ideation rules

1. **Mix angles** — never more than 5 ideas on the same angle. Cover at least 6 distinct angles per slate.
2. **Mix formats** — 60% static, 25% carousel, 15% video.
3. **Pull from winners** — if past performance data is available, prioritise variations of the top-performing concepts (different hook, same visual format).
4. **Match the brand voice** — read `CLAUDE.md` for voice rules. If voice rules say "no rule-of-three", don't write rule-of-three headlines.
5. **Respect compliance** — strip medical claims, income claims, before/after promises if the brand has flagged them.

## Common angles to draw from

- Time-pressed (busy professional)
- Result / transformation
- Local / community pride
- Anti-mainstream (not a chain, not a globo-gym, not a typical X)
- Member / customer proof
- Behind-the-scenes
- Common objection + reframe
- Specific number / stat
- Question hook
- Pattern interrupt visual

## Companion skill

Pairs with [`ad-batch-generator`](../ad-batch-generator/SKILL.md) — Monday morning routine that reads the slate, generates the high-priority rows, marks them complete.

## Suggested cadence

- **Sunday 7pm** — run `creative-slate` (this skill)
- **Monday 8am** — run `ad-batch-generator` (high-priority rows only, ~15-30 of them)
- **Friday afternoon** — review, mark winners in sheet, those become the inputs for next week's slate
