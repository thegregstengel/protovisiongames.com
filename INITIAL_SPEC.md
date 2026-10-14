> **Historical version 1.0 snapshot.** This file records the site as of June 1, 2026. Read [CLAUDE.md](CLAUDE.md) for current behavior. The live site is a one-file interactive LOGON terminal. Vanilla JavaScript is allowed in that file. Sound uses the Web Audio API, and the site ships no audio files. The palette is blue phosphor. TIC-TAC-TOE is a hidden command.

# PROTOVISION GAMES

## Product & Technical Design Document

### Version 1.0 (retrofit)

> **Note on this document.** This spec was written *after* the site shipped, to
> bring `protovisiongames.com` in line with the sibling Protovision projects
> (`jackslevel.com`, `brookesplate.com`) that each carry an `INITIAL_SPEC.md`.
> It documents what exists and the philosophy that governs it. This is a
> single static HTML file by design — most sections of the standard 22-section
> template do not apply, and where that is the case the section says so plainly
> rather than inventing scope. **The guiding rule is: keep it simple.**

---

# 1. Product Overview

**PROTOVISION GAMES** is the studio landing page for Protovision Games. It is a
single static HTML file presenting a retro CRT-terminal "game list" inspired by
the WOPR terminal from the 1983 film *WarGames*.

The list reproduces the film's game menu (FALKEN'S MAZE → GLOBAL THERMONUCLEAR
WAR) as decorative, non-clickable entries. The one real, live entry is
**BIG BANG SMUGGLERS**, which links out to `bigbangsmugglers.com` — the studio's
shipped game. New studio titles are added to the list as they go live.

The page is intentionally a curiosity and a calling card, not an app. It loads
instantly, has zero dependencies beyond one webfont, and is meant to be
maintenance-free.

---

# 2. Users and Personas

There is one persona and it is informal.

### Visitor / Curious Passer-by
Someone who heard about Protovision Games, saw a link, or is poking at the
domain. They should immediately get the joke (WarGames), recognize it as a
games studio, and find the one working link to the studio's live game.

There are no accounts, no roles, no admins, no logged-in state. The site does
not know or care who the visitor is.

---

# 3. Problems and Goals

## Problem
Protovision needs a public face at its apex domain that (a) signals "games
studio," (b) has personality, and (c) points to the studio's live products —
without becoming a thing that needs ongoing engineering.

## Goals
- Establish the studio's presence at `protovisiongames.com`.
- Express the brand: retro, playful, WarGames-literate, hacker-adjacent.
- Surface live games as one-line links.
- Cost effectively nothing to run and nothing to maintain.

## Non-Goals
- Not a marketing site, not a blog, not a store, not a portfolio CMS.
- No analytics funnel, no lead capture, no SEO program.
- No per-game detail pages — games link out to their own sites.

---

# 4. MVP Scope

The site *is* the MVP and is considered complete.

## Included
- One CRT-terminal landing page (`index.html`).
- Decorative WarGames game list.
- One (or more, as they ship) live links to studio games.
- CRT visual treatment (scanlines, vignette flicker, blinking cursor, phosphor glow).
- Mobile responsive breakpoint.

## Excluded (deliberately, possibly forever)
- JavaScript of any kind.
- A build step / toolchain / framework.
- Multiple pages or routing.
- Backend, database, auth, forms, APIs.
- Content management — edits are made by hand in the HTML.

---

# 5. Feature Set

- **Game list.** An unordered list styled as a terminal menu. Each item is
  prefixed with a `>` glyph. Decorative items are dim green; live items are
  bright green, glow on hover, and wrap an `<a>` that opens in a new tab.
- **Prompt + cursor.** A bare `>` prompt followed by a blinking block cursor,
  evoking a terminal awaiting input.
- **CRT effects (pure CSS).** Scanline overlay, radial vignette with a slow
  flicker animation, phosphor text-shadow glow.
- **Responsive.** Single breakpoint at 600px reduces font size and padding.

Adding a newly-shipped game = add one `<li class="available">` with an anchor.
That is the entire content-management story.

---

# 6. User Flows

There is one flow:

1. Visitor opens `protovisiongames.com`.
2. Reads the terminal game list; gets the WarGames reference.
3. Clicks the one bright/live entry (e.g. BIG BANG SMUGGLERS).
4. Lands on that game's site in a new tab.

---

# 7. Data Model

None. There is no data layer. "Content" is the hardcoded HTML game list. If a
data model is ever wanted, that is a signal the project has outgrown its
premise — reconsider before adding one.

---

# 8. Architecture

```mermaid
graph LR
    REPO["GitHub repo\nthegregstengel/protovisiongames.com\nmain branch"] -->|GitHub Pages auto-serve| LIVE["protovisiongames.com\n(index.html)"]
    LIVE -->|outbound link| BBS["bigbangsmugglers.com"]
```

