# PLAN: Brooklyn Community Kitchen AI Assistant

> **Status:** Approved by the project owner on 2026-11-13 (M2-M6 gates, decisions, and estimates remain open). **On 2026-11-18 the owner replaced the v1 approach** (section 6): the M2–M6 sections below are a draft revision awaiting owner approval.  
> **Planning date:** 2026-11-06  
> **Inputs:** [CONCEPT-IDEA.md](./CONCEPT-IDEA.md) (owner-approved) and [SPECIFICATION.md](./SPECIFICATION.md) v0.2.2 (owner-approved 2026-11-13; implementation readiness remains open); this revision follows the v0.3.2 draft  
> **Companion:** [BACKLOG.md](./BACKLOG.md) holds the ordered task list. This plan defines scope, sequence, proposed technical decisions, gates, and effort.

## 1. Purpose and planning status

The project owner's M0/M1 scope was approved on 2026-11-03: deliver a production-hosted public entry shell and a fake-data volunteer-flow prototype. This document turns that scope into a timeboxed plan; the owner approved it on 2026-11-13, and that approval does not approve any unresolved product or technical decision.

The capacity provided for this plan is **10 hours per week**. The original target was M6 by the end of week 5 (50 hours total). On 2026-11-18 the T-011 checkpoint found that infeasible, and **the owner chose to move the M6 date** rather than cut scope or add hours. The new target is **M6 by the end of week 14 (February 14, 2027)**, 140 hours in total at the same 10 hours per week (section 5). It is a target worked out from draft estimates, not a commitment: 22 hours of the estimate are provisional and several open questions remain. No Must story is being removed or deferred from v1 by this target.

The M0/M1 target is November 21, 2026. On 2026-11-13 the owner confirmed this as the target for a **demo production release**: the M0 entry shell and the M1 fake-data volunteer flow, deployed to and demonstrated at a production URL. The concept and specification now use the same wording. It is not the full v1 release; no v1 production-release date is committed.

## 2. Scope and guardrails

### M0/M1 target scope

- **M0:** publish a real, directly reachable production URL for a minimal Brooklyn Community Kitchen tool-entry shell. It may be empty of operational functions, but it must load from production and must not expose real data.
- **M1:** demonstrate a fake-data volunteer flow: select a task, see a full-task waitlist state, and see a second task request in the same week rejected. This is a prototype, not a live signup system.
- Verify the public page on desktop and phone, walk through it with the owner, and record feedback and blockers.

### Not authorized by M0/M1

- Real volunteer, donor, or financial data; production signup submissions; persistence; or connection to Google Sheets, email, payments, or other external services.
- Operator authentication, profile editing, scheduled email, withdrawals, accounting, or onboarding beyond the fake-data prototype.
- Changes to the existing Squarespace website until OQ-16 (location, method, access, and cost) is resolved and approved.
- A conversational AI agent, or replacement/redesign of the existing Squarespace website.

Do not treat a prototype or partial milestone as satisfying the full v1 definition of done. No real-data use is allowed until the specification's privacy, authentication, and spreadsheet gates are cleared.

## 3. Capacity, budget, and estimation

- **Available capacity:** 10 hours/week. Originally five weeks (50 hours); extended on 2026-11-18 to fourteen weeks, Nov 9, 2026 to Feb 14, 2027 (140 hours maximum), when the owner moved the M6 date.
- **Project budget for this plan:** $0 (owner decision, 2026-11-18; OQ-09). Do not incur a new recurring or one-time cost, including a plan upgrade, paid add-on, domain or paid tier of any service. If any work turns out to need a cost, stop and return to the owner and board first.
- **Skill level:** beginner. Base estimates include ordinary learning, setup, and manual verification time; they are still rough estimates.
- **Buffer rule:** each committed estimate below adds a 50% contingency to the base estimate. The buffer is explicit and is not additional feature scope.

| M0/M1 milestone | Base estimate | 50% buffer | Planned total |
| --- | ---: | ---: | ---: |
| M0 — production shell | 4 h | 2 h | 6 h |
| M1 — fake-data flow and demo | 8 h | 4 h | 12 h |
| **M0 + M1** | **12 h** | **6 h** | **18 h** |

Original envelope (superseded 2026-11-18): to reach M6 within 50 hours, **no more than 32 hours including the 50% buffer** remained for M2-M6, rework, and release acceptance. That is a hard feasibility envelope, not an estimate that the remaining v1 scope fits. Reserve time for decisions and estimation inside the same 50-hour cap; do not silently count owner decision time as extra capacity.

