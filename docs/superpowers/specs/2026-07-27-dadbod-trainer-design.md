# dadbod-trainer: Design

## Purpose
An open-source workout diary. Fahd started training with Brian Andrews (celebrity trainer, @brianandrewsfit, founder of Define Fit, @definefitapp) on Sunday, July 26, 2026. Each session gets logged publicly as a simple static site, growing over time as an ongoing diary.

## Scope
Ongoing diary, not a one-off. Session 1 is the first entry; more sessions get added later through the same manual workflow.

## Architecture
Plain static HTML/CSS. No JS framework, no build tooling, no static site generator, no npm dependency. GitHub Pages serves the site directly from the repo root on `main`.

## Structure
- `index.html` — diary homepage. Lists entries newest-first as cards (date, title, quick stats), each linking to its own page.
- `sessions/session-N.html` — one page per diary entry. Not every entry is a structured lifting session:
  - **Workout sessions** (e.g. session 1): the clean session card (Round / Slot / Exercise / Muscle / Target / Note, as structured in the source Excel file), plus a collapsible "How this was built" section with the coaching transcript for that session (Slack quotes, Claude's draft attempts including the wrong ones, Brian's verbatim corrections, the "RULE LEARNED" callouts).
  - **Check-in / cardio / nutrition entries** (e.g. session 2): no rounds table. Presented as the Slack-style exchange (guidance given, questions asked) plus a short summary, still crediting Brian/Define Fit.
- `style.css` — single shared stylesheet. Minimal: system fonts, whitespace, plain table styling, no color-scheme flourishes.
- `source-files/` — raw source material per session (the Excel/Word files as received), kept for reference, not published as-is.
- `README.md` — project pitch, what this is, how it's updated, credits to Brian Andrews / Define Fit with links.
- `LICENSE` — MIT.
- `CLAUDE.md` — project-local context so a fresh Claude Code session started from this folder has full context without relying on cross-session memory.

## Content fidelity
Transcript quotes (Brian's corrections, Slack messages, Claude's draft attempts) are kept verbatim, including their em-dashes, since altering quoted source text would misrepresent it. All other writing (README, captions, headers, commit messages) follows the standard no-em-dash rule.

## Sensitive health information
Physical injury detail (e.g. the 2020 wrist injury) is published verbatim since it's directly load-bearing for the exercise choices shown. Medical/medication history (e.g. hypertension and its treatment) is summarized without naming the specific condition or medication, referencing only the general health goal it motivates. This distinction is decided per piece of information, not a blanket rule, so re-check it when a new session includes personal health detail.

## Update workflow
No script, no data pipeline. For each new session, Fahd hands the session data to Claude in a Claude Code conversation run from this folder; Claude writes/appends the new `sessions/session-N.html` and a new `index.html` entry by hand.

## Deployment
1. Push the repo to `fahdi/dadbod-trainer` on GitHub, public.
2. Enable GitHub Pages: Settings → Pages → Deploy from branch → `main` / root (or via `gh api`).
3. Confirm the live URL (`https://fahdi.github.io/dadbod-trainer/`) serves the site after the first Pages deploy.

## Out of scope
- No backend, no database, no user accounts.
- No build step or static site generator.
- No automatic ingestion of Excel/Word files — each session is hand-authored into HTML.
