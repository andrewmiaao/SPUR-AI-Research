# PLAN: Brooklyn Community Kitchen AI Assistant

> **Status:** Approved by the project owner on 2026-11-13 (M2-M6 gates, decisions, and estimates remain open)  
> **Planning date:** 2026-11-06  
> **Inputs:** [CONCEPT-IDEA.md](./CONCEPT-IDEA.md) (owner-approved) and [SPECIFICATION.md](./SPECIFICATION.md) v0.2.2 (owner-approved 2026-11-13; implementation readiness remains open)  
> **Companion:** [BACKLOG.md](./BACKLOG.md) holds the ordered task list. This plan defines scope, sequence, proposed technical decisions, gates, and effort.

## 1. Purpose and planning status

The project owner's M0/M1 scope was approved on 2026-11-03: deliver a production-hosted public entry shell and a fake-data volunteer-flow prototype. This document turns that scope into a timeboxed plan; the owner approved it on 2026-11-13, and that approval does not approve any unresolved product or technical decision.

The five-week capacity provided for this plan is **10 hours per week, 50 hours total**. The owner's target is now to reach M6, including all Must stories and production acceptance, by the end of week five, while resolving the necessary decisions early. Treat this as an **aggressive, conditional target**, not a credible commitment yet: M2-M6 still contain unresolved product decisions and backlog tasks marked unestimated. No Must story is being removed or deferred from v1 by this target.

The M0/M1 target is November 21, 2026. On 2026-11-13 the owner confirmed this as the target for a **demo production release**: the M0 entry shell and the M1 fake-data volunteer flow, deployed to and demonstrated at a production URL. The concept and specification now use the same wording. It is not the full v1 release; no v1 production-release date is committed.

## 2. Scope and guardrails

### Five-week target scope

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

- **Available capacity:** 10 hours/week for five weeks (50 hours maximum).
- **Project budget for this plan:** close to $0. Do not incur a new recurring or one-time cost. Any exception requires owner approval first.
- **Skill level:** beginner. Base estimates include ordinary learning, setup, and manual verification time; they are still rough estimates.
- **Buffer rule:** each committed estimate below adds a 50% contingency to the base estimate. The buffer is explicit and is not additional feature scope.

| M0/M1 milestone | Base estimate | 50% buffer | Planned total |
| --- | ---: | ---: | ---: |
| M0 — production shell | 4 h | 2 h | 6 h |
| M1 — fake-data flow and demo | 8 h | 4 h | 12 h |
| **M0 + M1** | **12 h** | **6 h** | **18 h** |

To reach M6 within 50 hours, **no more than 32 hours including the 50% buffer** remain for M2-M6, rework, and release acceptance. That is a hard feasibility envelope, not an estimate that the remaining v1 scope fits. Reserve time for decisions and estimation inside the same 50-hour cap; do not silently count owner decision time as extra capacity.

M2-M6 are not credibly estimable yet: their backlog items include `U` sizes and depend on unresolved requirements, access, and cost decisions. Front-load those decisions in week 1; then decompose each milestone, estimate base effort, add a 50% buffer, and update the backlog. At the end of week 1, compare the buffered remaining estimate to the 32-hour envelope. If it exceeds the envelope, report that M6 by week 5 is infeasible at 10 hours/week without an owner-approved scope, budget, or capacity change. Do not compress testing, bypass an implementation gate, or invent estimates to preserve the date. No paid service or architecture selection is implied.

## 4. Milestones and sequence

Every milestone has a result that can be shown in under one minute. The target is to complete M0-M6 within five weeks, with M0/M1 as the first production-hosted prototype and M2-M6 conditional on early decisions, estimates, and the feasibility checkpoint. Milestone sequencing does not waive any gate.