### M2–M6 re-estimate after the approach change (draft, 2026-11-18, not approved)

The T-011 estimates below assumed a Google Apps Script web app. The owner replaced that approach the same day (section 6), so those estimates no longer apply. Claude drafted new base estimates task by task in BACKLOG.md for Google Forms, Google Sheets formulas, Gmail and the AI agent, at a beginner's pace. Building the form and formulas is less work than writing an application; the agent's runbook, connection checks and approval logging are new work. **These are drafts for the owner to approve.**

| Milestone | Tasks | Base estimate | 50% buffer | Planned total | Of which provisional (base) |
| --- | --- | ---: | ---: | ---: | ---: |
| M2 — agent access, schedule and sign-up core | T-047a, T-047b, T-048, T-012–T-015, T-042, T-043 | 14.5 h | 7.25 h | 21.75 h | 1 h |
| M3 — protected volunteer records | T-016–T-020, T-038, T-040, T-041 | 9.5 h | 4.75 h | 14.25 h | 2.5 h |
| M4 — agent email, withdrawals and promotion | T-022–T-026, T-039, T-044, T-046, T-049–T-051 | 17 h | 8.5 h | 25.5 h | 6 h |
| M5 — finance and volunteer preparation | T-027–T-033 | 10 h | 5 h | 15 h | 7.5 h |
| M6 — acceptance and release | T-034–T-037, T-045 | 9 h | 4.5 h | 13.5 h | 0 h |
| Squarespace entry point | T-007, T-008 | 1 h | 0.5 h | 1.5 h | 0 h |
| **M2–M6 total** | 42 tasks | **61 h** | **30.5 h** | **91.5 h** | **17 h** |

At 10 hours/week from week 3 (Nov 23), 91.5 buffered hours end early in week 12 (Jan 25–31, 2027), leaving about 28.5 hours of slack before the February 14, 2027 target, which is unchanged. The forecast still depends on OQ-17: if the agent cannot reach Gmail or the workbook as needed, the email and withdrawal work changes and must be re-estimated.

### M2–M6 estimate and feasibility verdict (T-011, 2026-11-18; superseded the same day)

Base estimates were drafted by Claude and **approved by the project owner on 2026-11-18**, task by task in BACKLOG.md, using the approved Google Apps Script and Google Sheets approach (section 6) and a beginner's pace, including first-time Apps Script setup, learning and manual checks. **Provisional** hours assume a simple answer to an open question (OQ-01, OQ-03–OQ-08, OQ-12) and must be re-estimated once that question is answered. Recording tasks count only the project's writing time, not the owner's or board's time to decide.

| Milestone | Tasks | Base estimate | 50% buffer | Planned total | Of which provisional (base) |
| --- | --- | ---: | ---: | ---: | ---: |
| M2 — schedule and sign-up core | T-012–T-015, T-042, T-043 | 18 h | 9 h | 27 h | 1.5 h |
| M3 — protected volunteer records | T-016–T-021, T-038, T-040, T-041 | 15.5 h | 7.75 h | 23.25 h | 4.5 h |
| M4 — email, withdrawals and promotion | T-022–T-026, T-039, T-044, T-046 | 16.5 h | 8.25 h | 24.75 h | 6 h |
| M5 — finance and volunteer preparation | T-027–T-033 | 13.5 h | 6.75 h | 20.25 h | 10 h |
| M6 — acceptance and release | T-034–T-037, T-045 | 9.5 h | 4.75 h | 14.25 h | 0 h |
| Squarespace entry point | T-007, T-008 | 1 h | 0.5 h | 1.5 h | 0 h |
| **M2–M6 total** | 37 tasks | **74 h** | **37 h** | **111 h** | **22 h** |
| T-011 (this estimate) | — | 2 h | 1 h | 3 h | — |

**Verdict: M6 by the end of week 5 is infeasible at 10 hours/week.** The buffered remaining work (111 h, or 114 h including T-011) is about 3.5 times the 32-hour envelope. The result doesn't depend on the provisional figures: without them the work is 52 h base, 78 h buffered, still well over 32 h. At 10 hours/week, M2–M6 as estimated is about 11 weeks of work.

What does fit: M2 alone (27 h buffered) fits inside the envelope.

