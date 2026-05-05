---
name: ad-batch-generator
description: Monday-morning batch generation routine. Reads the project Google Sheet, pulls all rows with status "Ideated" up to a configurable limit, generates each via Higgsfield, marks them complete with job_id and result URL. Use on Monday morning or when the user asks to "run the batch", "generate the slate", or "fire the queue".
---

# Ad Batch Generator

Reads the slate, generates everything, marks each row done. The other half of the weekly content engine.

## When to invoke

- Monday mornings (manual or scheduled)
- User says "run the batch", "fire the queue", "generate the slate", "process the ideated rows"

## What this skill does

1. Reads the project Google Sheet's `creative-slate` tab
2. Filters to rows where `status = Ideated`
3. Limits to the top N rows (default 30, sorted by `priority` then row number)
4. For each row:
   - Calls the right Higgsfield model based on `format` and `model` columns
   - Waits for the job to finish
   - Captures the `job_id` and `result_url`
   - Updates the row's `status` to `Generated` and writes back the IDs
5. Reports a summary: X generated, Y failed, total credits used

## Defaults

| Setting | Value |
|---|---|
| Batch size | 30 rows |
| Parallelism | 4 (respect Higgsfield Plus parallel limit of 8 images / 6 videos) |
| Timeout per job | 10 minutes |
| Retry on failure | once |

## Failure handling

If a job fails (sensitive-content block, model error, credit exhaustion):
- Mark the row's `status` as `Failed`
- Append the error to a `notes` column
- Continue with the rest of the batch
- At the end, surface failures to the user with suggested fixes

## Hard rules

- **Never duplicate a row.** Skip rows already marked `Generated` or `In Review`.
- **Stop on credit exhaustion.** If Higgsfield returns `not_enough_credits`, halt the batch and tell the user. Don't keep retrying.
- **Always reference an asset image** when one is named in the row's `reference_image` column.
- **Respect rate limits.** If Higgsfield 429s, back off 30s and retry.

## Output

Sample summary:

```
Batch run 2026-05-06 08:14
- Total in queue: 30
- Generated: 27
- Failed: 2 (sensitive content)
- Skipped: 1 (duplicate)
- Credits used: 54
- Credits remaining: 946
- Sheet updated: ✓
- Result URLs: see column M
```

## Companion skill

Pairs with [`creative-slate`](../creative-slate/SKILL.md) — the Sunday ideation routine that fills the queue this skill drains.

## Scaling up

Once you trust the outputs:
- Increase `batch_size` from 30 to 50
- Run twice weekly (Monday + Friday)
- Pipe `result_url` straight to a posting tool (Potato, Zernio, Buffer)