| Milestone | Scope and dependencies | Demo outcome (under one minute) | Exit criteria / traceability |
| --- | --- | --- | --- |
| **M0 — Live entry shell** | Verify GitHub Pages access and the production URL; create the minimal public shell; deploy it. Preserve the existing SPUR landing page by proposing a separate `/kitchen/` path under the existing Pages site. | Open the production URL on a phone or desktop and show the Brooklyn Community Kitchen entry shell with no operational data or live signup. | Production URL loads on desktop and phone; deployment result and exact URL recorded; no real data exposed. Backlog T-002–T-004; infrastructure and FR-17 route prerequisite. **This deployment is mandatory, even though the page is otherwise empty.** |
| **M1 — Fake-data signup prototype** | Add only the task-choice and status states using clearly fictional, prepared examples. No persistence or integrations. Depends on M0. | In one short walkthrough, choose an available task, show a full task placing a sample request on the waitlist, then show a second task request in the same week rejected. | All three states are reproducible; the rule that a volunteer may request only one task per week is clear; no submission reaches a live system. Capture owner feedback and unresolved decisions. Backlog T-005; T-008's formal integrated walkthrough remains blocked until the approved Squarespace route is available. US-02 prototype only, not acceptance of FR-03/FR-04 for production. |
| **M2 — Schedule and signup core (gated; target week 2–3)** | Build schedule creation/publication and persistent signup capacity, duplicate, deadline, and one-task-per-week rules after application/storage and budget decisions. | Show a fictional published week, accept a request while capacity remains, and show the next request waitlisted. | FR-02–FR-04 and US-02/US-07; owner decisions and buffered estimate first (backlog T-010–T-015). |
| **M3 — Protected volunteer records (gated; target week 3)** | Implement approved operator access and the operator-only master-spreadsheet workflow. Keep public requests separate from profile edits. | Show an operator updating a fictional volunteer record, then show that a public visitor cannot open or change it. | FR-01, FR-15, FR-16 and US-01; OQ-07, OQ-08, OQ-15 and the public-profile risk review must be resolved first (T-016–T-021, T-038, T-040–T-041). |
| **M4 — Email, withdrawals, and promotion (gated; target week 4)** | Implement approved scheduled communications, visible delivery outcomes, withdrawal handling, and eligible waitlist promotion. | Show a fictional signup/confirmation status and a withdrawal that promotes the next eligible request, including the operator-visible outcome. | FR-05–FR-07, FR-14 and US-02/US-03; resolve email, inbox, retry, and cost decisions first (OQ-05, OQ-06, OQ-09, OQ-12; T-022–T-026, T-039, T-046). |
| **M5 — Finance and approved volunteer preparation (gated; target week 4)** | Implement donation tracking, expense entry, and reports only after their fields and rules are approved. Resolve the apparent onboarding requirement conflict before implementing or claiming US-05 complete. | Show one fictional donation, one categorized expense, and the resulting example report; show the approved compliance-video treatment if applicable. | FR-08–FR-11 and US-04–US-06; resolve OQ-01–OQ-03 and the US-05/FR-11 inconsistency first (T-027–T-033). |
| **M6 — Integrated v1 acceptance and release (gated; target week 5)** | Run the approved end-to-end weekly-operation walkthrough, accessibility/device, privacy/access, and production checks, then deploy the approved v1. | Demonstrate the owner-approved weekly workflow from its public entry point and show the corresponding operator outcome using approved test data. | All approved Must-story acceptance and definition-of-done checks; resolve OQ-07–OQ-13, OQ-15/OQ-16 and remaining gates. Re-estimate after decisions and work decomposition (T-034–T-037). |

The Squarespace entry point is not a prerequisite for M0's direct production URL. It remains required for the approved public operational flow before FR-17 can be accepted; do not make an unapproved website edit to make an M0 demo appear complete.

## 5. Five-week accelerated target schedule

The schedule below targets M6 by the end of week five while keeping capacity capped at 50 hours. The November 21 date remains the M0/M1 demo production release target. Week 1 is a go/no-go checkpoint for the remaining work, not permission to skip an unresolved gate. Weekly numbers are ceilings, not work that must be filled with new scope.

