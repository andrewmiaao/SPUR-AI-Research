# BACKLOG: Brooklyn Community Kitchen AI Assistant

> **Purpose of this document:** the living, ordered list of work. One line per item,
> small enough to finish in a sitting, traceable back to the specification.
> **Input:** `SPECIFICATION.md` (what) + `PLAN.md` (order).
> **Rule:** the top of `Now` is always the next thing you pick up.

**Status:** Approved by the project owner on 2026-11-13 (generated 2026-11-13 from SPECIFICATION.md v0.2.2 and PLAN.md). Approval does not unblock any task: `Blocked by` entries and `U` estimates stand until their blockers are resolved.

**How to read it**

- **Ref** is the specification ID the task serves (US-xx / FR-xx), or `Infra` for infrastructure and project-gate work.
- **Est.** is base effort in hours, before the plan's 50% buffer. `U` means unestimated: the task cannot be sized until its blocker is resolved.
- **Blocked by** names the open question (OQ-xx, SPECIFICATION.md §12) or task that must be closed first. A blocked task must not be started by guessing the answer.
- Task IDs match the references in PLAN.md §4. IDs are not in strict numeric order; the order of the rows is the priority.

---

## Now (M0 and M1: demo production release, target 2026-11-21)

Base estimate remaining: M0 0 h (complete 2026-11-13), M1 8 h (8 h before the 50% buffer). Fictional data only. No persistence, no form submission, no external service, no cost.

| # | ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | --- | ---: | --- |
| 1 | T-005a | Prototype state 1: the page lists the two public shift blocks (7:30 a.m. and 11:00 a.m.) from hard-coded fictional data, and choosing one with space shows the request as active. | US-02, FR-03 (prototype only) | 2.5 | T-004 |
| 2 | T-005b | Prototype state 2: choosing a shift block that is already full shows the request as waitlisted. | US-02, FR-03 (prototype only) | 1.5 | T-005a |
| 3 | T-005c | Prototype state 3: a second request in the same week is rejected with a plain-language message. | US-02, FR-04 (prototype only) | 1.5 | T-005a |
| 4 | T-005d | Deploy the prototype; confirm on desktop and phone that all three states work from a clean page load and that the page sends no data anywhere. | US-02 (prototype only) | 1.5 | T-005b, T-005c |
| 5 | T-009 | Walk the owner through the demo at the production URL in under one minute; record feedback, blockers and new decisions in WORK-LOG.md. | US-02 (prototype only) | 1 | T-005d |

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

## Next (M2 to M6: gated, not yet estimated)

Every implementation task here is `U` until T-011 is done. Nothing below is authorized by the M0/M1 approval.

### Planning gate (plan week 1 checkpoint)

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-010 | Record the owner's decisions on the application and storage approach and on the project budget as approved entries in PLAN.md §6. | Infra | U | OQ-09, OQ-15 |
| T-011 | Give every `U` task below a base estimate plus 50% buffer, compare the total with the 32-hour envelope, and record the feasibility verdict in PLAN.md §3. | Infra | 2 | T-010 |

### Squarespace entry point

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-006 | Record the owner's decision on where the sign-up entry point goes on the Squarespace site, the method (link or embed), access and cost. | FR-17 | U | OQ-16 |
| T-007 | Add the approved entry point to the Squarespace site, pointing at the production sign-up flow. | FR-17 | U | T-006 |
| T-008 | Walk through the sign-up flow starting from the Squarespace site and record the result. | FR-17, US-02 | U | T-007 |

### M2: schedule and sign-up core

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-012 | Operators can create, save and reopen a week's schedule with task names, start and end times, and caps. | FR-02, US-07 | U | T-010 |
| T-042 | Record the owner's decision on cap reductions below the active count, then implement cap editing with that rule. | FR-02 | U | OQ-04, T-012 |
| T-013 | Operators can publish a schedule; an unpublished week's form link shows no tasks and accepts no sign-ups. | FR-13 | U | T-012 |
| T-014 | The public form saves a sign-up as active until the cap is reached, then as waitlisted in request order, including simultaneous requests for the last place, and closes Thursday 6:00 p.m. Eastern. | FR-03, US-02 | U | T-013 |
| T-015 | The form rejects a second request from the same volunteer in the same week and explains why. | FR-04, US-02 | U | T-014 |
| T-043 | Operators see a weekly summary with each task's time, cap, active count and waitlist count. | FR-12, US-07 | U | T-014 |

### M3: protected volunteer records

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-016 | Record the owner's decision on how operators sign in and how operator accounts are added and removed. | FR-01 | U | OQ-08 |
| T-017 | Record the board's privacy, retention and deletion rules for volunteer, donor and accounting data in SPECIFICATION.md. | US-01 | U | OQ-07 |
| T-018 | Record who owns the existing master spreadsheet and get operator access to it in the board's Google Workspace. | US-01 | U | OQ-15 |
| T-038 | Record the owner's review of the backend email-matching risk, the approved abuse controls and the recovery process. | FR-15 | U | T-017 |
| T-019 | Operator screens require the approved sign-in. | FR-01 | U | T-016 |
| T-020 | Operators can view and edit a volunteer's name, email, phone and shift preferences, and the save updates the master spreadsheet. | FR-01, US-01 | U | T-018, T-019 |
| T-021 | The public form collects profile fields and stores them with the sign-up, separate from the master sheet, and never displays stored volunteer information. | FR-15, FR-16 | U | T-014 |
| T-040 | Operators can review a submission's profile details next to the matched record and save approved changes to the master sheet. | FR-15, FR-16 | U | T-020, T-021 |
| T-041 | Verify and record that a visitor cannot open operator screens or see any other volunteer's details. | FR-16 | U | T-019, T-021 |

