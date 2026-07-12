# letsphi.com

Static site for **Let's Phi** — beyond academic philosophy. Built with [Hugo](https://gohugo.io/) and the [Blowfish](https://blowfish.page/) theme, deployed to GitHub Pages.

Content migrated from the old Google Sites site (www.letsphi.com) in July 2026.

## Local development

```bash
git clone --recurse-submodules https://github.com/0xkkonrad/letsphi.git
cd letsphi
hugo server          # http://localhost:1313, live-reloads on save
```

Requires Hugo extended ≥ 0.146 (built with 0.163.3).

## Structure

```
config/_default/     # site + theme configuration (params.toml = design knobs)
content/             # one folder per page; images live next to their page
assets/img/          # logo + hero image
assets/css/custom.css# custom styles (people grid, testimonial cards)
layouts/shortcodes/  # `people` / `person` card shortcodes
interviews/          # interview transcripts: drop in inbox/, pipeline moves to processed/
newsletter/issues/   # Substack-ready issue drafts produced by the pipeline
.claude/skills/      # `new-issue` — transcript → story page + opportunities refresh + issue draft
docs/ROADMAP.md      # operating model (living library + interview flywheel) and V2 ideas
```

### Changing the design

- **Color scheme**: `colorScheme` in `config/_default/params.toml`. Blowfish ships: `blowfish` (current, purple), `avocado`, `fire`, `forest`, `princeton`, `neon`, `bloody`, `terminal`, `marvel`, `noir`, `autumn`, `congo`, `slate`, `sapphire`, `ocean`.
- **Homepage layout**: `[homepage] layout` in `params.toml` — `page`, `profile`, `hero` (current), `card`, `background`, `custom`.
- **Logo**: `assets/img/logo.png` (referenced from `config/_default/languages.en.toml`).
- **Hero image**: `assets/img/hero-wave.png`.

Theme docs: https://blowfish.page/docs/

## Deployment

Every push to `main` builds and deploys via GitHub Actions (`.github/workflows/deploy.yml`) to GitHub Pages. No manual steps.

## DNS / custom domain

The domain is registered at **Squarespace Domains** (migrated from Google Domains). See the repo's deployment docs / DNS instructions for the cut-over from Google Sites to GitHub Pages.