**Caveats.** (1) The envelope assumes M0 and M1 used their planned 18 hours. No actual hours have been reported in WORK-LOG.md, so the real figure is unknown. (2) This checkpoint was due at the end of week 1 (Nov 15) and is recorded in week 2. (3) The Zeffy-to-Sheets connection (T-030) has not been shown to be possible at $0. If it isn't, FR-08 needs an owner decision, not more hours.

**Owner decision, 2026-11-18: move the M6 date.** Weekly capacity stays at 10 hours and v1 scope is unchanged. Starting M2 in week 3 (Nov 23), the 111 buffered hours need weeks 3–14, so the new M6 target is the end of week 14, **February 14, 2027**. Weeks 3–14 give 120 hours, leaving 9 hours of slack (about 8%) beyond the 50% buffer. That slack is not enough to absorb a missed week: holidays and other weeks below 10 hours aren't planned for, so each lost week moves M6 by about a week. Re-check the forecast at the end of each milestone against reported hours.

## 4. Milestones and sequence

Every milestone has a result that can be shown in under one minute. The target is to complete M0-M6 by the end of week 14 (February 14, 2027), with M0/M1 as the first production-hosted prototype and M2-M6 conditional on early decisions, estimates, and the feasibility checkpoint. Milestone sequencing does not waive any gate.

| Milestone | Scope and dependencies | Demo outcome (under one minute) | Exit criteria / traceability |
| --- | --- | --- | --- |
| **M0 — Live entry shell** | Verify GitHub Pages access and the production URL; create the minimal public shell; deploy it. Preserve the existing SPUR landing page by proposing a separate `/kitchen/` path under the existing Pages site. | Open the production URL on a phone or desktop and show the Brooklyn Community Kitchen entry shell with no operational data or live signup. | Production URL loads on desktop and phone; deployment result and exact URL recorded; no real data exposed. Backlog T-002–T-004; infrastructure and FR-17 route prerequisite. **This deployment is mandatory, even though the page is otherwise empty.** |
| **M1 — Fake-data signup prototype** | Add only the task-choice and status states using clearly fictional, prepared examples. No persistence or integrations. Depends on M0. | In one short walkthrough, choose an available task, show a full task placing a sample request on the waitlist, then show a second task request in the same week rejected. | All three states are reproducible; the rule that a volunteer may request only one task per week is clear; no submission reaches a live system. Capture owner feedback and unresolved decisions. Backlog T-005; T-008's formal integrated walkthrough remains blocked until the approved Squarespace route is available. US-02 prototype only, not acceptance of FR-03/FR-04 for production. |
| **M2 — Agent access, schedule and signup core (gated; target weeks 3–5)** | Decide and verify the agent's accounts and connections (OQ-17), check free limits, then build the operator workbook's schedule tab, the public Google Form and the status formulas (cap, waitlist order, one request per week, deadline). | Show a fictional week: two responses fill a block's cap and the next one shows as waitlisted; a second response from the same email shows as a rejected duplicate. | FR-02–FR-04, FR-12, FR-13, FR-15 and US-02/US-07; OQ-17 first (T-047, T-048, T-012–T-015, T-042, T-043). |
| **M3 — Protected volunteer records (gated; target weeks 5–6)** | Share the workbook only with operators, make the existing master spreadsheet operational as the master profile tab, and add the operator-only on-file match. | Show an operator updating a fictional volunteer row, then show that a visitor using the form link cannot see any stored data. | FR-01, FR-15, FR-16 and US-01; OQ-07 (including the agent handling personal data), OQ-08, T-018 and the public-profile risk review first (T-016–T-020, T-038, T-040–T-041). |
| **M4 — Agent email, withdrawals, and promotion (gated; target weeks 6–9)** | Write the agent's weekly runbook, set up scheduled runs, and have the agent send the Tuesday and Friday emails on schedule, send waitlist notices and promotion emails, process withdrawals, and log everything. | Show a scheduled run sending a fictional Friday batch to test addresses and the email log showing it sent; then a fictional waitlisted response getting its notice and a withdrawal promoting the next request. | FR-05–FR-07, FR-14, FR-18, FR-19 and US-02/US-03; OQ-05, OQ-06, OQ-12, OQ-17, OQ-21 first (T-022–T-026, T-039, T-044, T-046, T-049–T-051). |
| **M5 — Finance and approved volunteer preparation (gated; target weeks 9–10)** | The agent records Zeffy donations; operators enter expenses; report tabs calculate spending and budget. Resolve the onboarding conflict before claiming US-05. | Show one fictional donation recorded by the agent, one categorized expense, and the resulting example report. | FR-08–FR-11 and US-04–US-06; OQ-01–OQ-03 and the US-05/FR-11 inconsistency first (T-027–T-033). |
| **M6 — Integrated v1 acceptance and release (gated; target weeks 10–12, by Feb 14, 2027 at the latest)** | Run the approved end-to-end weekly walkthrough, including a missed agent run and the manual fallback, plus the device, privacy and access checks; then start the approved v1. | Demonstrate the owner-approved weekly workflow from the Squarespace link to the Friday confirmation using approved test data. | All approved Must-story acceptance and definition-of-done checks; OQ-07–OQ-13, OQ-15–OQ-17 and remaining gates (T-034–T-037, T-045). |

