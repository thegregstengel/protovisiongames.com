# protovisiongames.com

Protovision Games studio landing page. Retro terminal aesthetic inspired
by WarGames. Recreates Lightman's WOPR logon: a bare `LOGON:` prompt that
answers HELP LOGON, HELP GAMES, LIST GAMES and JOSHUA exactly as the film
does. Anything else gets "IDENTIFICATION NOT RECOGNIZED BY SYSTEM /
--CONNECTION TERMINATED--" and the screen resets. The game list contains
Big Bang Smugglers as the only real, clickable entry.

---

# Tech stack

- Static HTML (single file, no build step)
- CSS (inline in `<style>` tag)
- Vanilla JS (inline `<script>`, drives the LOGON prompt)
- Google Fonts (VT323)
- GitHub Pages (hosting)
- Zero dependencies

---

# Repo structure

```
index.html     # The entire site (HTML + CSS + JS)
CNAME          # GitHub Pages custom domain (protovisiongames.com)
.nojekyll      # Disables Jekyll processing on GitHub Pages
README.md      # Minimal (just the repo name)
```

---

# Common commands

- View locally: open `index.html` in a browser
- Deploy: push to `main` (GitHub Pages auto-serves)
- No install, no build, no test

---

# Deployment

GitHub Pages serves from the `main` branch automatically. Custom domain
configured via `CNAME` file.

---

# Conventions

- All changes go directly to `main`
- Keep it minimal: one file, no libraries, no dependencies. The only JS is
  the inline terminal script.
- Blue phosphor: glowing light-blue text (`#9ec9ff`, blue text-shadow bloom)
  on near-black (`#020308`). Not green, not a navy background.
- Prompt sits in the upper-left like a real terminal, not centered.
- VT323 monospace font throughout
- CRT scanline and vignette effects via CSS pseudo-elements

---

# Gotchas

- The entire site is one HTML file. Do not add a build step.
- Only Big Bang Smugglers is a real link (points to bigbangsmugglers.com).
  All other game titles are decorative.
- Recognized commands (case-insensitive): HELP LOGON, HELP GAMES,
  LIST GAMES, JOSHUA, TIC-TAC-TOE. Add new ones in the `respond()` function.
  Keep the film's wording verbatim.
- TIC-TAC-TOE (also TIC TAC TOE / TICTACTOE) is deliberately NOT in the
  game list. You just have to know to type it. It asks NUMBER OF PLAYERS:
  - 2: X and O alternate. Type a square number (1-9) or click a square.
  - 1: you are X, Joshua is O (easy heuristic: win, block, centre, corner).
  - 0: Joshua plays itself with perfect play (minimax), every game a
    stalemate, faster each game, screen bleaches to white, then it cycles
    the war scenarios (WINNER: NONE) and ends on "A STRANGE GAME..." before
    returning to LOGON. Nothing is interruptible during this run.
  - ESC quits a 1/2-player game back to LOGON. Y/N after a game is a single
    keypress, as is a move; NUMBER OF PLAYERS needs Enter.
- The board is an inline SVG drawn by `drawBoard()` (thick periwinkle
  strokes on black in a white frame, like the WOPR big board). The white-out
  is the fixed `#white` overlay.
- Input comes from an off-screen `<input>` so the mobile keyboard opens;
  any tap on the page refocuses it.
- Sound is synthesized with the Web Audio API (per-character printout blip,
  carrier-drop noise on disconnect). No audio files; the film's actual audio
  is not shipped. Audio unlocks on the first keypress or tap per browser
  autoplay rules.
- Mobile breakpoint at 600px

---

# Shared knowledge base (Obsidian vault)

Durable docs for this site live in the shared vault at `~/nas/Obsidian/`:

- `20-Protovision/protovisiongames-com/profile.md` -- project profile

See `~/nas/Obsidian/CLAUDE.md` for vault rules; use the `doc-writer-obsidian`
skill to publish new docs. The vault is Greg's and Claude's shared long-term
memory across machines.
