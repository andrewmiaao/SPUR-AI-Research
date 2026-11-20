# BACKLOG: Brooklyn Community Kitchen AI Assistant

> **Purpose of this document:** the living, ordered list of work. One line per item,
> small enough to finish in a sitting, traceable back to the specification.
> **Input:** `SPECIFICATION.md` (what) + `PLAN.md` (order).
> **Rule:** the top of `Now` is always the next thing you pick up.

**Status:** Approved by the project owner on 2026-11-13 (generated 2026-11-13 from SPECIFICATION.md v0.2.2 and PLAN.md). Approval does not unblock any task: `Blocked by` entries and `U` estimates stand until their blockers are resolved.

**How to read it**

- **Ref** is the specification ID the task serves (US-xx / FR-xx), or `Infra` for infrastructure and project-gate work.
- **Est.** is base effort in hours, before the plan's 50% buffer. `U` means unestimated: the task cannot be sized until its blocker is resolved. `p` means provisional: the estimate assumes a simple answer to an open question and must be re-estimated when that question is answered. The M2–M6 estimates were drafted by Claude (T-011) and approved by the owner on 2026-11-18, then re-drafted the same day for the new approach and await approval.
- **Blocked by** names the open question (OQ-xx, SPECIFICATION.md §12) or task that must be closed first. A blocked task must not be started by guessing the answer.
- Task IDs match the references in PLAN.md §4. IDs are not in strict numeric order; the order of the rows is the priority.

---

## Now (M0 and M1: demo production release, target 2026-11-21)

Base estimate remaining: M0 0 h (complete 2026-11-13), M1 0 h (all tasks done 2026-11-16). Fictional data only. No persistence, no form submission, no external service, no cost.

| # | ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | --- | ---: | --- |

