# protovisiongames.com

Protovision Games studio landing page. Retro terminal aesthetic inspired
by WarGames. Lists fictional WOPR game titles with Big Bang Smugglers as
the only real, clickable entry.

---

# Tech stack

- Static HTML (single file, no build step)
- CSS (inline in `<style>` tag)
- Google Fonts (VT323)
- GitHub Pages (hosting)
- Zero dependencies

---

# Repo structure

```
index.html     # The entire site (136 lines)
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
- Keep it minimal: one file, no JS, no dependencies
- Green phosphor color scheme (`#00ff41` on black)
- VT323 monospace font throughout
- CRT scanline and vignette effects via CSS pseudo-elements

---

# Gotchas

- The entire site is one HTML file. Do not add a build step.
- Only Big Bang Smugglers is a real link (points to bigbangsmugglers.com).
  All other game titles are decorative.
- Mobile breakpoint at 600px

---

# Shared knowledge base (Obsidian vault)

Durable docs for this site live in the shared vault at `~/nas/Obsidian/`:

- `20-Protovision/protovisiongames-com/profile.md` -- project profile

See `~/nas/Obsidian/CLAUDE.md` for vault rules; use the `doc-writer-obsidian`
skill to publish new docs. The vault is Greg's and Claude's shared long-term
memory across machines.