The Squarespace entry point is not a prerequisite for M0's direct production URL. It remains required for the approved public operational flow before FR-17 can be accepted; do not make an unapproved website edit to make an M0 demo appear complete.

## 5. Target schedule (M6 date moved 2026-11-18)

Weeks 1–2 are as originally planned. From week 3 the schedule follows the draft re-estimate after the approach change (section 3) at 10 hours per week, one milestone after another; a milestone may finish early in the same week the next one starts. The November 21 date remains the M0/M1 demo production release target. Weekly numbers are ceilings, not work that must be filled with new scope.

| Week | Capacity | Planned work |
| --- | ---: | --- |
| 1 — Nov 9–15 | Up to 10 h | Resolve required owner decisions/access first; complete M0 (6 h including buffer), start M1, and decompose/re-estimate M2-M6. |
| 2 — Nov 16–22 | Up to 10 h | Finish M1 (12 h total including buffer across weeks 1–2); demonstrate by Nov 21. Owner decisions (T-010) and the feasibility checkpoint (T-011, 3 h). |
| 3–5 — Nov 23–Dec 13 | 10 h/week | M2: agent access, schedule and sign-up core (21.75 h, draft). |
| 5–6 — Dec 7–Dec 20 | 10 h/week | M3: protected volunteer records (14.25 h, draft). |
| 6–9 — Dec 14–Jan 10 | 10 h/week | M4: agent email, withdrawals and promotion (25.5 h, draft). |
| 9–10 — Jan 4–17 | 10 h/week | M5: finance and volunteer preparation (15 h, draft). |
| 10–12 — Jan 11–31, 2027 | 10 h/week | M6: acceptance and release (13.5 h) plus the Squarespace link and walkthrough (1.5 h), draft. |
| 12–14 — Jan 25–Feb 14, 2027 | 10 h/week | Slack (about 28.5 h) for open-question rework and lost weeks. **M6 target: Feb 14, 2027 (unchanged).** |

This sequencing has little slack (9 hours across weeks 3–14). M3-M5 may overlap only where their approved dependencies permit; do not parallelize work in a way that bypasses review, data-access controls, or testing. If a decision remains open when its milestone begins, stop that affected implementation, record the blocker, and use the week-1 checkpoint or revised forecast rather than substituting an unapproved behavior. If GitHub Pages access or production deployment is blocked, escalate immediately; M0 is not complete until the production URL works.

## 6. Technical decisions

**On 2026-11-13 the owner approved the M0/M1 rows** (M0 hosting and route, M0 page, M1 interaction, and no production data or services in M0/M1). **On 2026-11-18 the owner decided the v1 budget, platform, spreadsheet service, application approach and payment system** (resolving OQ-09 and OQ-15). The choices under "Still deferred" remain unapproved.

