---
title: Personal Profile Page — vfreitas.com
date: 2026-05-10
status: approved
---

# Personal Profile Page

## Goal

A casual, personal public presence page at vfreitas.com (and www.vfreitas.com). Not a job-hunting page or freelance pitch — just a clean "here's who I am" place to point people to.

## Design Principles

- Tone: casual and personal, not corporate or resume-like
- Aesthetic: dark minimal, inherited from the Drifting app page (`#080808` background, `#a07af0` accent)
- Low maintenance: no sections that require frequent updates
- Single HTML file with inline CSS, no build tooling

## Sections

### 1. Hero

- Circular profile photo (`photo.jpg` — casual Instagram-style photo)
- Name: **Vitor Freitas**
- Tagline: *"I write code for a living. Sometimes for fun too."*
- Background line (muted, smaller): *"Fintech engineer — previously Nubank, now Toast."*
- Social icon links: GitHub (https://github.com/vitorpfr) and LinkedIn (https://www.linkedin.com/in/vitorpfreitas/)

### 2. Projects

Section title: **Projects**

One card, same dark surface/border/rounded style as Drifting feature cards:

- **Drifting** — *"An iOS radio app I built. Visualizes music as it plays."*
  - Framed as a personal project, not a shipped product
  - Links to https://github.com/vitorpfr (GitHub profile)

Below the card: a horizontal scrolling strip of phone screenshots (`screenshots/screenshot1-4.png`), same style as the original Drifting page — tall rounded images, horizontal scroll on mobile, centered on desktop.

A second card slot is reserved for **Drifting Web** (a website for the radio app, currently in development). It will be added when ready — no placeholder shown in the initial version.

### 3. About

Three cards in a single row (same card style as Projects):

| Card | Content |
|------|---------|
| **Where** | Dublin, Ireland. Senior Engineer & Tech Lead at Toast. |
| **Stack** | Mostly Java, Kotlin, Clojure — open to whatever gets it done |
| **Outside work** | Playing drums and bass, catching live concerts |

No "contact" card — email is in the footer to avoid repetition.

### 4. Footer

- © 2026 Vitor Freitas
- Links: GitHub · LinkedIn · hello@vfreitas.com

## Color Tokens (inherited from Drifting)

```
--bg:      #080808
--surface: #111111
--border:  #222222
--text:    #f0f0f0
--muted:   #888888
--accent:  #a07af0
```

## Layout & Typography

- Font: `-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`
- Max content width: ~600px centered
- Responsive: single column on mobile (cards stack vertically)
- Hero photo: 96px circular (border-radius: 50%)

## Files

- `index.html` — single file, inline CSS (replaces existing Drifting-based file)
- `photo.jpg` — profile photo to be added by user
- `screenshots/screenshot1-4.png` — Drifting app screenshots (already exist in repo)

## Out of Scope

- Blog or writing section
- Detailed work history / timeline
- Contact form
- Analytics
- "Currently building" section (requires ongoing maintenance)
- Drifting Web card (added in a future update when the project is ready)