No M0 or M1 task remains. The planning gate is done (T-010, T-011). The owner moved the M6 target to February 14, 2027 (PLAN.md §5). Later on 2026-11-18 the owner replaced the Apps Script approach with Google Forms, Sheets, Gmail and the AI agent; M2 now starts with T-047a and T-047b (connecting and verifying the agent's Gmail and Google Drive access) and T-048 (free limits), and the re-planned tasks and estimates below await owner approval.

### Acceptance criteria

**T-002**
- **Given** the repository's Pages settings, **when** they are checked, **then** the source (branch and `/docs` folder) and the production URL are written in PLAN.md §10.
- **Given** Pages is not enabled or the URL does not load, **when** this is found, **then** the blocker is recorded and raised with the owner, and no other host is used without approval.

**T-003**
- **Given** the repository, **when** `docs/kitchen/index.html` is opened locally, **then** it shows the Brooklyn Community Kitchen name and a short statement that the volunteer tools are coming, with no form, no real names and no operational data.
- **Given** the change, **when** `docs/index.html` is compared with the previous commit, **then** it is unchanged.

**T-004**
- **Given** the shell is pushed, **when** the production `/kitchen/` URL is opened on a desktop browser and on a phone, **then** the page loads and is readable on both without horizontal scrolling.
- **Given** the deployment, **when** the site root URL is opened, **then** the existing SPUR landing page still loads.
- **Given** verification is finished, **when** WORK-LOG.md is read, **then** it shows the exact URL, the date, and the browser and device used.

**T-005a**
- **Given** a clean page load, **when** the page appears, **then** it shows a fictional week with the 7:30 a.m. and 11:00 a.m. shift blocks, each marked as having space or full, and a visible label that this is a demo with sample data.
- **Given** a shift block with space, **when** the visitor chooses it, **then** the page shows the request as active for that block.

**T-005b**
- **Given** a shift block whose fictional places are all taken, **when** the visitor chooses it, **then** the page shows the request as waitlisted, and the number of active places shown for that block does not go above its cap.

**T-005c**
- **Given** the visitor already has an active or waitlisted request in the demo week, **when** they choose another shift block, **then** no second request is created and the page says they are already signed up for the first one.
- **Given** the page is reloaded, **when** it appears, **then** the demo starts again with no saved request.

**T-005d**
- **Given** the deployed prototype, **when** the three states are run from a clean page load on desktop and on phone, **then** each state appears as described in T-005a to T-005c.
- **Given** the browser's network panel is open, **when** the three states are run, **then** no request is sent after the page's own files have loaded.
- **Given** the page source, **when** it is searched, **then** it contains no real volunteer name, email address or phone number.

**T-009**
- **Given** the deployed prototype, **when** the owner is shown the three states at the production URL, **then** the walkthrough takes under one minute with no setup steps.
- **Given** the walkthrough is over, **when** WORK-LOG.md is read, **then** it lists the owner's feedback, any blockers and any decisions, and new ideas have been added under `Later`.

---

## Next (M2 to M6: gated; re-planned 2026-11-18 for Google Forms, Sheets, Gmail and the AI agent)

On 2026-11-18 the owner replaced the Google Apps Script approach with Google Forms, Google Sheets and Gmail, no paid Google Workspace subscription, and the AI agent doing the automation (PLAN.md §6, SPECIFICATION.md v0.3.2). The tasks below are re-scoped for that approach. **The estimates are new drafts by Claude, awaiting owner approval:** 61 h base, 91.5 h with the 50% buffer (PLAN.md §3). The T-011 estimates approved earlier that day assumed Apps Script and no longer apply. Estimates are not approval: nothing below is authorized by the M0/M1 approval, and `Blocked by` entries still stand. Tasks marked *new* did not exist before; tasks marked *re-scoped* keep their ID with a changed description.

### Squarespace entry point

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-007 | Add the approved entry point to the Squarespace site, pointing at the production Google Form. *Re-scoped.* | FR-17 | 0.5 | T-013, T-014 |
| T-008 | Walk through the sign-up flow starting from the Squarespace site and record the result. | FR-17, US-02 | 0.5 | T-007 |

### M2: agent access, schedule and sign-up core

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-047a | Test run on the owner's NYU school Google account, where the existing kitchen forms and sheets were built (owner decision, 2026-11-20, replacing the personal-Gmail choice): connect Gmail, Google Drive and Google Sheets with that account and check what the agent can do with fictional data only, sending only to test addresses the owner controls: create and edit a workbook (values and formulas), create a form and open and close it, read the inbox, send, and schedule. Existing forms and response sheets are inspected for structure only; their responses are not read unless the owner confirms they hold no real volunteer data (real data waits for OQ-07), and files owned by classmates are not changed. Record the results, and any school-account restriction that would not apply to the kitchen's account, in PLAN.md §8. Does not complete T-047. **Run 2026-11-20:** Drive, Sheets and Gmail checks and a one-time cloud scheduled run all passed; form editing and Gmail scheduled send are not available through the connectors; the owner reported the existing form can be filled in from outside NYU (PLAN.md §8). *New.* | Infra | 1.5 | Owner connects the school account and gives test addresses |
| T-047b | Repeat the T-047a checks on the kitchen's Google account (the system's real home: kitchen's Gmail, Drive and Sheets), including for cloud scheduled runs. T-047 is done only when this passes. OQ-17 decided 2026-11-18. *New.* | Infra | 1 | Access to the kitchen's Google account; T-047a |
| T-048 | Check the free limits that matter on the kitchen's account (Gmail daily sending limit against the volunteer list size, and any Forms or Sheets limit) and record the result with sources in PLAN.md §8. *New.* | Infra | 1 | T-047b |
| T-012 | Create the operator workbook with a schedule tab where operators enter a week's task names, start and end times, and caps, and reopen it with the saved values. *Re-scoped.* | FR-02, US-07 | 2 | T-047b |
| T-042 | Record the owner's decision on cap reductions below the active count, then make the formulas and the agent follow that rule. | FR-02 | 1 p | OQ-04, T-012 |
| T-013 | Create the public Google Form (two shift blocks; name, email, phone, shift preferences; no sign-in; no response summary; no editing after submitting) linked to a responses tab; operators or the agent open and close it, and a closed form shows only its closed message. Absorbs T-021. *Re-scoped.* | FR-13, FR-15, US-02 | 2 | T-012 |
| T-014 | Add status formulas to the responses tab: active in timestamp order up to the block cap (7 for 7:30 a.m., 9 for 11:00 a.m.; OQ-20), then waitlisted; late after Thursday 6:00 p.m. Eastern; week worked out from the timestamp. *Re-scoped.* | FR-03, US-02 | 3 | T-013 |
| T-015 | Add the duplicate formula: a later response from the same email in the same week is a rejected duplicate and counts for nothing. *Re-scoped.* | FR-04, US-02 | 1.5 | T-014 |
| T-043 | Add the summary tab: each task's time and cap, each block's cap, active and waitlist counts, errors shown as errors, and the agent's last-run time. *Re-scoped.* | FR-12, US-07 | 1.5 | T-014 |

### M3: protected volunteer records

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-016 | Record the owner's decision on operator access and how operators are added and removed (proposal: Google sharing, PLAN.md §6). | FR-01 | 0.5 p | OQ-08 |
| T-017 | Record the board's privacy, retention and deletion rules for volunteer, donor and accounting data, including whether the AI agent may handle real data, in SPECIFICATION.md. | US-01 | 1 p | OQ-07 |
| T-018 | Record who owns the existing master spreadsheet and bring it into the operator workbook as the master profile tab. | US-01 | 1 | OQ-15, T-047b |
| T-038 | Record the owner's review of the email-matching risk, the approved abuse controls and the recovery process. | FR-15 | 1 p | T-017 |
| T-019 | Share the workbook only with operators' Google accounts and confirm that a visitor and a signed-out browser cannot open it. *Re-scoped.* | FR-01 | 1 | T-016 |
| T-020 | Operators can view and edit a volunteer's name, email, phone and shift preferences in the master profile tab, directly or through the agent. *Re-scoped.* | FR-01, US-01 | 2 | T-018, T-019 |
| T-021 | *Merged into T-013 on 2026-11-18*: the Google Form collects the profile fields and stores them in the responses tab, apart from the master profile tab. | FR-15, FR-16 | — | — |
| T-040 | Add the operator-only "on file" match column to the responses tab; operators, or the agent at their instruction, copy approved changes to the master profile tab. *Re-scoped.* | FR-15, FR-16 | 2 | T-020, T-013 |
| T-041 | Verify and record that a visitor using the form cannot see any other volunteer's details, response summaries or the workbook. | FR-16 | 1 | T-019, T-013 |

### M4: agent email, withdrawals and promotion

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-022 | Record the approved wording of the Tuesday sign-up email, the Friday confirmation, the waitlist notice, the promotion email, and any duplicate or late notice. | FR-06, FR-07, FR-05, FR-19 | 0.5 p | OQ-06, OQ-21 (promotions, duplicate and late notices only) |
| T-039 | Record the internal address for withdrawal requests and how a message identifies the sign-up. | FR-14 | 0.5 p | OQ-05 |
| T-046 | Record the approved rules for failed sends, missed runs, retries and duplicate-send prevention. | FR-06, FR-07, FR-18 | 1 p | OQ-12 |
| T-049 | Write the agent's weekly runbook in the repository: what it does on Tuesday, at the Thursday close, on Friday, and on every run (withdrawals, promotions, donations); how it asks for approval; what it writes to the run log and email log; and how operators do each step by hand. *New.* | FR-18, US-03 | 3 | T-047b |
| T-050 | Set up the agent's cloud scheduled runs at the agreed US Eastern times, decide with the owner how often the in-between runs happen (waitlist notices, withdrawals), and confirm a missed run shows as overdue on the summary tab. *New.* | FR-18 | 1.5 p | T-049 |
| T-023 | On the Tuesday scheduled run the agent sends the approved sign-up email to every volunteer without showing other recipients, with the form link, at 2:30 p.m. Eastern and without operator approval; it holds and flags the batch if anything doesn't match. *Re-scoped.* | FR-06, US-03 | 2 | T-022, T-049, T-013 |
| T-024 | After the Thursday close the agent sends one Friday confirmation per active volunteer at 9:00 a.m. Eastern without operator approval; it holds and flags the batch if anything doesn't match. *Re-scoped.* | FR-07, US-03 | 1.5 | T-022, T-049, T-014 |
| T-044 | Add the email log tab: each batch's held, awaiting-approval, scheduled, sent, failed or not-sent status and each failed recipient; scheduled turns to sent only after the agent checks Gmail's sent mail. *Re-scoped.* | FR-06, FR-07, FR-19 | 1.5 | T-046, T-049 |
| T-025 | When a place opens, the formulas promote the first waitlisted request and the agent sends the promotion email (with operator approval unless OQ-21 removes it); a failed email shows as failed. *Re-scoped.* | FR-05, US-02 | 1.5 | T-014, T-022, T-049 |
| T-051 | At each run the agent sends one waitlist notice to each newly waitlisted volunteer, without operator approval, and never sends two for the same request. *New.* | FR-19, US-02 | 1.5 | T-014, T-022, T-049 |
| T-026 | The agent processes a withdrawal email from an address on file, records the withdrawal and triggers promotion; unmatched emails are flagged in the run log. *Re-scoped.* | FR-14, US-02 | 2.5 p | T-039, T-025 |

### M5: finance and volunteer preparation

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-027 | Record the owner's decision on the donor fields to store and how the agent reads Zeffy donations at $0 (for example Zeffy's notification emails or an export). Payment system decided 2026-11-18: Zeffy. | FR-08 | 2 p | OQ-01 |
| T-028 | Record the approved expense categories and fields, report and budget periods, currency, and who sets the budget. | FR-09, FR-10 | 1 p | OQ-03 |
| T-029 | Update SPECIFICATION.md so US-05 and FR-11 agree on what volunteer preparation v1 includes. | US-05, FR-11 | 0.5 | OQ-02 |
| T-030 | The agent records each new Zeffy donation in the donations tab with amount, donor name, donor email, date and reference, no operator identity, and no duplicates. *Re-scoped.* | FR-08, US-04 | 2.5 p | T-027, T-019 |
| T-031 | Add the expenses tab with the approved category list; operators enter an expense directly or through the agent. *Re-scoped.* | FR-09, US-06 | 1.5 | T-028, T-019 |
| T-032 | Add spending and budget report formulas for a period; a failed calculation shows as an error, never zero. *Re-scoped.* | FR-10, US-06 | 2 p | T-031 |
| T-033 | Include the approved compliance video link in the Tuesday sign-up email, with no completion tracking. | FR-11, US-05 | 0.5 | T-029, T-023 |