| Week | Capacity | Planned work |
| --- | ---: | --- |
| 1 — Nov 9–15 | Up to 10 h | Resolve required owner decisions/access first; complete M0 (6 h including buffer), start M1, and decompose/re-estimate M2-M6. By week's end, verify the remaining buffered estimate fits the 32-hour envelope. |
| 2 — Nov 16–22 | Up to 10 h | Finish M1 (12 h total including buffer across weeks 1–2); demonstrate by Nov 21. Begin M2 only if its gates are cleared and week-1 feasibility check passes. |
| 3 — Nov 23–29 | Up to 10 h | Target M2 and M3: schedule/signup core, then protected volunteer records. Use approved architecture and fictional data until real-data gates are cleared. |
| 4 — Nov 30–Dec 6 | Up to 10 h | Target M4 and M5: email/withdrawals/promotion, then finance and the owner-approved US-05 behavior. |
| 5 — Dec 7–13 | Up to 10 h | Target M6: integrated Must-story walkthrough, remaining approved accessibility/privacy/access checks, production verification, and release. Demo the approved end-to-end outcome in under one minute. |

This sequencing is intentionally aggressive. M3-M5 may overlap only where their approved dependencies permit; do not parallelize work in a way that bypasses review, data-access controls, or testing. If a decision remains open when its milestone begins, stop that affected implementation, record the blocker, and use the week-1 checkpoint or revised forecast rather than substituting an unapproved behavior. If GitHub Pages access or production deployment is blocked, escalate immediately; M0 is not complete until the production URL works.

## 6. Proposed technical decisions

These are proposals for the owner to review, not approvals for the full v1 architecture. **On 2026-11-13 the owner approved the M0/M1 rows** (M0 hosting and route, M0 page, M1 interaction, and no production data or services in M0/M1). The later v1 architecture and Squarespace integration rows remain deferred and unapproved.

| Decision | Proposal and reason | Alternatives rejected for this plan |
| --- | --- | --- |
| M0 hosting and route | Use the repository's existing GitHub Pages `/docs` publishing path, with a `/kitchen/` subpath if the Pages configuration supports it. The repository already has a static `docs/` site; reusing it avoids a new account, vendor, and expected hosting charge, and a subpath preserves the existing SPUR landing page. Verify repository Pages settings and the exact production URL before treating this as available. | Replacing the existing root page risks breaking the current SPUR landing page. A new hosting vendor or paid host adds account/cost/setup without helping the static M0 requirement. A local-only demo fails the production-URL requirement. |
| M0 page | A minimal static page, with no form submission or operational data, is sufficient to prove the production route. | A database, server, or live form is unnecessary for an empty entry shell and adds risk and setup. |
| M1 interaction | For owner review, propose plain HTML/CSS and a small amount of browser JavaScript with hard-coded fictional examples; keep state in the page only. This matches the existing static site and minimizes dependencies for a beginner. It is a prototype choice, not a commitment to the v1 application stack. | A framework, build pipeline, backend, or external form service adds learning/setup and is not required for the three fake-data states. Real Sheets/email integration violates M1's scope and its unresolved privacy/access gates. |
| Production data and services | Use no real personal/financial data and add no service, account, API, or recurring cost in M0/M1. | Connecting Google Workspace, payment, or email services before requirements, permissions, privacy, and cost are approved is rejected. |
| Later v1 architecture | Defer framework, data store, authentication, email provider, and other implementation choices. Record each approved choice with its rationale and rejected alternatives after the relevant open questions are resolved. | Choosing an architecture now would contradict the specification's undecided decisions and could introduce cost or lock-in. |
| Squarespace integration | Defer the exact link/embed/location choice until OQ-16 is answered; demo the direct Pages URL meanwhile. | Editing or embedding into Squarespace without approval could break the existing site or incur unreviewed cost. |

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
| Squarespace location, method, access, and cost (OQ-16) are unresolved. | Website integration and FR-17 acceptance cannot be claimed. | M0/M1 demo directly at the deployed URL; keep T-006/T-007 blocked until approved. |
| The Nov 21 demo production release could be mistaken for the full v1. | Stakeholders may expect real sign-ups or data on that date. | Nov 21 covers M0/M1 only (fake data, no live submissions), as the concept and specification now state; label the demo clearly as a demo. |
| Onboarding language conflicts. | US-05 is Must, while FR-11 describes a compliance link without a completion workflow and the readiness section says US-05 is not yet satisfied. | Resolve OQ-02 and update the approved acceptance criteria before M5 or any v1 completion claim. |
| Budget is close to $0 and several integrations are undecided. | Paid services or new accounts could make the plan infeasible. | No cost or new service without owner approval; validate the full service cost and access model before M2-M6. |
| Remaining v1 requirements are not estimated and depend on decisions. | The 32-hour buffered envelope for M2-M6, including decisions, rework, and release, may be insufficient. | Resolve decisions and produce buffered estimates by the end of week 1. If the total exceeds the envelope, mark the five-week M6 target infeasible at current capacity and seek an owner-approved change; do not claim readiness based on a guess. |