Push to `main` → GitHub Pages serves the static file at the custom domain. There
are no other moving parts.

---

# 9. Tech Stack

| Layer      | Technology           | Notes                                  |
| ---------- | -------------------- | -------------------------------------- |
| Markup     | HTML5                | One file                               |
| Styling    | CSS3 (inline `<style>`) | CRT effects, animations, responsive |
| Font       | VT323 (Google Fonts) | Terminal / CRT typeface                |
| Scripting  | None                 | Zero JS                                |
| Framework  | None                 | Zero dependencies                      |
| Build      | None                 | No toolchain                           |
| Hosting    | GitHub Pages         | Custom domain via `CNAME`              |
| CI/CD      | Push to `main` → live | No pipeline                           |

**Color:** green phosphor only — `#00ff41` (bright), `#00cc34`/`#80ffaa`
(text), `#007a1f` (dim) on black. Do not introduce other colors.

---

# 10. API Requirements

None. The site neither exposes nor consumes any API.

---

# 11. Security and Permissions

Minimal by construction — there is no server, no input, no state, nothing to
authenticate or authorize.

- All outbound links use `target="_blank"` with `rel="noopener"`.
- No JS means no XSS surface and no third-party script supply chain (beyond the
  Google Fonts stylesheet).
- HTTPS is provided by GitHub Pages.

---

# 12. UI/UX Direction

## Philosophy
Evoke a 1983 mainframe terminal. The whole page should read as a CRT awaiting a
command. Restraint is the aesthetic — emptiness and glow do the work.

## Characteristics
- Centered terminal column, max ~520px.
- Green-on-black phosphor with text-shadow glow.
- Scanlines + vignette flicker for CRT authenticity.
- Blinking block cursor at a bare `>` prompt.
- No chrome, no nav, no footer, no headings — just the list and the prompt.

---

# 13. Theme and Branding

- **Reference:** WOPR / *WarGames* (1983). The game list is the film's menu.
- **Tone:** playful, retro, hacker-literate, understated.
- **Personality:** the studio is in on the joke; knows its roots; doesn't
  over-explain.
- **Naming convention:** Protovision hosts/services carry WarGames names
  (WOPR, Joshua, Crystal Palace). This site is the public expression of that
  in-house theme.

---

# 14. Admin and Moderation

Not applicable. No users, no content submission, no moderation surface.

---

# 15. Notifications

Not applicable. The site sends nothing.

---

# 16. Analytics

None currently, by choice. If basic traffic insight is ever wanted, a
privacy-friendly, cookieless, no-JS-or-single-snippet option (e.g. Plausible)
could be added — but only if there is a real question to answer. Default is no
analytics.

---

# 17. Monetization

None. This is a studio calling card, not a revenue surface. Revenue lives in the
games it links to.

---

# 18. Integrations

- **Outbound links** to studio game sites (currently `bigbangsmugglers.com`).
- **Google Fonts** for the VT323 webfont.

No other integrations, and none planned.

---

# 19. Deployment and Operations

- **Hosting:** GitHub Pages, custom domain `protovisiongames.com` via `CNAME`.
- **Deploy:** `git push origin main` — served immediately. No build, no preview,
  no staging.
- **Branching:** changes go straight to `main`. (Branch if you want a sanity
  check, but the site is small enough to verify by eye.)
- **`.nojekyll`** disables Jekyll processing on GitHub Pages.
- **Operational burden:** effectively zero. No secrets, no env, no rotation, no
  uptime concerns beyond GitHub Pages itself.

---

# 20. Testing Plan

Manual, by eye. Open the file in a browser; confirm the list renders, the live
link works, the cursor blinks, and the mobile breakpoint looks right. No
automated test suite — the surface is too small to justify one.

---

# 21. Legal and Compliance

Minimal. No personal data is collected or processed, so privacy-law exposure is
negligible. The WarGames game titles are used as an affectionate homage; they
are descriptive list items, not a commercial product claim.

---

# 22. Roadmap

The roadmap is mostly "do nothing on purpose."

## Steady state
- Keep the site live and unchanged.
- Add a live link when a new studio game ships (one `<li class="available">`).

## Allowed evolution (only if a real need appears)
- Optional cookieless analytics snippet.
- Minor copy/animation polish in keeping with the CRT aesthetic.

## Explicitly off the table (unless the project's premise changes)
- JavaScript, a build step, a framework, multiple pages, a backend, a CMS.
  Any of these is a sign the site is becoming something it was never meant to
  be — stop and reconsider first.

---

# Final Note

The strongest version of `protovisiongames.com` is the simplest one: a single
HTML file that loads instantly, gets the joke across, and points at the games
that actually matter. Complexity is the enemy of this project. When in doubt,
leave it alone.
