# dotgibson

> _"Hack the Gibson."_

A **ten-repo dotfiles system** built on a three-layer model — one Core, authored
once, vendored into every machine; OS-native layers for each platform; and Role
layers for offense and defense. The Gibson is the mainframe everything reaches
back to: [`dotfiles-core`](https://github.com/dotgibson/dotfiles-core) is the
single source of truth, `git subtree`-vendored into every OS repo so a fix lands
once and fans out N-way.

## The three layers

| Layer         | What it owns                                   | Repos |
| ------------- | ---------------------------------------------- | ----- |
| **Core**      | zsh, tmux, nvim, git, starship — identical everywhere | [`dotfiles-core`](https://github.com/dotgibson/dotfiles-core) |
| **OS-native** | package manager, clipboard, paths — per platform | [MacBook](https://github.com/dotgibson/dotfiles-MacBook) · [Windows](https://github.com/dotgibson/dotfiles-Windows) · [Fedora](https://github.com/dotgibson/dotfiles-Fedora) · [Arch](https://github.com/dotgibson/dotfiles-Arch) · [openSUSE](https://github.com/dotgibson/dotfiles-openSUSE) · [Alpine](https://github.com/dotgibson/dotfiles-Alpine) · [Gentoo](https://github.com/dotgibson/dotfiles-Gentoo) |
| **Role**      | tooling layered on top of an OS               | [Kali (offensive)](https://github.com/dotgibson/dotfiles-Kali) · [Defense (defensive)](https://github.com/dotgibson/dotfiles-Defense) |

Plus the supporting cast:

- **[dotfiles-web](https://github.com/dotgibson/dotfiles-web)** — the public
  showcase + docs site (Astro, Tokyo Night, GitHub Pages). Not a config layer —
  the system's public face.
- **[htpx](https://github.com/dotgibson/htpx)** — the structured, ATT&CK-tagged,
  red↔blue-paired corpus vendored into Kali's offensive companion.

## Red meets blue

The two Role repos are mirrors: **Kali** carries offensive engagement tooling and
the attacker-authored purple-team detections; **Defense** carries detection
engineering, hunt/triage tooling, and a Dockerized detection lab. `htpx` pairs
each attack with its detection so the two sides stay in step.

## How it fits together

```
dotfiles-core  ──git subtree──▶  dotfiles-{MacBook,Windows,Fedora,Arch,openSUSE,Alpine,Gentoo}
     │                                        │
     │                                   + Role layer
     └──────────────────────────▶  dotfiles-{Kali,Defense}

htpx  ──git subtree──▶  dotfiles-Kali/offensive/companion
```

Core is authored once and synced out; OS repos add only what changes with the
platform; Role repos add only what changes with the operator. Edit upstream,
`make audit`, `make sync` — never hand-edit a vendored `core/`.

## Start here

New to the system? → **[dotfiles-web getting-started](https://github.com/dotgibson/dotfiles-web)**
Want the rules? → **[dotfiles-core README + CONTRIBUTING](https://github.com/dotgibson/dotfiles-core)**
