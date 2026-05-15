# Claude Code Statusline Setup

This is the statusline you saw in the talk — shows your current directory, git branch, model, effort level, context window usage, rate limits, session time, token burn rate, and your last prompt.

Powered by [`@chongdashu/cc-statusline`](https://www.npmjs.com/package/@chongdashu/cc-statusline).

---

## Quick Install

### Step 1 — Install `jq` (recommended)

Enables richer JSON parsing. Without it, some features fall back to regex.

```bash
# Mac
brew install jq

# Ubuntu / Debian
sudo apt install jq
```

### Step 2 — Generate the statusline script

```bash
npx @chongdashu/cc-statusline install
```

This writes `~/.claude/statusline.sh`.

### Step 3 — Wire it into Claude Code

Add this to `~/.claude/settings.json` (create the file if it doesn't exist):

```json
{
  "statusLine": {
    "type": "command",
    "command": "~/.claude/statusline.sh",
    "padding": 0
  }
}
```

If `settings.json` already has content, merge the `statusLine` key into the existing object.

### Step 4 — Restart Claude Code

The statusline appears at the top of every session.

---

## Bonus: Token Burn Rate + Session Time

Install [`ccusage`](https://www.npmjs.com/package/ccusage) to unlock the session timer and tokens-per-minute display:

```bash
npm install -g ccusage
```

---

## What Each Section Shows

| Icon | What it is |
|------|------------|
| 👤 | Logged-in account email prefix |
| 📁 | Current working directory |
| 🌿 | Git branch (+ `[worktree]` if in a git worktree) |
| 🤖 | Active Claude model |
| ⚡ | Effort level (`low` / `medium` / `high`) |
| 🧠 | Context window usage bar + percentage |
| 🚦 | Rate limit usage — 5-hour and 7-day windows |
| ⌛ | Time remaining in current usage session (requires `ccusage`) |
| 📊 | Total tokens used + burn rate in tokens/min (requires `ccusage`) |
| → | Your last prompt, truncated to fit the terminal |

---

## Customizing

The generated `~/.claude/statusline.sh` is plain bash — edit it directly to change colors, remove sections, or add your own data sources. The color palette uses 256-color ANSI codes; look for the `*_color()` functions near the top.

To regenerate with different options:

```bash
npx @chongdashu/cc-statusline install --theme minimal
```

Run `npx @chongdashu/cc-statusline --help` to see all available themes and flags.