| Decision | Decision and reason | Alternatives rejected for this plan |
| --- | --- | --- |
| M0 hosting and route | Use the repository's existing GitHub Pages `/docs` publishing path, with a `/kitchen/` subpath if the Pages configuration supports it. The repository already has a static `docs/` site; reusing it avoids a new account, vendor, and expected hosting charge, and a subpath preserves the existing SPUR landing page. Verify repository Pages settings and the exact production URL before treating this as available. | Replacing the existing root page risks breaking the current SPUR landing page. A new hosting vendor or paid host adds account/cost/setup without helping the static M0 requirement. A local-only demo fails the production-URL requirement. |
| M0 page | A minimal static page, with no form submission or operational data, is sufficient to prove the production route. | A database, server, or live form is unnecessary for an empty entry shell and adds risk and setup. |
| M1 interaction | For owner review, propose plain HTML/CSS and a small amount of browser JavaScript with hard-coded fictional examples; keep state in the page only. This matches the existing static site and minimizes dependencies for a beginner. It is a prototype choice, not a commitment to the v1 application stack. | A framework, build pipeline, backend, or external form service adds learning/setup and is not required for the three fake-data states. Real Sheets/email integration violates M1's scope and its unresolved privacy/access gates. |
| Production data and services | Use no real personal/financial data and add no service, account, API, or recurring cost in M0/M1. | Connecting Google Workspace, payment, or email services before requirements, permissions, privacy, and cost are approved is rejected. |
| v1 project budget | **Owner decision, 2026-11-18 (OQ-09, T-010):** the project budget is $0. No paid service, plan upgrade, paid add-on, domain or paid tier is used. If any v1 work turns out to need a cost, work stops and returns to the owner and board. | The earlier working cap below $300: replaced by the $0 decision. The nonprofit's approximately $30,000 in funds: not the project budget. |
| v1 platform | **Owner decision, 2026-11-18, revised the same day:** Google Forms, Google Sheets and Gmail on free Google accounts, with **no paid Google Workspace subscription** and no other Google Workspace tools. The only other exceptions are the Squarespace link and Zeffy (below), and the AI agent (below). | A paid Google Workspace subscription: not wanted. Other vendors or hosting platforms (for example a separate database, server host or email provider): outside the owner's decision. |
| v1 spreadsheet and data store | **Owner decision, 2026-11-18 (OQ-15, T-010):** Google Sheets holds the master volunteer spreadsheet and the system's operational records, in one operator-only workbook. Still open: who owns the existing master spreadsheet and how operators and the helper get access (T-018), and the privacy and retention rules (OQ-07). | Other spreadsheet services or a separate database: outside the owner's decision. |
| v1 application approach | **Owner decision, 2026-11-18, replacing the Apps Script decision made earlier that day:** no custom application. (1) The public sign-up is a Google Form linked to the operator workbook; volunteers need no Google account. (2) The rules that must always hold (block caps, waitlist order, one request per week, the Thursday 6:00 p.m. Eastern deadline) are spreadsheet formulas over the form's timestamps, so they hold whether or not the agent is running. (3) Gmail sends volunteer email and receives withdrawal requests. (4) The AI agent does the rest (row below). (5) The GitHub Pages `/kitchen/` demo stays until the owner decides otherwise; the Squarespace link (T-007) points to the Google Form. | Google Apps Script web app (decided and then replaced on 2026-11-18): the owner chose not to use Apps Script for now. AppSheet: no-cost inclusion depends on the Workspace edition. A separate host or database: outside the owner's decision. |
| AI agent | **Owner decisions, 2026-11-18:** the AI agent (Claude) is part of v1 and does the automation: opening and closing the form, sending the weekly emails, sending waitlist notices and promotion emails, processing withdrawal emails, recording Zeffy donations, and logging each run. It runs on the owner's own Claude account; the form and workbook are in a Google Drive folder the owner owns, shared with the kitchen's Google account; the repository is shared with the board. **Sending:** the Tuesday signup email and Friday confirmations go out on scheduled runs without operator approval; the agent holds a batch and flags it if something doesn't match (SPECIFICATION.md §1.1). Waitlist notices also need no approval. Promotions and other one-off emails need approval until OQ-21 is decided. Volunteer email goes from the kitchen's Gmail account; scheduled runs happen in the cloud, so no computer has to stay on; the Claude subscription does not count against the project budget. The agent changes master profiles only on an operator's instruction. Not yet verified (T-047, T-050): what the Gmail and Google Drive connections can do, and how often the cloud runs happen. Handing the agent over to the board is a later goal (BACKLOG.md `Later`). | Approval of every weekly batch by an operator: the owner chose not to require it. Apps Script triggers for unattended sending: Apps Script is not being used. |
| One standing sign-up form (proposal, not approved) | Use one Google Form for every week rather than a new form each week; the week is worked out from each response's timestamp, and the form is opened on Tuesday and closed at Thursday 6:00 p.m. Eastern. The Squarespace link and the link in each Tuesday email then never change. | A new form each week: the Squarespace link would need editing every week by a board member. |
| Operator access (proposal for OQ-08, not approved) | Share the operator workbook, and the kitchen Gmail if needed, only with each operator's Google account; add or remove an operator by changing the sharing. No public or link sharing. | A separate sign-in system: there is no custom application to put it in. |
| v1 donation payment system | **Owner decision, 2026-11-18 (T-010, T-027):** donations come through Zeffy. Still open: the donor fields to store and whether board-entered donations are also recorded (OQ-01), and how Zeffy donations reach Google Sheets automatically (FR-08). Any connection method must cost $0 and is not yet verified. | Other payment providers: not chosen by the owner. |
| Still deferred | Operator access and account management (OQ-08, T-016; proposal above), approval for one-off emails (OQ-21), withdrawal inbox (OQ-05), email content (OQ-06), and failure and retry behaviour (OQ-12). Record each approved choice here with its rationale and rejected alternatives once its open question is resolved. | Choosing these now would contradict the specification's open questions. |
| Squarespace integration | **Owner decision, 2026-11-16 (OQ-16, T-006):** the volunteer sign-up entry point is a link or button on the Squarespace site's existing volunteer page, opening the sign-up page at its own address. A board member with existing Squarespace access makes the change. Cost is $0 only; if a plan upgrade or paid add-on is needed, stop and return to the board. The link is added only once the production sign-up flow exists (T-007); demo the direct Pages URL meanwhile. | Embedding the form in a Squarespace page: embedded code is limited on some Squarespace plans and would need the plan checked first. A main-navigation item: not chosen. Giving a project contributor Squarespace access: not needed when a board member makes the change. |