### M6: integrated acceptance and release

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-034 | Record the owner's "full operation" checklist and the supported devices, browsers and accessibility standard. | US-07 | 1 | OQ-10, OQ-13 |
| T-035 | Run the end-to-end weekly walkthrough with approved test data against the checklist, including one missed agent run and the manual fallback, and record each result. | US-01 to US-07 | 3 | T-034, M2 to M5 |
| T-036 | Run and record the accessibility, device, privacy and access checks on the Google Form and workbook sharing. | FR-03, FR-16 | 2.5 | T-034 |
| T-045 | Write the README sections on how the weekly system runs (operators, the agent and the runbook) and how to contribute. | Infra | 1 | T-049 |
| T-037 | Confirm costs fit the approved budget, start the approved v1 and record the release. | Infra | 1.5 | T-035, T-036, T-008 |

---

## Later

Ideas from CONCEPT-IDEA.md that are outside v1. None is approved or scheduled.

- The AI agent's open-ended collaboration with the board beyond the weekly operational work in v1, including new capabilities and handover.
- Volunteer attendance tracking.
- Volunteer surveys.
- Supplies intake and inventory tracking.
- Drafting impact data.
- Tracking grant measures.
- Online donation acceptance, if the board wants it (OQ-01).
- Measures of success beyond completing a full operation (OQ-11).
- Hand the agent over to the board so a board member runs it on their own Claude account (owner goal, 2026-11-18). Things to settle first: move ownership of the Drive folder, form and workbook from the owner's personal account to the kitchen's Google account; decide whose Claude account and which paid plan, and whether that cost needs board approval, since the board would be paying; reconnect Gmail and Google Drive and recreate the scheduled runs on the new account; walk a board member through the runbook (T-049).
- An email step before the shift choice, with a silent backend check of whether the address is on the volunteer list. A fake-data prototype exists in pull request 4 (branch `demo-email-step`), unmerged. Parked by the owner on 2026-11-16; it has no specification requirement yet.
- Make the demo more of a form, with fields such as name and job preferences (owner idea from the T-009 walkthrough, 2026-11-16). The v1 public form already requires name, email, phone, shift preferences and the weekly choice (FR-15, backlog T-021); this idea is about showing those fields in the prototype with sample data.