## 9. Ordered cut list if time runs out

Cut or defer work in this order; do not remove the required M0 production deployment or the M1 core demo states to make the schedule look complete:

1. Decorative branding, animation, and visual polish beyond a clear, readable, mobile-usable shell.
2. Additional prototype scenarios or sample data beyond task choice, full-task waitlist, and second-task rejection.
3. Squarespace link/embed work from the current five-week target if OQ-16, access, or cost is still unresolved; keep the direct production URL available and leave integration visibly blocked, not silently dropped from v1.
4. If the buffered M2-M6 estimate exceeds 32 hours, move the M6 date or seek an owner-approved increase in capacity/budget. Do not silently cut a Must story, bypass a gate, or label a partial build as v1; any v1 scope reduction requires an approved specification and backlog change.

If the M0 deployment itself is blocked, record the blocker and seek an approved zero-cost way to complete the production deployment. Do not report the milestone as complete or substitute an unapproved service.

## 10. Review and approval

- [x] Concept approved by the project owner.
- [x] Specification v0.2.1 approved for planning; v0.2.2 applies owner-directed corrections (2026-11-13). The owner approved the v0.2.2 specification document on 2026-11-13. Implementation readiness remains open.
- [x] M0/M1 scope approved by the project owner on 2026-11-03.
- [x] M0/M1 technical proposals in section 6 approved by the project owner on 2026-11-13 (`/kitchen/` route under `docs/` on GitHub Pages, a static page, plain HTML/CSS/JS with fictional data, no real data or services). This does not approve the later v1 architecture.
- [x] This plan approved by the project owner on 2026-11-13. The backlog was approved the same day.
- [x] Production URL and GitHub Pages configuration verified on 2026-11-13: Pages publishes from `main`, `/docs` (checked through the GitHub API); the owner confirmed the `/kitchen/` URL loads on a real desktop and phone. See section 11.
- [ ] OQ-16 resolved before any Squarespace change.
- [ ] Remaining milestone scope, decisions, and buffered estimates approved before implementation.

**Current verdict:** `Approved by the project owner on 2026-11-13; M6 by week 5 is an aggressive, conditional target at 10 hours/week. Full-v1 feasibility remains unverified pending early decisions and buffered estimates.`

## 11. Environments

| Environment | URL | Source | Status |
| --- | --- | --- | --- |
| Production (GitHub Pages) — Brooklyn Community Kitchen entry shell | <https://andrewmiaao.github.io/SPUR-AI-Research/kitchen/> | `main` branch, `docs/kitchen/` | Returned HTTP 200 on 2026-11-13 (automated request). Owner confirmed on 2026-11-13 that it loads on a real desktop and phone; browser and device models not recorded. |
| Production (GitHub Pages) — existing SPUR landing page | <https://andrewmiaao.github.io/SPUR-AI-Research/> | `main` branch, `docs/` | Returned HTTP 200 on 2026-11-13; unchanged. |

GitHub Pages publishes from the `main` branch, `/docs` folder (legacy branch build, HTTPS enforced). There is no staging environment; local preview is opening the files under `docs/` directly.