## 7. Quality and release checks

- For M0, open the deployed URL directly (not just a local preview) on desktop and phone. Confirm the page contains no real volunteer or operational data.
- For M1, use fictional examples only. Rehearse all three states from a clean page load and confirm no form submission, persistence, or network integration is implied.
- Keep each demo under one minute: one outcome, prepared data, and no setup steps during the demo.
- Record the production URL, verification date, browser/device used, owner feedback, and blockers in the project work log/backlog.
- Do not claim accessibility, privacy, security, or production-readiness acceptance beyond the checks actually completed. Final device/browser and accessibility acceptance remains gated on OQ-13.
- Never commit credentials or secrets.

## 8. Risks and decision gates

| Risk / open decision | Effect | Gate / response |
| --- | --- | --- |
| GitHub Pages is not enabled or the production URL is unknown. | Could prevent M0's mandatory production deployment. | Verify immediately with the repository maintainer. Do not mark M0 done without a working production URL or switch hosts without approval. |
| The current `/docs` landing page is for SPUR AI Research. | Replacing it could damage an existing public page. | Proposed separate `/kitchen/` route; confirm Pages configuration and preserve the root page. |
| Squarespace location, method, access, and cost were decided on 2026-11-16 (OQ-16), but the link is not yet added and the exact page and board member are not recorded. | FR-17 acceptance cannot be claimed until the link exists and is walked through. | M0/M1 demo directly at the deployed URL; T-007 waits for the production sign-up flow; confirm the page and editor before T-007 starts. |
| The Nov 21 demo production release could be mistaken for the full v1. | Stakeholders may expect real sign-ups or data on that date. | Nov 21 covers M0/M1 only (fake data, no live submissions), as the concept and specification now state; label the demo clearly as a demo. |
| Onboarding language conflicts. | US-05 is Must, while FR-11 describes a compliance link without a completion workflow and the readiness section says US-05 is not yet satisfied. | Resolve OQ-02 and update the approved acceptance criteria before M5 or any v1 completion claim. |
| The budget is $0 (decided 2026-11-18) and v1 runs on free Google Forms, Sheets and Gmail, Zeffy, and the AI agent on the owner's own Claude account (outside the project budget). | Free Gmail has daily sending limits that could block a Tuesday send to the whole volunteer list; Zeffy donations may not reach the agent for free. None is verified yet. | Check before the milestone that needs it (T-048 before M2 build work; Zeffy at T-027). If a requirement can't fit, stop and return to the owner; don't pay for more. |
| **T-047a results, 2026-11-20 (test run on the owner's NYU school account, fictional data only).** All three connections (Google Drive, Google Sheets, Gmail) were signed in as the school account. In a new test folder ("BCK agent test - fictional data only (T-047a)" in the owner's My Drive): **Drive** created a folder, a spreadsheet and a blank form. **Sheets** added tabs, set the time zone to `America/New_York`, wrote values and formulas, and read back calculated results. Status formulas over fictional responses, with test caps of 2 and 1, gave the expected results: active up to the cap, then waitlisted; a second response from the same email in the same week (different case and spaces) marked a rejected duplicate; a response after Thursday 6:00 p.m. marked late; and a withdrawal row promoted the first waitlisted response straight away, with the summary counts matching. **Gmail** sent one fictional test email to the owner's two test addresses in BCC and confirmed it in sent mail; it also created a draft and listed inbox metadata. **Not possible with these connectors:** adding questions to a form, changing its settings, opening or closing it, reading its questions, or linking it to a sheet (there is no Google Forms connector); and scheduling a send in Gmail (the Gmail connector sends immediately or makes a draft). The owner confirmed both test emails arrived in the correct inboxes. **Cloud scheduled run, 2026-11-20:** a one-time cloud routine ("BCK T-047 cloud connector test", set for 20:05 UTC; it started at 20:06 UTC and took 25 seconds) had the Google Sheets, Google Drive and Gmail connectors attached automatically from the owner's account. It added a 'Run log' tab and wrote and read back a row, read the Summary tab, read the test folder's details in Drive, and sent one test email BCC to the two test addresses. Claude confirmed the row in the workbook and the email in sent mail independently. Lessons: the run wrote 'succeeded' for the send into the email body before the send had returned, so the runbook must record a send's result only after the call returns (FR-18); and a run can start about a minute after its set time. The owner confirmed the cloud-run email arrived in both inboxes, and reported that the existing Saturday Shift Claim Form can be filled in by people outside NYU. **Not tested:** cloud runs on the kitchen's account (T-047b). Existing files were inspected for structure only: the "Volunteer Sign-Up (Responses)" sheet has one tab with 13 columns (timestamp, first and last name, email, phone, prior volunteering, Saturday availability, work types, lifting, how they heard, future updates, two approval columns) and time zone `America/Detroit`; no response rows were read. No response sheet named for the "Saturday Shift Claim Form" was found, and its questions could not be read. | Form building, its settings (no sign-in, no response summary) and opening and closing it stay manual for an operator; the Thursday deadline still holds because the formula marks late responses. Weekly emails cannot be pre-scheduled in Gmail, so they depend on a cloud run at the send time. | T-013 and T-047b: an operator builds and opens and closes the form by hand, recorded in the runbook (T-049); T-050 sets cloud runs at the Tuesday and Friday send times and T-047b confirms the cloud runs can reach the connections. |
| **T-047 attempt, 2026-11-18: blocked.** The owner does not yet have access to the kitchen's Google account. A Google Drive connection made that day was signed in to the owner's school (NYU) Google account. Claude only listed file names and the kitchen folder's sharing: the folder is owned by that school account and shared with three classmates' school accounts, not with the kitchen's account; existing kitchen forms and response sheets are there, some owned by classmates. No file contents were read and nothing was created or changed. | A system built in a school account depends on that account staying open and on the school's sharing rules, and the kitchen would not own its data. | Reconnect Gmail, Google Drive and Google Sheets with the kitchen's account once the owner has access, then run T-047. Decide with the owner whether the workbook and form are created in the kitchen's account rather than the school folder, and whether any existing forms or response sheets are reused (they may hold real volunteer data, so not before OQ-07). |
| The agent's Gmail and Google Drive connections are not set up, and what they can do (send, schedule, edit Sheets, open and close a form) is unverified. | If the agent can only create drafts, operators must press send; if it can't edit the form, operators open and close it by hand. | T-047 verifies each ability with fictional data before M2 build work; the runbook records which steps are manual. |
| The agent is not always running, and the weekly emails go out without an operator checking them. | A missed run means a weekly email goes out late or not at all; a wrong recipient list or wording would reach every volunteer. | Show overdue runs and held batches on the summary tab (FR-18); the agent holds a batch when the wording, schedule, form or recipient list doesn't match; test each weekly email with fictional addresses first (T-047, T-049); keep a manual runbook. |
| Volunteer, donor and financial data would pass through the AI provider. | The board may not accept this for real data. | Part of OQ-07 (T-017); the agent uses fictional data only until it is approved. The repository is shared with the board, so it must never hold volunteer, donor or financial data or any key. |
| Remaining v1 estimates are drafts, 22 h of them provisional, and the moved schedule has 9 h of slack. | Open questions, holidays or weeks below 10 hours could push M6 past Feb 14, 2027. | Re-estimate provisional tasks as each open question is answered; compare reported hours with the plan at the end of each milestone; if the forecast passes Feb 14, 2027, return to the owner for a date, capacity or scope decision. Do not claim readiness based on a guess. |

