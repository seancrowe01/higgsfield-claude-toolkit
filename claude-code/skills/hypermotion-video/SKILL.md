---
name: hypermotion-video
description: Generate a Hypermotion-style premium product launch video via Higgsfield Marketing Studio. Fast cuts, dramatic zooms, polished feel. Use when the user asks for a launch video, a hype video, or a high-energy product reveal.
---

# Hypermotion Video

A reusable recipe for premium product launch videos. Reverse-engineered from the [Next Level YouTube walk-through](https://www.youtube.com/watch?v=xn6Z5PYyAIE) — the version that landed best for sleep-supplement ads.

## When to invoke

User says any of:
- "launch video"
- "hype video"
- "product reveal"
- "Hypermotion"
- "premium product video"

## What this skill does

1. Asks 4 quick questions to pin down the brief
2. Constructs a Marketing Studio prompt with the `hyper_motion` mode
3. Calls `higgsfield generate create marketing_studio_video` with the right defaults
4. Returns the result URL

## Questions to ask before generating

1. **Product** — what are we showing? (provide a reference image if possible)
2. **Aspect ratio** — `9:16` (default, vertical), `1:1`, or `16:9`?
3. **With or without a presenter** — product-only or include a UGC presenter?
4. **Mood word** — pick one: energetic / calm-luxury / cinematic / playful

## Hard rules

- **Always Marketing Studio + `hyper_motion` mode.** Never substitute another model.
- **5-second clip.** Don't go longer.
- **Reference the product image in the prompt** if one was provided. Tell the model: "the product must appear exactly as shown in the reference image — same colour, same text, do not change anything."
- **Default aspect ratio: 9:16.** Override only if user asks.
- **If generation is blocked for sensitive content:** read the prompt back, identify the trigger word (often "shocking", "secret", "guaranteed", or anything implying medical claims), strip it, retry.

## Prompt template

```
Hypermotion-style premium product launch video for {PRODUCT}.

Style: fast cuts, dramatic zooms, hero product close-ups, slow-motion product reveal,
clean studio lighting transitioning to dynamic colour wash. Mood: {MOOD}.

The product must appear exactly as shown in the reference image — same colour,
same text, same proportions. Do not change anything about the product itself.

5 seconds. {ASPECT_RATIO}. High energy. Designed to stop the scroll.
```

## Command

```bash
higgsfield generate create marketing_studio_video \
  --mode hyper_motion \
  --aspect_ratio {ASPECT_RATIO} \
  --duration 5 \
  --prompt "{COMPILED_PROMPT}" \
  --start-image {REFERENCE_IMAGE_PATH} \
  --wait
```

## After running

- Print the result URL
- Append a row to the project's generation tracker (Google Sheet) with: timestamp, product, mode, prompt, job_id, result_url, status
- Suggest 2 variations the user could test next (different hook angle, different mood word)

## Common failures

| Symptom | Fix |
|---|---|
| Text on the bottle/product is mangled | Re-run with a stronger reference instruction; consider switching to a label-free shot for the video then post-adding text in CapCut |
| Movement is too slow | Add "fast pacing, rapid cuts every 0.7 seconds" to the prompt |
| Looks like generic stock footage | Specify the brand colour palette in the prompt |
| Sensitive-content block | Strip claim words ("guaranteed", "cure", "transform"), retry |

## Reference output

A successful Hypermotion video has:
- Product visible in 4 of 5 seconds
- 6-8 micro-cuts
- One slow-motion beat
- Coordinated colour palette throughout
- Recognisable brand asset in every frame
