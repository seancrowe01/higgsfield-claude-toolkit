# Higgsfield × Claude Toolkit

Turn Claude into a one-person creative agency using Higgsfield AI for image and video generation across 30+ models — Nano Banana Pro, Veo 3.1, Kling 3.0, Seedance 2.0, Marketing Studio, and more.

Two setup paths. Pick the one that matches you.

---

## Path A — Claude.ai (browser)

Best for: ad-hoc generation, no terminal, "just make me an image".

1. Go to **claude.ai → Settings → Connectors → Add custom connector**
2. Name it `Higgsfield`
3. Paste the MCP URL from [higgsfield.ai/mcp](https://higgsfield.ai/mcp)
4. Click **Configure** → sign in with your Higgsfield account
5. Done. In any Claude chat, the `Higgsfield` connector is now available.

**Try it:**
> Make me a hero image for a sleep supplement brand. Modern, calming, minimal.

[Full Claude.ai setup walk-through →](./claude-web/SETUP.md)

---

## Path B — Claude Code (terminal)

Best for: agencies, batch generation, automation, building reusable skills.

```bash
# 1. Install the CLI (Mac/Linux)
curl -fsSL https://raw.githubusercontent.com/higgsfield-ai/cli/main/install.sh | sh

# 2. Authenticate
higgsfield auth login

# 3. Install agent skills
npx skills add higgsfield-ai/skills
```

Windows users: [the npm install fails on Windows due to a tar-path bug. Manual install instructions here](./claude-code/SETUP.md#windows).

**Try it from inside Claude Code:**
> Make me a Hypermotion launch video for a wireless headphone brand.

[Full Claude Code setup walk-through →](./claude-code/SETUP.md)

---

## What's in this toolkit

| Folder | What |
|---|---|
| [`claude-web/`](./claude-web/) | MCP connector setup + 20 plug-and-play prompt recipes |
| [`claude-code/`](./claude-code/) | CLI setup, project template, custom skills, automation routines |
| [`examples/`](./examples/) | Sample outputs and breakdowns of what's possible |

## Custom skills (Claude Code path)

Pre-built recipes that extend Higgsfield's official skills:

- **`hypermotion-video`** — Premium product launch videos via Marketing Studio. Reverse-engineered from a winning generation.
- **`creative-slate`** — Weekly Sunday routine: analyses past performance, ideates 50 new ad variations, writes them to a Google Sheet.
- **`ad-batch-generator`** — Monday morning routine: pulls 30 unprocessed ideas from the sheet, generates them, marks each as complete.

[Skills directory →](./claude-code/skills/)

## License

MIT. Use, fork, and remix freely.

## Credits

Built on top of [Higgsfield AI's official CLI](https://github.com/higgsfield-ai/cli) and [skills](https://github.com/higgsfield-ai/skills). Inspired by the Next Level YouTube walk-through.
