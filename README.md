# Claude Code ABQ — May 2026

Repo for *"Inside My Claude Code Setup — Plugins, Skills, Agents, and Mobile Workflow"*, the May 14, 2026 Albuquerque Claude Code meetup.

If you scanned this QR from the room: welcome. Everything I show tonight lands here so you can take it home.

## What's in here

- `index.html` — the slide deck. Open it in any browser; press `S` for speaker notes.
- [`STATUSLINE.md`](STATUSLINE.md) — how to set up the statusline from the talk
- [`PLUGINS.md`](PLUGINS.md) — all 28 active plugins, organized by what they do, with install commands
- Coming during and after the talk:
  - my Claude Code config and `CLAUDE.md`
  - skills, plugins, agents, and slash commands
  - mobile workflow setup
  - [`power-pages-liquid-js-plugin`](https://github.com/MartyBonacci/power-pages-liquid-js-plugin) — built live at the meetup (Tim, this one's yours)

## tmux configs

Two companion repos for the mobile/multi-device workflow from the talk:

**[tmux-dangerclaude-config](https://github.com/MartyBonacci/tmux-dangerclaude-config)** — tmux dotfiles with nine aliases that invoke Claude Code with `--dangerously-skip-permissions`, removing all confirmation prompts. Built for desktop, laptop, and phone (Termux over SSH + Tailscale). ⚠️ Don't use the danger aliases on machines with production credentials.

```bash
git clone https://github.com/MartyBonacci/tmux-dangerclaude-config
cd tmux-dangerclaude-config && ./install.sh
```

**[tmux-auto-claude-config](https://github.com/MartyBonacci/tmux-auto-claude-config)** — same tmux setup but uses `--permission-mode auto` instead, the safer autonomous mode added in Claude Code v2.1.83+. Same multi-device setup (SSH + Tailscale), same session persistence — just without the "I accept all consequences" footgun.

```bash
git clone https://github.com/MartyBonacci/tmux-auto-claude-config
cd tmux-auto-claude-config && ./install.sh
```

> Pick `auto` unless you have a specific reason to go full danger mode. Both require tmux 3.0+ and an Anthropic plan that supports the respective permission mode.

## About the meetup

Claude Code ABQ is Albuquerque's AI-assisted development community. We meet monthly at the CNM STEMulus Center, hosted by Deep Dive Coding.

Our deal: we share what's actually working with AI-assisted dev. No hype, no marketing. If something better than Claude Code shows up, we'll cover that next.

Past meetups, next meetup, and RSVP → **[claudeabq.dev](https://claudeabq.dev)**

## Viewing the deck

Open `index.html` in any browser. Press `S` for speaker notes. No build step — plain HTML + reveal.js loaded from CDN.

## License

MIT — see [LICENSE](LICENSE).
