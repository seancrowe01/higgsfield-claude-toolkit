# Claude Code Setup — Higgsfield CLI

15 minutes. Faster, cheaper, and unlocks batch automation that the browser path can't do.

## Prerequisites

- [Claude Code](https://claude.com/claude-code) installed
- Node.js 20+ (`node --version`)
- A Higgsfield account ([higgsfield.ai](https://higgsfield.ai))

## Mac / Linux

```bash
# 1. Install the CLI
curl -fsSL https://raw.githubusercontent.com/higgsfield-ai/cli/main/install.sh | sh

# 2. Authenticate (browser opens)
higgsfield auth login

# 3. Install agent skills (run from your project root)
cd /path/to/your-project
npx skills add higgsfield-ai/skills
```

When `npx skills` prompts:
- Source: confirm `higgsfield-ai/skills`
- Skills to install: **space to toggle each of the 4 skills**, then enter
- Agents: pick **Claude Code** (`.claude/skills`)
- Scope: **Project**

## Windows

The npm install `npm install -g @higgsfield/cli` fails on Windows due to a known tar/backslash bug in the postinstall script. Use the manual install below.

### Step 1 — Download the binary

```powershell
# In PowerShell
$ver = "0.1.28"
$dir = "$env:LOCALAPPDATA\Higgsfield\bin"
mkdir -p $dir
Invoke-WebRequest -Uri "https://github.com/higgsfield-ai/cli/releases/download/v$ver/hf_${ver}_windows_amd64.tar.gz" -OutFile "$env:LOCALAPPDATA\Higgsfield\hf.tar.gz"
tar -xzf "$env:LOCALAPPDATA\Higgsfield\hf.tar.gz" -C $dir
```

### Step 2 — Avoid the HuggingFace clash

The binary ships as `hf.exe` — but if you have HuggingFace's CLI installed, that binary is also called `hf`. Rename Higgsfield's binary to avoid the clash:

```powershell
Rename-Item "$env:LOCALAPPDATA\Higgsfield\bin\hf.exe" "higgsfield.exe"
```

### Step 3 — Add to user PATH

```powershell
[Environment]::SetEnvironmentVariable("Path", $env:Path + ";$env:LOCALAPPDATA\Higgsfield\bin", "User")
```

**Close and reopen your terminal** so the new PATH loads.

### Step 4 — Verify

```powershell
higgsfield version
# Should print: higgsfield 0.1.28 ...
```

If you previously tried `npm install -g @higgsfield/cli` and it failed, clean up the broken shim:

```powershell
Remove-Item "$env:APPDATA\npm\higgsfield*" -Force
```

### Step 5 — Authenticate

```powershell
higgsfield auth login
```

### Step 6 — Install skills

```powershell
cd C:\path\to\your-project
npx skills add higgsfield-ai/skills
```

Same picker as Mac/Linux. Pick all 4 skills, Claude Code, Project scope.

## Verify the full install

```bash
# Confirm CLI works
higgsfield version

# Confirm you're authenticated
higgsfield account

# Confirm skills are installed
ls .claude/skills/ | grep higgsfield
# Should list 4 entries:
#   higgsfield-generate
#   higgsfield-marketplace-cards
#   higgsfield-product-photoshoot
#   higgsfield-soul-id
```

## First test run (uses credits)

```bash
higgsfield generate create nano_banana_2 \
  --prompt "abstract teal and pink gradient, soft light, minimal" \
  --aspect_ratio 1:1 --resolution 2k --wait
```

Should return a result URL within ~30 seconds.

## Set up your creative project

Drop the [`CLAUDE.md.template`](./CLAUDE.md.template) into your project root and customise it. This gives Claude Code the right defaults (model preferences, brand colours, voice rules) for every generation.

## What's next

- **Custom skills** — extend Higgsfield's official skills with your own recipes. See [`skills/`](./skills/).
- **Routines** — schedule batch generation to run on a cadence. See [`routines/`](./routines/).