## Done

| ID | Task | Ref | Done | Result |
| --- | --- | --- | --- | --- |
| T-001 | Get the owner's decision on the M0/M1 proposals in PLAN.md §6. | Infra | 2026-11-13 | Owner approved all M0/M1 proposals without changes; recorded in PLAN.md §6 and §10. |
| T-002 | Confirm GitHub Pages is enabled for this repository and serving from `/docs`; record the exact production URL in PLAN.md §10. | Infra | 2026-11-13 | Pages was already enabled, publishing from `main`, `/docs`. Source and URL recorded in PLAN.md §11 (Environments) and referenced from §10. |
| T-003 | Create the minimal Brooklyn Community Kitchen entry shell at `docs/kitchen/index.html`, leaving `docs/index.html` unchanged. | Infra (FR-17 route prerequisite) | 2026-11-13 | Created and deployed; `docs/index.html` unchanged. By owner instruction the page shows the project name and the concept's one-sentence pitch, not the "tools are coming" statement in the acceptance criterion. |
| T-004 | Deploy the shell and verify the production URL on desktop and phone; record URL, date and devices in WORK-LOG.md. | Infra (FR-17 route prerequisite) | 2026-11-13 | Deployed to <https://andrewmiaao.github.io/SPUR-AI-Research/kitchen/>. Owner confirmed it loads and reads without horizontal scrolling in Google Chrome on desktop and Safari on phone; site root still serves the SPUR page. Recorded in WORK-LOG.md; device models not reported. |
| T-005a | Prototype state 1: the page lists the two public shift blocks (7:30 a.m. and 11:00 a.m.) from hard-coded fictional data, and choosing one with space shows the request as active. | US-02, FR-03 (prototype only) | 2026-11-13 | Built at `docs/kitchen/demo/index.html`. Owner confirmed the acceptance criteria are met and approved the page location. Sample caps set by the owner for the demo: 7 for the 7:30 a.m. shift and 9 for the 11:00 a.m. shift. |
| T-005b | Prototype state 2: choosing a shift block that is already full shows the request as waitlisted. | US-02, FR-03 (prototype only) | 2026-11-13 | Choosing the full 11:00 a.m. shift shows the request as waitlisted and the count stays at 9 of 9. Owner confirmed it works in a local check; not yet verified at the deployed URL (T-005d). |
| T-005c | Prototype state 3: a second request in the same week is rejected with a plain-language message. | US-02, FR-04 (prototype only) | 2026-11-13 | Merged in pull request 3 and deployed. Checked at the production URL in a desktop browser: a second request is rejected with a message naming the first shift, counts do not change, and a reload starts the demo again with no saved request, no cookies and no browser storage. Real-phone check remains in T-005d. |
| T-005d | Deploy the prototype; confirm on desktop and phone that all three states work from a clean page load and that the page sends no data anywhere. | US-02 (prototype only) | 2026-11-16 | Deployed at <https://andrewmiaao.github.io/SPUR-AI-Research/kitchen/demo/>. All three states ran from a clean load: on phone by the owner (Safari on iPhone), on desktop by Claude in the Claude desktop app's built-in browser. No request was sent after the page loaded, and the live source has no name, email or phone number. The owner later ran the three states on desktop during the T-009 walkthrough (Google Chrome on a Mac). Details in WORK-LOG.md. |
| T-009 | Walk the owner through the demo at the production URL in under one minute; record feedback, blockers and new decisions in WORK-LOG.md. | US-02 (prototype only) | 2026-11-16 | Owner ran the three-state walkthrough at the production URL in about 10 seconds, in Google Chrome on a Mac. Feedback, blockers (none) and decisions (none) recorded in WORK-LOG.md; one new idea added under `Later`. |
| T-006 | Record the owner's decision on where the sign-up entry point goes on the Squarespace site, the method (link or embed), access and cost. | FR-17 | 2026-11-16 | Owner decided: a link or button on the existing volunteer page; a board member with existing access makes the change; $0 only. Recorded in PLAN.md §6 and SPECIFICATION.md v0.2.3 (OQ-16). Exact page, editor and link wording not yet recorded. |
| T-010 | Record the owner's decisions on the application and storage approach and on the project budget as approved entries in PLAN.md §6. | Infra | 2026-11-18 | Owner decided: $0 budget (OQ-09); Google Workspace for everything unless the owner says otherwise; Google Sheets for data (OQ-15); a Google Apps Script web app; Zeffy for donations. Recorded in PLAN.md §6 and SPECIFICATION.md v0.2.4, in pull request 6. Not yet verified: Apps Script quotas, the board's account type and cost, public web-app access, and a free Zeffy-to-Sheets connection. |
| T-011 | Give every `U` task below a base estimate plus 50% buffer, compare the total with the 32-hour envelope, and record the feasibility verdict in PLAN.md §3. | Infra | 2026-11-18 | Claude drafted base estimates for all 37 M2–M6 and Squarespace tasks: 74 h base, 111 h with buffer (114 h including T-011). Verdict recorded in PLAN.md §3: M6 by week 5 is infeasible at 10 h/week; it exceeds the 32-hour envelope even without the 22 h of provisional estimates. Owner approved the estimates on 2026-11-18 and moved the M6 target to February 14, 2027 (PLAN.md §5; SPECIFICATION.md v0.2.5). Pull request 6. |
