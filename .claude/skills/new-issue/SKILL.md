---
name: new-issue
description: Turn an interview transcript into a Let's Phi story page, a refreshed opportunities board, and a Substack-ready newsletter issue. Use when Konrad drops a new interview into interviews/inbox/ or says "new issue" / "process the interview".
---

# New issue pipeline

Input: one interview in `interviews/inbox/<slug>/` containing a transcript (`.md`, `.txt`, `.vtt` or similar), optionally a headshot (`.jpg`/`.png` — never `.svg`) and a `notes.md` with the interviewee's name, current role, degree(s) and links. If anything essential is missing from transcript + notes (name, current role), ask Konrad — never guess biography.

Everything below is DRAFTING. Nothing is published by this skill: Konrad reviews, then pushes (deploys the site) and pastes the issue into Substack himself.

## 1. Story article

Write `content/posts/story-<slug>/index.md`:

- Front matter: `title`, `description`, `date` (today), plus `featured.jpg`/`.png` in the bundle if a headshot was provided.
- Form: narrative profile with woven-in quotes, or Q&A if the conversation was naturally structured. 600–1,000 words. Lead with the person and the leap ("from X degree to Y job"), not with Let's Phi.
- **Quotes must be verbatim from the transcript** (light cleanup of filler words is fine; meaning-changing edits are not). Every biographical fact comes from the transcript or `notes.md` — nothing invented, nothing pulled from memory about the person.
- Voice: warm, concrete, plain. British English ("organisation"). Address the reader as "you" where natural. No LLM-slop patterns (no "in today's rapidly evolving landscape", no bullet-point life lessons, no gratuitous em-dash chains).
- End with the standing CTA: invite readers with their own story to reach out (link Konrad's LinkedIn), and link `{{< ref "opportunities" >}}`.

Add the person to `content/stories/index.md`: a `{{< person >}}` entry at the TOP of the people block (name, headshot copied into `content/stories/`, current role as `role`, degree + university + year as `sub`, their preferred link). Keep the existing entries' format exactly.

## 2. Opportunities refresh

Update `content/opportunities/index.md` → "Current openings":

- WebSearch for currently-open philosopher-shaped roles: ethics consulting, AI ethics/governance/policy, research governance, responsible tech, risk, bioethics. Also check the sources already listed under "Where to look" (GovAI etc.).
- **Verify every listing with WebFetch before adding it** — the org's own careers page, not an aggregator. Each entry: role, org (linked to the org's own page), one clause on why it fits a philosopher, deadline if known.
- Move expired/closed entries out (delete; move to "Archive" only if historically interesting). Update the "*Last refreshed:*" date.
- Quality bar: 3–8 real openings beats 15 padded ones. If the sweep finds nothing verifiable, leave the section honest and small — never pad with aggregator links or made-up roles.

## 3. Newsletter issue draft

Write `newsletter/issues/YYYY-MM-DD-<slug>.md` — Substack-ready:

- `# <Title>` — the story's hook, not "Newsletter #N".
- Story section: a 200–300 word cut of the article that stands alone, then "Read the full story →" linking to the letsphi.com post.
- "Opportunities right now" section: the fresh openings from step 2 (titles + links + one clause each), and a one-line pointer to the full board.
- Sign-off from Konrad, first person, one or two sentences, human.
- **Formatting for paste: every paragraph on a single line** (no hard-wrapped source), standard markdown links. No cadence promises ("see you next month" is banned — "until the next story" is fine).

## 4. Review gate

Spawn a cold-read subagent (first-time-reader: no context beyond the files) on both the story article and the issue draft: does it read as human, is anything confusing, does any claim look unsupported by the transcript? Fix what it flags.

Then move `interviews/inbox/<slug>/` → `interviews/processed/<slug>/`, run `hugo` to confirm the site builds, and commit everything with a message like `Story: <Name> (<field>)`.

## 5. Hand back to Konrad

Tell him exactly three things remain: (1) review the story + issue (and ideally send the draft to the interviewee for a quick OK), (2) `git push` to deploy the site, (3) paste the issue into Substack and send. (Semi-automated sending is a V2 item — see `docs/ROADMAP.md`.)
