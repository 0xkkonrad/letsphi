# Let's Phi — operating model & roadmap

Decided July 2026. Let's Phi runs as a **living library** maintained by Konrad at ≤1–2 h/month:

1. **Evergreen resource library** — the site (stories, opportunities board, events archive) is the product; SEO does distribution; agents do maintenance.
2. **Interview flywheel** — purely opportunistic: when Konrad records an interview, the `new-issue` skill (`.claude/skills/new-issue/`) drafts the story page, refreshes `/opportunities`, and drafts a Substack-ready issue. Konrad reviews ~20 min, pushes, pastes into Substack. No cadence promises anywhere on the site or in issues.
3. **AI-curated content only as a section** — the auto-swept, link-verified opportunities section rides inside interview issues. No fully AI-written issues (slop risk with this audience).

## V1 manual steps (accepted for now)

- Final Substack paste + send (~10 min, inside the review ritual).
- `git push` after review (deploys via GitHub Actions).

## V2 — to consider later

**Semi-automated newsletter sending** (parked 2026-07-12, Konrad wants this revisited):

- Substack has no official publishing API — that's the blocker for full automation on the current platform.
- Options when revisiting:
  - **Buttondown** — real API, markdown-native, can import the Substack list; paid at ~1,800 subs (~$29+/mo tier); loses Substack's recommendation-network growth.
  - **Mailgun direct** — MX for letsphi.com is already on Mailgun (do not touch the MX records — see `dns-cutover.md` era notes); full API control but we'd own list management, unsubscribes and deliverability ourselves. Most control, most ops.
  - **Browser automation into Substack** (Playwright drafts the post, Konrad clicks send) — keeps the list and network, brittle but zero migration.
- Decision criteria: only worth it if the paste step actually becomes the bottleneck or cadence rises well above ~monthly.

**Other parked ideas** (not decided, revisit if ever relevant):

- Donations: Substack paid-subs-as-tips or an Open Collective link (zero-effort liveness signal, not revenue).
- Chapters: inbound-only — the site invites people to start one; no active recruiting.
- Janitor agent: scheduled quarterly link-rot / site-up check (cheap to add once the flywheel has run a few times).