### M4: email, withdrawals and promotion

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-022 | Record the approved wording of the Tuesday sign-up email and the Friday confirmation. | FR-06, FR-07 | U | OQ-06 |
| T-039 | Record the internal address for withdrawal requests and how a message identifies the sign-up. | FR-14 | U | OQ-05 |
| T-046 | Record the approved rules for failed sends, missed jobs, retries and duplicate-send prevention. | FR-06, FR-07 | U | OQ-12 |
| T-023 | Send the Tuesday 2:30 p.m. Eastern sign-up email to every volunteer individually, with the week's form link. | FR-06, US-03 | U | T-022, T-013 |
| T-024 | Send the Friday 9:00 a.m. Eastern confirmation to volunteers with active sign-ups. | FR-07, US-03 | U | T-022, T-014 |
| T-044 | Operators see each email batch's status and each failed recipient. | FR-06, FR-07 | U | T-046, T-023 |
| T-025 | When a place opens, promote the first waitlisted request and email the volunteer; a failed email shows as failed to operators. | FR-05, US-02 | U | T-014, T-022 |
| T-026 | Process a withdrawal email from an address on file, remove the sign-up and trigger promotion; unmatched emails are flagged for an operator. | FR-14, US-02 | U | T-039, T-025 |

### M5: finance and volunteer preparation

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-027 | Record the owner's decision on the donation payment system and the donor fields to store. | FR-08 | U | OQ-01 |
| T-028 | Record the approved expense categories and fields, report and budget periods, currency, and who sets the budget. | FR-09, FR-10 | U | OQ-03 |
| T-029 | Update SPECIFICATION.md so US-05 and FR-11 agree on what volunteer preparation v1 includes. | US-05, FR-11 | U | OQ-02 |
| T-030 | Record each incoming donation automatically with amount, donor name, donor email and payment reference, and no operator identity. | FR-08, US-04 | U | T-027, T-019 |
| T-031 | Operators can enter an expense with date, amount and category and see it in the expense list. | FR-09, US-06 | U | T-028, T-019 |
| T-032 | Operators can generate a spending report and a budget report for a period; a failed calculation never shows as zero. | FR-10, US-06 | U | T-031 |
| T-033 | Include the approved compliance video link in the Tuesday sign-up email, with no completion tracking. | FR-11, US-05 | U | T-029, T-023 |

### M6: integrated acceptance and release

| ID | Task | Ref | Est. | Blocked by |
| --- | --- | --- | ---: | --- |
| T-034 | Record the owner's "full operation" checklist and the supported devices, browsers and accessibility standard. | US-07 | U | OQ-10, OQ-13 |
| T-035 | Run the end-to-end weekly walkthrough with approved test data against the checklist and record each result. | US-01 to US-07 | U | T-034, M2 to M5 |
| T-036 | Run and record the accessibility, device, privacy and access checks on the sign-up flow. | FR-03, FR-16 | U | T-034 |
| T-045 | Write the README sections on how to run the project and how to contribute. | Infra | U | T-010 |
| T-037 | Confirm costs fit the approved budget, deploy the approved v1 and record the release. | Infra | U | T-035, T-036, T-008 |

---

## Later

Ideas from CONCEPT-IDEA.md that are outside v1. None is approved or scheduled.

- The conversational AI agent that works alongside the board, including its capabilities, boundaries and handover.
- Volunteer attendance tracking.
- Volunteer surveys.
- Supplies intake and inventory tracking.
- Drafting impact data.
- Tracking grant measures.
- Online donation acceptance, if the board wants it (OQ-01).
- Measures of success beyond completing a full operation (OQ-11).

## Done

| ID | Task | Ref | Done | Result |
| --- | --- | --- | --- | --- |
| T-001 | Get the owner's decision on the M0/M1 proposals in PLAN.md §6. | Infra | 2026-11-13 | Owner approved all M0/M1 proposals without changes; recorded in PLAN.md §6 and §10. |
| T-002 | Confirm GitHub Pages is enabled for this repository and serving from `/docs`; record the exact production URL in PLAN.md §10. | Infra | 2026-11-13 | Pages was already enabled, publishing from `main`, `/docs`. Source and URL recorded in PLAN.md §11 (Environments) and referenced from §10. |
| T-003 | Create the minimal Brooklyn Community Kitchen entry shell at `docs/kitchen/index.html`, leaving `docs/index.html` unchanged. | Infra (FR-17 route prerequisite) | 2026-11-13 | Created and deployed; `docs/index.html` unchanged. By owner instruction the page shows the project name and the concept's one-sentence pitch, not the "tools are coming" statement in the acceptance criterion. |
| T-004 | Deploy the shell and verify the production URL on desktop and phone; record URL, date and devices in WORK-LOG.md. | Infra (FR-17 route prerequisite) | 2026-11-13 | Deployed to <https://andrewmiaao.github.io/SPUR-AI-Research/kitchen/>. Owner confirmed it loads and reads without horizontal scrolling in Google Chrome on desktop and Safari on phone; site root still serves the SPUR page. Recorded in WORK-LOG.md; device models not reported. |