## 9. Ordered cut list if time runs out

Cut or defer work in this order; do not remove the required M0 production deployment or the M1 core demo states to make the schedule look complete:

1. Decorative branding, animation, and visual polish beyond a clear, readable, mobile-usable shell.
2. Additional prototype scenarios or sample data beyond task choice, full-task waitlist, and second-task rejection.
3. Squarespace link/embed work from the current M6 target if OQ-16, access, or cost is still unresolved; keep the direct production URL available and leave integration visibly blocked, not silently dropped from v1.
4. If the buffered M2-M6 forecast no longer fits before the M6 target (Feb 14, 2027 since 2026-11-18), move the M6 date or seek an owner-approved increase in capacity/budget. Do not silently cut a Must story, bypass a gate, or label a partial build as v1; any v1 scope reduction requires an approved specification and backlog change.

If the M0 deployment itself is blocked, record the blocker and seek an approved zero-cost way to complete the production deployment. Do not report the milestone as complete or substitute an unapproved service.

## 10. Review and approval

- [x] Concept approved by the project owner.
- [x] Specification v0.2.1 approved for planning; v0.2.2 applies owner-directed corrections (2026-11-13). The owner approved the v0.2.2 specification document on 2026-11-13. Implementation readiness remains open.
- [x] M0/M1 scope approved by the project owner on 2026-11-03.
- [x] M0/M1 technical proposals in section 6 approved by the project owner on 2026-11-13 (`/kitchen/` route under `docs/` on GitHub Pages, a static page, plain HTML/CSS/JS with fictional data, no real data or services). This does not approve the later v1 architecture.
- [x] This plan approved by the project owner on 2026-11-13. The backlog was approved the same day.
- [x] Production URL and GitHub Pages configuration verified on 2026-11-13: Pages publishes from `main`, `/docs` (checked through the GitHub API); the owner confirmed the `/kitchen/` URL loads on a real desktop and phone. See section 11.
- [x] OQ-16 resolved for volunteer sign-up by the project owner on 2026-11-16 (section 6). No Squarespace change has been made.
- [x] OQ-09 and OQ-15 resolved by the project owner on 2026-11-18 (section 6): $0 budget, Google Workspace for the entire system, Google Sheets for the spreadsheets.
- [x] v1 application approach (Google Apps Script) and donation payment system (Zeffy) decided by the project owner on 2026-11-18 (section 6). T-010 done. The owner replaced Apps Script with Google Forms, Sheets, Gmail and the AI agent later the same day (next item).
- [x] M2–M6 buffered estimates (T-011) and the moved M6 target (Feb 14, 2027) approved by the project owner on 2026-11-18. V1 scope is unchanged.
- [ ] The 2026-11-18 approach change (Google Forms, Sheets, Gmail and the AI agent; no Apps Script, no paid Workspace) reviewed by the owner: SPECIFICATION.md v0.3.2, the draft re-estimate in section 3 and the new backlog tasks.
- [ ] Remaining open questions decided before the tasks that depend on them start. Provisional (`p`) estimates are re-estimated when their question is answered.

