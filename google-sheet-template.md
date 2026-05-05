# Google Sheet Template

The single source of truth for every generation. Used by `creative-slate` and `ad-batch-generator`.

Make a copy: [Higgsfield × Claude — Generation Tracker](#) *(template link to add once Sheet is published)*

## Tabs

### Tab 1 — `generations`

Every Higgsfield call you've ever made.

| Column | Type | Example |
|---|---|---|
| `id` | string | `gen-2026-05-06-014` |
| `timestamp` | datetime | `2026-05-06 09:14:22` |
| `product` | string | `90-day boxing program` |
| `format` | enum | `static` / `carousel` / `video` |
| `model` | string | `nano_banana_2` |
| `mode` | string | `hyper_motion` (Marketing Studio only) |
| `aspect_ratio` | string | `9:16` |
| `prompt` | text | (full prompt) |
| `reference_image` | string | `assets/hooked-gloves.jpg` (optional) |
| `job_id` | string | Higgsfield job ID |
| `status` | enum | `Pending` / `Generated` / `Failed` / `In Review` / `Approved` / `Rejected` |
| `result_url` | URL | from Higgsfield |
| `credits_used` | number | 2 |
| `notes` | text | failure reason or human note |

### Tab 2 — `creative-slate`

Ideated ads waiting to be generated. Drains into `generations` once the batch generator runs.

| Column | Type | Example |
|---|---|---|
| `id` | string | `slate-2026-w19-001` |
| `created` | date | `2026-05-04` |
| `priority` | enum | `high` / `med` / `low` |
| `product` | string | `90-day boxing program` |
| `format` | enum | `static` / `carousel` / `video` |
| `angle` | string | `time-pressed-pro` |
| `headline` | string | `30 MINS. NO CHITCHAT. JUST TRAINING.` |
| `subtext` | string | `Built around your schedule.` |
| `model` | string | `nano_banana_2` |
| `prompt` | text | (full prompt) |
| `reference_image` | string | optional |
| `status` | enum | `Ideated` / `Generated` / `Skipped` |
| `linked_generation_id` | string | filled in once generated |

### Tab 3 — `performance` (optional, fed by your ad platform)

Real-world performance data, joined to `generations` by `result_url`.

| Column | Type | Example |
|---|---|---|
| `result_url` | URL | (matches `generations.result_url`) |
| `platform` | string | `meta` / `tiktok` |
| `date_range` | string | `2026-05-06 to 2026-05-13` |
| `spend` | number | £200 |
| `impressions` | number | 50000 |
| `clicks` | number | 800 |
| `ctr` | number | 1.6% |
| `cpc` | number | £0.25 |
| `conversions` | number | 12 |
| `cpa` | number | £16.67 |
| `verdict` | enum | `winner` / `loser` / `inconclusive` |

### Tab 4 — `by-product` (auto-rollup)

Pivot table aggregating `generations` and `performance` by product. Shows total spend, best CPA, top hook angle per product.

### Tab 5 — `by-angle` (auto-rollup)

Pivot showing which angles win across products. Feeds the ideation prompt for next week's slate.

## How the skills use this sheet

| Skill | Reads | Writes |
|---|---|---|
| `creative-slate` | `generations`, `performance`, `by-angle` | `creative-slate` (new rows) |
| `ad-batch-generator` | `creative-slate` (status=Ideated) | `creative-slate` (status update), `generations` (new rows) |
| `performance-review` (build yourself) | `generations`, ad platform API | `performance`, `creative-slate` (annotation) |

## Setup

1. Make a copy of the template (link above)
2. Set the sheet ID in your project `.env`:
   ```
   GENERATION_TRACKER_SHEET_ID=1AbCdEfGhIjKl...
   ```
3. The skills will read/write via the [GWS CLI](https://github.com/google-workspace/gws-cli) or the Google Sheets MCP.

## Why a sheet?

- You can edit it manually when needed
- Stakeholders can view it without running anything
- Pivots and filters give you instant visibility into what's working
- Cheaper than a real database for this scale

If you outgrow it (>10K generations/month), graduate to Airtable or Postgres.
