# Claude.ai Setup — MCP Connector

5 minutes. No terminal needed.

## 1. Sign up for Higgsfield

Go to [higgsfield.ai](https://higgsfield.ai) and create an account. You'll need an active subscription for generation (Starter $15/mo or Plus $49/mo).

## 2. Get the MCP connector URL

In your Higgsfield dashboard, go to **MCP and CLI**. Copy the MCP server URL.

## 3. Add it to Claude.ai

1. Open [claude.ai](https://claude.ai)
2. Click your profile → **Settings**
3. Click **Connectors** in the left sidebar
4. Click **Add custom connector**
5. Name: `Higgsfield`
6. Paste the URL from step 2
7. Click **Add**

## 4. Authenticate

Claude.ai will show the connector in a "needs auth" state.

1. Click **Configure**
2. A new tab opens to Higgsfield's OAuth page
3. Sign in with your Higgsfield account
4. Approve the connection

## 5. Set permissions

Back in Claude.ai's connector settings:
- **Always allow** for fastest workflow, OR
- **Ask each time** if you want to review tool calls

## 6. Test it

Open a new Claude chat. Click the connectors icon (🔌) → confirm `Higgsfield` is listed.

Type:
> Generate me an image of a wireless headphone in a minimalist studio setting.

Claude will call Higgsfield, generate the image, and reply with the result URL.

## What to do next

Browse the [prompt recipes](./prompt-recipes.md) for plug-and-play examples covering:
- Product hero shots
- Instagram ad statics
- UGC-style videos
- Marketing Studio launch videos
- Soul ID character training

## Limitations vs Claude Code path

- ✅ Easy setup, no terminal
- ❌ Each tool call uses more tokens (MCP is more verbose than CLI)
- ❌ No reusable skills, routines, or batch automation
- ❌ No project-level memory of past generations

If you start running 50+ generations a week, [switch to the Claude Code path](../claude-code/SETUP.md).