**Current verdict:** `Approved by the project owner on 2026-11-13. Feasibility checkpoint (T-011, 2026-11-18): M6 by week 5 was infeasible at 10 hours/week (111 h buffered vs a 32-hour envelope). The owner moved the M6 target to the end of week 14, February 14, 2027, with the same weekly capacity and scope (section 5). The owner approved the estimates the same day.`

## 11. Environments

| Environment | URL | Source | Status |
| --- | --- | --- | --- |
| Production (GitHub Pages) — Brooklyn Community Kitchen entry shell | <https://andrewmiaao.github.io/SPUR-AI-Research/kitchen/> | `main` branch, `docs/kitchen/` | Returned HTTP 200 on 2026-11-13 (automated request). Owner confirmed on 2026-11-13 that it loads on a real desktop and phone; Google Chrome on desktop and Safari on phone, readable without horizontal scrolling (details in WORK-LOG.md). M0 complete. |
| Production (GitHub Pages) — existing SPUR landing page | <https://andrewmiaao.github.io/SPUR-AI-Research/> | `main` branch, `docs/` | Returned HTTP 200 on 2026-11-13; unchanged. |

GitHub Pages publishes from the `main` branch, `/docs` folder (legacy branch build, HTTPS enforced). There is no staging environment; local preview is opening the files under `docs/` directly.
