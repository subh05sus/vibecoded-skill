# vibecoded

**Make AI Slop Again.**

A Claude Code skill that builds or restyles UI in the look every AI coding assistant shipped in 2023: purple-blue gradients, glassmorphism, glowing pill buttons, blurred gradient orbs, an oversized centered hero, a browser mockup with floating cards, and copy like "Supercharge Your Workflow With **Next-Gen AI**".

It's a parody, but a tidy one: consistent tokens, reusable components, responsive, keyboard accessible, reduced-motion aware, and no fake real-world logos, testimonials or stats.

It **only runs when you type `/vibecoded`**. Claude never loads it on its own, so it can't leak gradients into your normal work.

---

## Use it

```
/vibecoded
/vibecoded Build a landing page for an AI-powered music discovery platform
/vibecoded Redesign the existing dashboard
/vibecoded Add a pricing section to the current website
/vibecoded --mode maximum Build a landing page for an AI note-taking app
/vibecoded --mode light A waitlist page for a pet-sitting startup
```

With nothing after it, you get a complete generic AI SaaS landing page. In an existing project it reuses your framework, components and icons and only touches what you asked for. In an empty folder it writes one self-contained `index.html`.

### Modes

| Mode | What you get |
|---|---|
| `classic` (default) | Dark `#0B1020`, purple-blue-pink gradients, glass cards, orbs, glow |
| `maximum` | More orbs, spinning gradient borders, shimmer buttons, extra badges, more motion |
| `light` | White and pastel washes, translucent white cards, soft blue shadows, dark oversized type |

You can also just say it: "max slop", "light mode", "pastel".

---

## Install

In Claude Code, as a plugin:

```
/plugin marketplace add subh05sus/vibecoded-skill
/plugin install vibecoded@vibecoded
```

Or from a copy of this repo:

```bash
git clone https://github.com/subh05sus/vibecoded-skill ~/vibecoded-skill
ln -s ~/vibecoded-skill/skills/vibecoded ~/.claude/skills/vibecoded
```

## What's inside

```
skills/vibecoded/SKILL.md    the design system and workflow Claude follows
```

The front matter sets `disable-model-invocation: true`, which is what keeps it manual-only.

## License

MIT
