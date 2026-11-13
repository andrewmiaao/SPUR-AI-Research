# CONCEPT-IDEA: Brooklyn Community Kitchen AI Assistant

> **Purpose of this document:** capture *what* you want to exist and *why it matters* —
> before anyone argues about *how* to build it.
> **Written by:** the project owner (name not provided).
> **Reviewed by:** a human, before you move on to `SPECIFICATION.md`.

| Field | Value |
| --- | --- |
| Status | `Approved` |
| Author | Project owner |
| Reviewer(s) | Project owner |
| Created | 2026-10-31 |
| Last updated | 2026-11-13 |

---

## 1. One-sentence pitch

> The Brooklyn Community Kitchen AI Assistant helps the kitchen's five operating board members and a part-time helper coordinate volunteer and nonprofit operations so they can run the kitchen's work more easily. (inferred)

## 2. The problem

Brooklyn Community Kitchen is a small-scale community kitchen serving food for people in need in Brooklyn. Its five operating board members are the nonprofit's primary employees, and each has other commitments; it also has a part-time helper who is an outside consultant, who is doing this for a class. They have recurring work that includes scheduling shifts, managing volunteer information, and sending scheduling emails. These examples describe current needs rather than a fixed list: the nonprofit's priorities may change, and the assistant's work should adapt to what is most useful. They have an existing public website on Squarespace, social media campaign, and are working on an onboarding video and are building the operational tools, spreadsheets, forms, or systems described here.

 Board members have also requested a donation tracking system and a simple compliance-video flow in the initial volunteer emails. The time, money, or other costs of the current situation have not been measured.

## 3. Who it is for

| Audience | What they care about | How they'd find us |
| --- | --- | --- |
| Primary user: the five operating board members and a part-time helper | Easing day-to-day operations and making progress on the nonprofit's changing priorities, including volunteer coordination and administrative work | Not discussed; an internal introduction is possible (inferred) |
| Person who decides / pays | The operating board may decide on spending (inferred); the project budget is not approved and the budget is presumed to be close to zero| Not discussed |

## 4. The idea

Brooklyn Community Kitchen's longer-term vision is an AI agent that works alongside the board, helping ease operations as needs arise. The agent should collaborate with board members over time: helping them identify and make progress on useful projects, and taking on appropriate routine tasks so the board can focus its limited time on running the nonprofit. It should support the board rather than replace its judgment or decision-making, and adapt as priorities change. The first release is an operational tool with a conversational AI agent; when the agent is handed over to the board in a later phase, board members will need to be able to converse with it.

The first release will address six operational deliverables: shift scheduling with capacity limits, a volunteer database, automatic emailing, donation tracking, compliance-video communication, and accounting. These capabilities are the initial operational scope; they do not replace the longer-term goal of an ongoing working relationship with an AI agent. The board and agent should revisit priorities together as they learn what is most useful.

The board already has a public website on Squarespace. Building, replacing, or redesigning that website is out of scope. The project should connect approved public operational flows—starting with volunteer sign-up—to the existing Squarespace site, so visitors can reach the operational systems from the site's appropriate pages. Whether that connection is a link, an embedded experience, or another approach is undecided and must be confirmed before implementation; Squarespace account access is assumed, integrations, or added costs.

**Secondary goals to build toward:** The board would also like the agent to potentially support:

- Automating volunteer database management and attendance tracking.
- Automating emails and surveys.
- Supplies intake and inventory tracking.
- Drafting impact data.
- Tracking grant measures.
- Bookkeeping

These goals may overlap with the initial deliverables and are not separate commitments or a fixed implementation sequence. The board and agent can refine and prioritize them as needs and capacity become clearer.

The volunteer database should track each volunteer's name, email, phone number, and shift preferences. A form should let volunteers submit their information and weekly shift choices; public submissions should not directly edit the master spreadsheet, and the form should never show stored volunteer information, including email addresses. The system may match a returning volunteer by email in the backend only, to highlight their existing record for operator review. The master spreadsheet should remain the persistent source of volunteer profile truth and should be updated only by an authenticated operator. The system may keep separate persistent weekly sign-up and waitlist records. Weekly shift choices from the sign-up should be tracked in a different sheet. If the spreadsheet cannot be updated, the submission should be retained for up to seven days so an operator can retry the update. Each week, the system should create a shift sign-up form and send an initial sign-up email to all volunteer email addresses on Tuesday at about 2:30 p.m. Eastern time. That initial email should include the compliance video link; no separate onboarding or compliance-status workflow is required. Sign-ups close Thursday at 6:00 p.m. Eastern time. These scheduled times follow local Eastern time and adjust for daylight saving time. For each task, the upper end of the volunteer range in the operating schedule is the sign-up cap; all operators may change task caps at any time. When the cap is reached, additional volunteers should be able to join a waitlist. If a place opens, the next volunteer on the waitlist should be promoted automatically and notified by email. Volunteers may request withdrawal by emailing the kitchen's internal email address; the sender's email should be matched to identify the volunteer, and the agent should remove them from the affected sign-up(s) and move the next eligible waitlisted volunteer up automatically. Confirmation emails should be sent automatically on Friday at 9:00 a.m. Eastern time to volunteers who signed up.

