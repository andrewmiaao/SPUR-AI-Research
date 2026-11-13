# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

The repo is named "SPUR AI Research" (exploring sustainability topics with AI agents), but its active project is the **Brooklyn Community Kitchen AI Assistant**: an operational tool for a small nonprofit's five board members and one part-time helper. It covers weekly volunteer shift sign-ups with caps and waitlists, a volunteer master spreadsheet, scheduled emails, donation tracking, and expense/budget reports. The conversational AI agent is a **later phase and not part of v1**.

There is no application code yet. There is no build, lint or test tooling. The repo has:

- Planning docs at the root: `CONCEPT-IDEA.md` → `SPECIFICATION.md` → `PLAN.md` → `BACKLOG.md`, plus `WORK-LOG.md`.
- `docs/`: a static GitHub Pages site (`index.html` is the SPUR placeholder landing page; `.nojekyll` disables Jekyll). It is served straight from `/docs` with no build step.
- `.vscode/mcp.json`: MCP servers for VS Code/Copilot (GitHub, Context7, Microsoft Learn, Tavily, memory, sequential-thinking, filesystem, Playwright). The Tavily key is a prompt input. Never hard-code it.

## Planning workflow (from `.github/copilot-instructions.md`)

- The four planning docs are the source of truth. Check each doc's **status and reviewer sign-off** before relying on it. Current state: concept `Approved`; spec v0.2.2, plan and backlog approved by the owner on 2026-11-13. That approval covers the documents only: the spec's open questions, readiness checklist and implementation gates are still open, and blocked or unestimated backlog tasks stay blocked.
- Order is concept → spec → plan → backlog → implementation. Backlog items must trace to spec stories/requirements (US-xx, FR-xx). New ideas go under `Later`.
- **Do not choose** a language, framework, data store, auth approach, email provider or other undecided architecture. Write it up as a proposal with rationale and rejected alternatives for the owner to review (see the pattern in `PLAN.md` §6).
- Many requirements are blocked on open questions (OQ-01…OQ-16 in `SPECIFICATION.md` §12). If a requirement depends on an open OQ, stop and record the blocker. Don't invent the behavior.
- Do not claim work is approved, reviewed, deployed or complete unless the documented criteria are met. Report exactly what was verified.
- For research: cite credible sources, separate evidence from interpretation, state uncertainty, and never invent sources, quotations or data.

## Current milestone scope (M0/M1, demo production release targeted for 2026-11-21)

- **M0:** a minimal Brooklyn Community Kitchen entry shell deployed to a real production URL. The proposal is a `/kitchen/` subpath under `docs/` so the existing SPUR root page stays intact. Nothing is done until the deployed URL (not a local preview) loads on desktop and phone.
- **M1:** a fake-data prototype using plain HTML/CSS plus a little browser JS, with hard-coded fictional data and state kept in the page only. It shows three states: choosing a task, a full task putting the request on the waitlist, and a second task request in the same week being rejected.
- Not allowed in M0/M1: real personal or financial data, persistence, form submission to live systems, Google Sheets/Gmail/payment integrations, operator auth, any Squarespace edits (blocked on OQ-16), new accounts, and any cost. The budget is close to $0, and any spend needs owner approval.

## Domain rules that are easy to get wrong

- **One task per volunteer per week.** A second request is rejected even when the times don't overlap (spec §8, FR-04).
- **Public form submissions never write to the master profile sheet.** Only authenticated operators edit volunteer profiles (FR-15/FR-16). Sign-up/waitlist records live in a separate sheet, linked by email. The public form never shows stored volunteer information, including emails. Email matching happens only in the backend, for operator review, and there is no prefill.
- The public form shows only two shift blocks, 7:30 a.m. and 11:00 a.m. The detailed task table with caps is the internal operating schedule.
- All scheduled times are US Eastern and follow DST: signup email Tue ~2:30 p.m., sign-ups close Thu 6:00 p.m., confirmations Fri 9:00 a.m.
- Donation records contain **no operator identity**. They come automatically from the payment system.
- There is no onboarding/training workflow. Just a compliance video link goes in the Tuesday email (FR-11). The spec still lists US-05 as a blocked Must, which is a known inconsistency.
- November 21 is a **demo production release**: the M0/M1 demo live at a production URL with fake data. It is not the v1 release.
- Failed saves, sends or report calculations must never look like success or a valid zero.

## Work log

`WORK-LOG.md` records hours **the owner reports**. Never infer time from chat activity, and treat unreported time as unknown, not zero.
