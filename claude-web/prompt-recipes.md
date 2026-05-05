# Prompt Recipes — Claude.ai (MCP)

Plug-and-play prompts. Paste into a Claude chat with the Higgsfield connector enabled.

Replace `[BRACKETS]` with your specifics.

---

## Product hero shot

> Generate a product hero shot of [PRODUCT — e.g. wireless earbuds in matte black] using nano_banana_2. Aspect ratio 1:1. Studio lighting, clean white background, premium feel. Resolution 2K.

## Instagram story ad

> Generate an Instagram-ready vertical ad (9:16) for [PRODUCT]. Include a bold headline at the top: "[HEADLINE — e.g. STOP COUNTING SHEEP]". Below the product, smaller subtext: "[SUBTEXT — e.g. 60-night money back guarantee]". Use gpt_image_2 for clean text rendering.

## UGC-style ad video

> Use Higgsfield Marketing Studio to create a UGC-style video for [PRODUCT]. A real person uses the product naturally. 5 seconds. Vertical 9:16. Brand colour palette: [COLOURS].

## Hypermotion launch video

> Use Higgsfield Marketing Studio with the hyper_motion mode to create a premium launch video for [PRODUCT]. Fast cuts, dramatic zooms, product hero shots. 5 seconds. 9:16 vertical. Energetic, high-end feel.

## Soul ID — train your face

> Train a Soul ID called "[NAME]" using these reference photos: [drag in 5-20 photos of the same person]. Use the soul_v2 model.

## Soul ID — use your face

> Generate a portrait using my Soul ID `[REFERENCE_ID]`. Setting: [SCENE — e.g. modern office, soft window light]. Looking at camera, professional but warm.

## Carousel — 5 slides

> Create 5 social carousel slides for [TOPIC]. Slide 1 is a hook, slides 2–4 are key points, slide 5 is a CTA. Use product-photoshoot mode `social_carousel`. Each slide should feel cohesive — same colour palette, same typography style.

## Reference-faithful generation

> Generate an image based on this reference: [drag image]. Keep the product appearing exactly as shown — same colours, same text, same proportions. Do not change anything about the product itself. New background: [DESCRIBE NEW SCENE].

## Restyle an existing image

> Take this image [drag image] and restyle it as [STYLE — e.g. golden hour beach, cinematic, warm grade]. Use product_photoshoot mode `restyle`.

## Hero banner for a website

> Generate a wide-format hero banner (16:9 or 21:9) for [BRAND]. Headline: "[HEADLINE]". Mood: [MOOD]. Use product_photoshoot mode `hero_banner`. Resolution 2K.

## Pinterest pin

> Create a vertical 2:3 Pinterest pin for [PRODUCT]. Moodboard feel, lifestyle scene, soft natural light. Use product_photoshoot mode `moodboard_pin`.

## Marketplace main image

> Create a marketplace-compliant main product image for [PRODUCT — e.g. Amazon, Etsy]. Pure white background, product centred, no text, no extra props. Use marketplace-cards skill.

## Conceptual / surreal product shot

> Create a conceptual product shot of [PRODUCT] — surreal, levitating, with a splash element. Cinematic lighting. Use product_photoshoot mode `conceptual_product`.

## Ad creative pack — 4 variants

> Generate 4 coordinated ad variants of [PRODUCT] for Meta. Same brand, same product, but each variant emphasises a different angle: (1) feature, (2) emotion, (3) social proof / stat, (4) urgency. Use product_photoshoot mode `ad_creative_pack`.

## Animation — image to video

> Take this image [drag image] and turn it into a 5-second video. Camera move: [DESCRIBE — e.g. slow zoom in, slight rotation]. Use seedance_2_0 with `--start-image`.

## Tutorial-style ad video

> Use Marketing Studio in `tutorial` mode to create a 10-second explainer video for [PRODUCT]. A presenter walks the viewer through one feature.

## TV spot

> Use Marketing Studio in `tv_spot` mode to create a broadcast-style commercial for [PRODUCT]. 15 seconds. Cinematic, polished, professional voiceover feel.

## Virtual try-on

> Use product_photoshoot mode `virtual_model_tryout` to show [APPAREL/ACCESSORY] worn by an AI-rendered model. Setting: [LOCATION]. Lighting: [LIGHTING].

## Closeup with hands

> Generate a close-up product shot with hands holding [PRODUCT]. Use product_photoshoot mode `closeup_product_with_person`. Tight crop. Soft natural lighting.

## Lifestyle scene

> Generate a lifestyle scene featuring [PRODUCT] in real-world use. Natural environment, real action, atmosphere. Use product_photoshoot mode `lifestyle_scene`.

## Wild card video

> Use Marketing Studio in `wild_card` mode for [PRODUCT]. Let the model pick the vibe. Surprise me.

---

## Tips for better outputs

1. **Always reference a real product image** when you have one. Drag-drop the file and tell Claude "this product must appear exactly as shown."
2. **Be specific about aspect ratio** — `1:1`, `4:5`, `9:16`, `16:9`, `21:9`.
3. **Specify resolution** — `2k` for hero shots, `1k` for fast iteration.
4. **If a generation gets blocked** for sensitive content, ask Claude to read the prompt back and identify the trigger word. Don't just retry the same prompt.
5. **Track winners** — when one lands, copy the prompt and save it as a reusable recipe.