The owner confirmed this recurring operating outline: Shifts are weekly on Saturdays

| Time | Task / activities | Volunteer cap |
| --- | --- | ---: |
| 6:30 a.m. | Pick up bread and supplementary groceries from Jetro/Restaurant Depot and She-Wolf. | 2 |
| 7:30 a.m. | Prepare soup and unload food deliveries, including 1–2 people chopping soup ingredients (within the cap). | 4 |
| 8:30–11:00 a.m. | Prepare food and set up service, including bread, donated pizza, salads, trays, meal settings, coffee, water, and the service area. | 6 |
| 11:00 a.m.–12:30 p.m. | Meal serving. | 5 |
| 11:00 a.m.–12:30 p.m. | Kitchen dishes and trays. | 3 |
| 11:00 a.m.–12:30 p.m. | Front-of-house bread, fruit, and pizza distribution. | 2 |
| 11:00 a.m.–12:30 p.m. | Cleanup and packaging may begin as service slows. | Included in the applicable shift; separate cap not specified. |
| 12:30–2:00 p.m. | Close in-house service, distribute packaged meals, clean, sort/remove waste, deliver extra meals, complete a final walkthrough, and lock up. | 6 |

All operators may change task caps at any time. Withdrawal requests are emailed to the kitchen's internal inbox and sent to an operator to manage.

For accounting, the owner wants board members to be able to review incoming donations automatically tracked from the approved donation payment system, categorize expenses, and generate spending and budget reports. Donation records should not include the identity of the operator who entered them; the system should accept and preserve donor name, donor email, donation amount, and payment-system reference. The owner reports that there is currently no accounting system. The donor's phone number, email, name, and organization may be kept by the payment system or bookkeeping workflow as needed, but the system should not require operator entry for each donation event. Compliance-video content and report details are not chosen. The technical approach has not been chosen.

**Working alongside the board (happy path):**

1. Board members work with the agent as operational needs come up, deciding together what would be most helpful and what should take priority.
2. The agent helps make progress on agreed projects and handles or streamlines suitable recurring tasks, checking with the board where decisions or approval are needed.
3. For example, the agent may help prepare the weekly volunteer sign-up and confirmation process, maintain volunteer records, or support donation, onboarding, and accounting work using the deliverables the board has prioritized.
4. The board and agent learn from each week's operation and adjust the agent's support to fit the nonprofit's current needs.

## 5. What success looks like

The longer-term outcome is that an approved agent may become a useful, ongoing partner to the board and make the nonprofit's operations easier. The v1 operational tool is a separate, earlier deliverable; it does not include that agent. Whether and when a full operation can serve as an early demonstration remains subject to an owner-approved checklist and date.

| Signal | How we measure it | Target | By when |
| --- | --- | --- | --- |
| The kitchen's backend operations are complete| Check whether the master spreadsheet is running, integrated into the website, emails are being sent, and shifts are being scheduled; the exact checklist and date still need owner confirmation | One full operation (proposed; checklist and acceptance method not approved) | Saturday, November 21, 2026 is the target for a demo production release: the M0/M1 demo (live entry shell plus fake-data volunteer flow) at a production URL. That is not the full v1 release or proof of a full operation. The operation target date remains unconfirmed. |
| The agent provides useful ongoing support to the board | Board members review whether the agent helped with current priorities and eased routine operational work; specific measures are not yet agreed | Proposed longer-term outcome; v1 is an operational tool and does not include the conversational agent | Define and measure only after board-led discovery and approval of an agent pilot; no v1 date is set. |

The precise operation checklist and measures of ongoing usefulness—such as time saved or work the board can complete more easily—are not yet agreed.

## 6. Explicitly out of scope (for now)

- Building, replacing, or redesigning the existing Squarespace public website. Integrating approved operational flows with that website remains in scope.
- Not building marketing materials.
- Not building or managing social media.
- Not pursuing projects or automations without the board's agreement on their usefulness and priority.

## 7. Constraints and realities

