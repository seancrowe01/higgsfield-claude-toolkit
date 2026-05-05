# Routines — Scheduled Generation

Routines are scheduled prompts that fire on a cadence. Claude runs the prompt automatically, no human in the loop.

This directory holds the recommended setup for a weekly content engine.

## The weekly engine

```
Sunday 7pm  → /creative-slate          (ideate 30-50 new ads)
Monday 8am  → /ad-batch-generator       (generate the high-priority ideas)
Friday 4pm  → /performance-review       (read live data, mark winners)
```

## How to set up routines in Claude Code

In Claude Code, type:

```
/loop schedule "/creative-slate" weekly sun 19:00
/loop schedule "/ad-batch-generator" weekly mon 08:00
/loop schedule "/performance-review" weekly fri 16:00
```

(Exact syntax varies — see `/help loop` in your Claude Code version.)

## What each routine does

### Sunday 7pm — Creative Slate

Invokes the `creative-slate` skill. Outputs ~30-50 new ad ideas to the project Google Sheet, status `Ideated`.

You wake up Monday with a queue ready to go.

### Monday 8am — Ad Batch Generator

Invokes the `ad-batch-generator` skill. Pulls top 30 high-priority `Ideated` rows, generates them, marks each `Generated`, writes the result URL back.

You start your work day with 30 fresh ad creatives ready to review.

### Friday 4pm — Performance Review (build this yourself)

Pulls real performance data from your ad platform (Meta Ads API, TikTok, etc.), matches it back to the `result_url` in your sheet, marks winners and losers. Becomes the input for next Sunday's slate.

This isn't included as a pre-built skill because the data source is platform-specific. Use the [`/meta-report`](https://github.com/seancrowe01/agency-command-centre) skill from Agency Command Centre as a reference if you're on Meta.

## Scaling up

Once you trust the outputs:
- Run the slate twice a week (Sun + Wed)
- Run the batch generator three times a week (Mon, Wed, Fri)
- Add a `/post-content` routine that auto-publishes the best result URLs to your social channels

That's a fully autonomous content engine.

## Safety rails

- **Set a credit budget.** Don't let routines burn your entire monthly Higgsfield credits in one bad run. Configure `max_credits_per_run` in the batch generator skill.
- **Always review before posting.** Routines should generate, not publish. Keep a human in the loop on the post step.
- **Watch for prompt drift.** Every month, manually review what the slate is producing. AI ideation can spiral into the same 5 angles if not corrected.
