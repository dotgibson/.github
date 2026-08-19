<div align="center">

<img src="https://raw.githubusercontent.com/dotgibson/.github/main/profile/logo.png" alt="dotgibson logo — the ~/. ring mark" width="150" height="150" />

# `dotgibson`

### _"There is no right and wrong. There's only fun and boring."_

**One Core. Every machine. Zero drift.**

A cross-platform dotfiles system that is authored **once** and fans out to every
OS you touch — Mac, Windows, and six Linux distros — plus a red-team and a
blue-team layer that stay in lock-step. Fix a thing in one place; it lands
everywhere.

<br>

[![core](https://img.shields.io/github/v/release/dotgibson/dotfiles-core?style=plastic&label=dotfiles-core&labelColor=1a1b26&color=bb9af7&logo=git&logoColor=white)](https://github.com/dotgibson/dotfiles-core/releases/latest)
[![shell](https://img.shields.io/badge/zsh_·_nvim_·_tmux_·_starship-1a1b26?style=plastic&logo=gnubash&logoColor=7aa2f7)](https://github.com/dotgibson/dotfiles-core)

[![macOS](https://img.shields.io/badge/macOS-000000?style=plastic&logo=apple&logoColor=white)](https://www.apple.com/macos/)
[![Windows](https://img.shields.io/badge/Windows-0078D6?style=plastic&logo=windows&logoColor=white)](https://www.microsoft.com/windows)
[![Debian](https://img.shields.io/badge/Debian-A81D33?style=plastic&logo=debian&logoColor=white)](https://www.debian.org)
[![Fedora](https://img.shields.io/badge/Fedora-51A2DA?style=plastic&logo=fedora&logoColor=white)](https://fedoraproject.org)
[![Arch](https://img.shields.io/badge/Arch-1793D1?style=plastic&logo=archlinux&logoColor=white)](https://archlinux.org)
[![openSUSE](https://img.shields.io/badge/openSUSE-73BA25?style=plastic&logo=opensuse&logoColor=white)](https://www.opensuse.org)
[![Alpine](https://img.shields.io/badge/Alpine-0D597F?style=plastic&logo=alpinelinux&logoColor=white)](https://alpinelinux.org)
[![Gentoo](https://img.shields.io/badge/Gentoo-54487A?style=plastic&logo=gentoo&logoColor=white)](https://www.gentoo.org)
[![Kali](https://img.shields.io/badge/Kali-557C94?style=plastic&logo=kalilinux&logoColor=white)](https://www.kali.org)

</div>

---

## Why this exists

Most dotfiles repos are a single tangle that works on exactly one machine. Copy
it to a second box and you start forking — a tweak here, an OS quirk there — and
six months later you have four subtly different setups and no idea which one is
right.

**`dotgibson` refuses to let that happen.** The shared config lives in exactly
one place, [`dotfiles-core`](https://github.com/dotgibson/dotfiles-core), and is
vendored into every machine via `git subtree`. A defect fixed once fans out
N-way. There is no "which copy is canonical" — there is only Core.

```
   edit once  ──▶  make audit  ──▶  make sync  ──▶  live on every machine
```

## The three-layer model

Everything you configure answers to one question: **what does it change with?**

| Layer         | Changes with…      | Owns                                          | Repos |
| ------------- | ------------------ | --------------------------------------------- | ----- |
| 🧬 **Core**    | nothing — it's identical everywhere | zsh modules, tmux, Neovim, git, starship | [`dotfiles-core`](https://github.com/dotgibson/dotfiles-core) |
| 💻 **OS-native** | the operating system | package manager, clipboard, paths          | [MacBook](https://github.com/dotgibson/dotfiles-MacBook) · [Windows](https://github.com/dotgibson/dotfiles-Windows) · [Debian](https://github.com/dotgibson/dotfiles-Debian) · [Fedora](https://github.com/dotgibson/dotfiles-Fedora) · [Arch](https://github.com/dotgibson/dotfiles-Arch) · [openSUSE](https://github.com/dotgibson/dotfiles-openSUSE) · [Alpine](https://github.com/dotgibson/dotfiles-Alpine) · [Gentoo](https://github.com/dotgibson/dotfiles-Gentoo) |
| 🎭 **Role**    | the operator       | offense vs. defense tooling                   | [Offense (red)](https://github.com/dotgibson/dotfiles-Offense) · [Defense (blue)](https://github.com/dotgibson/dotfiles-Defense) |

> **The test:** if it changes when the _OS_ changes, it's not Core. If it changes
> when _you as an operator_ change, it's not Core. Everything left over is Core.

## 🔴 Red meets 🔵 blue

The two Role repos are deliberate mirrors of each other:

- **[dotfiles-Offense](https://github.com/dotgibson/dotfiles-Offense)** —
  offensive engagement scaffolding, an exploit-dev companion, evasion notes,
  and the attacker-authored purple-team detections. It stacks on any OS-native
  layer rather than assuming one.
- **[dotfiles-Defense](https://github.com/dotgibson/dotfiles-Defense)** —
  detection engineering, hunt/triage tooling, version-controlled detection
  content, and a Dockerized detection lab.

Binding them together is **[htpx](https://github.com/dotgibson/htpx)** — a
structured, ATT&CK-tagged, **red↔blue-paired** corpus. Every attack sits beside
its detection, so offense and defense never drift apart. It's vendored straight
into Offense's offensive companion as its own subtree.

## How it fits together

```
                         ┌─────────────────┐
                         │  dotfiles-core  │   ← authored ONCE, source of truth
                         └────────┬────────┘
                    git subtree   │   make sync
        ┌──────────────┬──────────┼──────────┬──────────────┐
        ▼              ▼          ▼          ▼              ▼
     MacBook   Debian · Fedora   Arch     openSUSE   Alpine · Gentoo
                                  │
                                  │  + Role layer
                        ┌─────────┴─────────┐
                        ▼                   ▼
                 dotfiles-Offense    dotfiles-Defense
                   (offense) ◀──── htpx ────▶ (defense)
```

> **Windows is a host too** — but it replicates Core natively in PowerShell
> rather than vendoring the `git subtree` (it mirrors only `nvim` and
> `starship`), so by design it sits outside this Core fan-out.

Core is authored once and synced out. OS repos add only what changes with the
platform. Role repos add only what changes with the operator. Edit upstream,
`make audit`, `make sync` — **never** hand-edit a vendored `core/`.

## The whole fleet

| Repo | Role |
| ---- | ---- |
| 🧬 [**dotfiles-core**](https://github.com/dotgibson/dotfiles-core) | The Core layer — single source of truth, vendored everywhere |
| 🍎 [dotfiles-MacBook](https://github.com/dotgibson/dotfiles-MacBook) | macOS host — Homebrew, aerospace, sketchybar, ghostty |
| 🪟 [dotfiles-Windows](https://github.com/dotgibson/dotfiles-Windows) | Windows host — PowerShell, Windows Terminal, scoop/winget, WSL2 bridge |
| 🌀 [dotfiles-Debian](https://github.com/dotgibson/dotfiles-Debian) | Debian family — `apt`; Ubuntu 24.04 LTS, Debian trixie and Kali rolling from one repo |
| 🎩 [dotfiles-Fedora](https://github.com/dotgibson/dotfiles-Fedora) | Fedora — `dnf` + RPM Fusion (the Linux template) |
| 🏛️ [dotfiles-Arch](https://github.com/dotgibson/dotfiles-Arch) | Arch — `pacman` + AUR |
| 🦎 [dotfiles-openSUSE](https://github.com/dotgibson/dotfiles-openSUSE) | openSUSE — `zypper`, Tumbleweed + Leap |
| 🏔️ [dotfiles-Alpine](https://github.com/dotgibson/dotfiles-Alpine) | Alpine — `apk`, musl libc, `doas` |
| 🐄 [dotfiles-Gentoo](https://github.com/dotgibson/dotfiles-Gentoo) | Gentoo — `emerge`, USE flags, source-based |
| 🐉 [dotfiles-Offense](https://github.com/dotgibson/dotfiles-Offense) | Offensive Role — recon→exploit→evasion field refs, stacked on any OS-native layer |
| 🛡️ [dotfiles-Defense](https://github.com/dotgibson/dotfiles-Defense) | Defensive Role — detection engineering + lab |
| 🌐 [dotfiles-web](https://github.com/dotgibson/dotfiles-web) | The public showcase + docs site (Astro · Tokyo Night) |
| 🧩 [htpx](https://github.com/dotgibson/htpx) | ATT&CK-tagged red↔blue corpus, vendored into Offense |

## Start here

<div align="center">

**New to the system?** → **[the getting-started site »](https://dotgibson.github.io/dotfiles-web/)**

**Browse the docs?** → **[the documentation hub »](https://dotgibson.github.io/dotfiles-web/docs)**

**Want the rules?** → **[dotfiles-core README + CONTRIBUTING »](https://github.com/dotgibson/dotfiles-core)**

<br>

<sub>Built on a three-layer model · themed in Tokyo Night · green-audit gated end to end</sub>

</div>