- **Time:** The concept's earlier estimate is 10–15 hours per week, mostly from the project owner in the part-time-helper role. These ranges have not been reconciled or confirmed as a sustainable capacity baseline; schedule forecasts are provisional until the owner confirms availability. The November 21, 2026 target is a demo production release: the M0/M1 demo (the live entry shell plus the fake-data volunteer flow) deployed to and reachable at a production URL. It is a target to aim for, not the full v1 release and not proof of a full kitchen operation.
- **Money:** No budget has been approved. The project should assume a low to zero budget; the nonprofit's has a total of $30,000 currently
- **Skills:** Not provided.
- **Rules:** Volunteer information identified so far is shift preferences, name, email, and phone number. All five board members and the part-time helper should be able to access and edit all project data. Privacy, retention, deletion, and other data-handling rules have not been provided and need to be clarified before deciding what information may be stored.

## 8. Alternatives considered

| Option | Why not (yet) |
| --- | --- |
| Do nothing / status quo | The current approach has some functional tools or system for this work, and it does not limit the number of people per shift. |
| Existing product | A nonoperational master spreadsheet, sign-up sheet, shift-sign up sheet, and compliance tracker are built but not available to the board; the existing Squarespace site is the public website, not the operational system. |

## 9. Open questions

- [ ] Should the donation capability also accept online donations, in addition to recording donations entered by board members? What donor details should be stored beyond identifying the donor?
- [ ] What onboarding and training steps or materials should the first version support?
- [ ] For accounting, which expense categories should be available, what should a spending/budget report contain, and who sets or updates the budget?
- [ ] Which internal email address should receive withdrawal requests, and how should a message identify which sign-up(s) the volunteer wants to withdraw from? What should the Tuesday signup email and Friday confirmation contain?
- [x] May a volunteer sign up for or be promoted to tasks whose times overlap? Resolved 2026-11-13: no. A volunteer may hold only one active or waitlisted task per week.
- [ ] If an operator lowers a task cap below its current active signup count, how should the system resolve the excess sign-ups?
- [ ] What privacy, retention, and deletion rules apply to volunteer, donor, and accounting information? Donor details beyond identifying the donor have not been specified.
- [ ] Which spreadsheet service will be used for the master spreadsheet? Google Workspace is being considered. Operators and helpers should have access.
- [ ] Where on the Squarespace site should operational flows appear, and should they open as links, embedded experiences, or another integration? What account access, platform capabilities, or costs would that require?
- [ ] The project budget remains unapproved; the working assumption is below $300. Who on the board will confirm this limit?
- [ ] What checklist defines a successfully completed “full operation” of the kitchen, and what will count as the first successful demonstration?
- [ ] How should the board assess whether the agent's ongoing support is useful (for example, time saved or routine work made easier)?
- [ ] What conversational capabilities, boundaries, and handoff process will the board need when the longer-term AI agent is introduced?

## 10. Assumptions

- 🔴 The project has conflicting, unreconciled capacity estimates: 10–15 hours/week in this concept and 7–12 hours/week in the plan. Neither is a confirmed schedule baseline. Whether all six operational capabilities fit any target date and the unapproved budget remains to be validated.
- 🟡 We assume the board members and part-time helper will work with the agent as an internal operational partner. (inferred)
- 🟡 We assume the initial deliverables listed in section 4 are useful priorities, while the board may adjust them and identify other needs through ongoing collaboration. (inferred)

---

## Reviewer sign-off

Previous reviewer: project owner (2026-10-31).

- [x] The problem is real and clearly stated, independent of the solution
- [x] The audience is specific (not "everyone")
- [x] Success criteria are measurable
- [x] Out-of-scope list is honest and meaningfully limits v1
- [x] Risky assumptions are identified
- [x] Open questions are captured, not hidden

**Previous verdict:** `Approved` — project owner reviewed the previous version and said it looks good.

**Previous revision:** `Approved` — project owner approved the previous concept on 2026-11-02, retaining all six operational capabilities for the first release, increasing available time to 10–15 hours per week, and defining the AI agent as a longer-term phase.

**Current revision:** `Approved` — the project owner approved this revision on 2026-11-03. It clarifies that the board already has a Squarespace website, excludes building or redesigning that website, and includes connecting approved operational flows to it. The integration method and access/cost implications remain open questions.

**Documentation clarification:** On 2026-11-05, the owner authorized clarifying that November 21 is a fake-data prototype target, separating v1 from the longer-term agent outcome, and recording the unreconciled capacity estimates. No operational scope or unresolved owner decision was changed.

**Owner-directed correction:** On 2026-11-13, the owner confirmed that a volunteer may sign up for only one task per week, that only operators edit volunteer profiles, that November 21, 2026 is the target for a demo production release of the M0/M1 scope, and that stored volunteer information, including emails, stays in the backend and is never shown on the public form.

**Reviewer notes:**

> Accounting, onboarding, privacy/retention, some schedule details, and the Squarespace integration method remain open for specification and planning; approval of this concept does not resolve them.
