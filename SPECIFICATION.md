# SPECIFICATION: Brooklyn Community Kitchen AI Assistant

> **Purpose of this document:** define *what the system does* precisely enough that two
> different people (or two different AI agents) would build roughly the same thing.
> **Input:** the owner-approved `CONCEPT-IDEA.md`.
> **Output:** the source of truth for `PLAN.md` and `BACKLOG.md`.
> **Rule:** describe behaviour, data, and rules — not implementation details you haven't decided yet.

| Field | Value |
| --- | --- |
| Status | `Approved` (project owner, 2026-11-13; open questions and implementation gates remain open) |
| Concept doc | [CONCEPT-IDEA.md](./CONCEPT-IDEA.md) |
| Author | Project owner with AI drafting assistance |
| Reviewer(s) | Project owner |
| Version | 0.2.2 |
| Last updated | 2026-11-13 |

---

## 1. Summary

The first release is an operational tool for the five operating board members and a part-time helper, covering volunteer records, weekly capped sign-ups and waitlists, scheduled email, donations, and accounting reports. The operational tool will be continuously iterated and improved as the board spends more time with the agent. The board already has a public Squarespace website and an existing master spreadsheet that is currently unoperational and is not owned by the board; building or redesigning the website is out of scope, while connecting approved operational flows to the website and making the existing spreadsheet operational remain in scope. The spreadsheet is housed in Google Workspace. The AI agent and its conversational interaction with the board are longer-term goals, not v1 requirements. The owner has confirmed that the 6:30 a.m. pickup and 7:30 a.m. soup/unloading tasks end at 7:15 a.m. and 8:15 a.m., respectively. The project owner approved this specification revision as a basis for planning on 2026-11-03. Accounting, privacy, website integration, and other schedule and withdrawal details still need decisions before the affected implementation. Further projects will be added to this document. No separate onboarding/training workflow is required; initial email communication includes the approved compliance video link instead.

## 2. Goals and non-goals

**Goals (v1 must achieve):**

1. Let volunteers choose shifts from a weekly sign-up form, enforce the stated upper volunteer limit for each defined task, and offer a waitlist when a task is full.
2. Record volunteer form submissions as weekly sign-up requests kept separate from the master spreadsheet, let the five board members and part-time helper (the operators) maintain volunteer profile information in the master spreadsheet, automatically push out weekly emails, and record donations and categorized expenses.
3. Support the requested onboarding/training and accounting/reporting capabilities. Their detailed requirements remain blocked by the open decisions listed in section 12.

**Non-goals (explicitly not in v1):**

1. Marketing materials or social media.
2. The longer-term conversational AI-agent capability and secondary goals listed in the concept.
3. Online donation processing is not included in this draft; whether it is wanted remains open.
4. Building, replacing, or redesigning the existing Squarespace website.

**Constraints:** The working planning assumption is 7–12 hours per week. The November 21, 2026 target is a demo production release: the M0/M1 demo (the live entry shell plus the fake-data volunteer flow) deployed to and reachable at a production URL. It is a target to aim for, not the full v1 release and not proof of a full kitchen operation. The working project-budget assumption is a low-to-zero budget with a planning cap below $300 until the board approves a higher limit. Success for the prototype is measured by whether the workflow is operational and reviewable by the board. The kitchen will be in operations, while backend functions are still being improved and may not be completely implemented. All six operational capabilities remain in first-release scope; feasibility against any production date and the budget still needs review, and no scope reduction is assumed.

## 3. Users and permissions

The concept confirms five board members and a part-time helper as operators, all with access to and editing rights for all data. Access will be provided and built through google workspace. They will have access through personal emails, and through Brooklyn Community Kitchen's google account.

| Role | Can do | Cannot do |
| --- | --- | --- |
| Visitor / volunteer using a weekly sign-up link | View the current weekly sign-up choices and submit a sign-up or waitlist request using their name, email, phone number, and shift choice. A public submission may be matched to a stored volunteer record for operator review and sign-up tracking, but it may not write profile data to the master spreadsheet as specified in FR-15 and FR-16. | View volunteer lists, other volunteers' contact details or sign-ups, donations, expenses, reports, or onboarding records; access operator screens. |
| Operator (board member or part-time helper) | Access and edit all data, including volunteer records, weekly shifts/sign-ups, email, donation, expense, report, and onboarding data. | No separate restriction from other operators is specified. |
| Admin / owner | The owner is one of the operators and reviews the product scope. No distinct system-admin privileges have been confirmed. | No distinct restriction or additional privilege has been specified. |

All operators may access and edit all data. The authentication method and operator account lifecycle remain undecided. A visitor signup must not reveal existing volunteer information.

## 4. User stories

| ID | Story | Priority |
| --- | --- | --- |
| US-01 | As an operator, I want volunteer profile information to be stored in the board's master spreadsheet and updated only through the operator workflow, with weekly sign-ups tracked separately, so that profile data stays accurate without allowing public submissions to write directly to the master record. | Must |
| US-02 | As a volunteer, I want to choose one task per week on the weekly signup form, join a waitlist when a task is full, receive an email if promoted, and request a withdrawal by emailing the kitchen, so that I can offer help without exceeding task caps and update my plans. | Must |
| US-03 | As an operator, I want the weekly signup email and Friday confirmations sent on the agreed schedule, so that volunteers receive timely information. | Must |
| US-04 | As an operator, I want to record a donation and who donated it, so that incoming donations are tracked. | Must |
| US-05 | As an operator, I want an onboarding and training capability for volunteers, so that new volunteers can be prepared for kitchen work. | Must — blocked until onboarding content and completion behavior are decided (OQ-02). |
| US-06 | As an operator, I want to categorize expenses and generate spending and budget reports, so that the board can review the kitchen's finances. | Must — report rules and budget periods need decisions (OQ-03). |
| US-07 | As an operator, I want to review the weekly schedule and current sign-ups, so that I can prepare for a full kitchen operation. | Must |

## 5. Functional requirements

Every requirement below has a Given/When/Then acceptance criterion. Requirements that depend on unresolved concept decisions are explicitly blocked and are not an authorization to invent the missing behavior.

| ID | Requirement | Story | Acceptance criteria |
| --- | --- | --- | --- |
| FR-01 | The system shall let an operator view and edit volunteer records containing a volunteer's name, email, phone number, and shift preferences. | US-01 | **Given** an authenticated operator and a volunteer record, **when** the operator opens it, **then** its saved values appear. **Given** an operator edits valid values and saves, **when** the save succeeds, **then** the record and master spreadsheet show the updated values. |
| FR-02 | The system shall let an operator create and review a weekly kitchen schedule using the owner-confirmed operating outline, task boundaries, dates/times, and each task's volunteer cap. All operators may change task caps at any time. | US-02, US-07 | **Given** an operator has entered a week's confirmed tasks, times, and caps, **when** the operator saves and opens that week's schedule, **then** the schedule shows those task names, times, and caps. Every task must have a defined start before its schedule can be published for sign-up. The handling of a cap reduction below the active signup count requires owner confirmation (OQ-04). |
| FR-03 | The system shall accept a volunteer's sign-up for one of the two public shift blocks, 7:30 a.m. or 11:00 a.m., until the task's confirmed upper limit is reached, then place additional requests on that task's waitlist in request order. Sign-ups close Thursday at 6:00 p.m. local Eastern time. | US-02 | **Given** a task with available places, **when** a volunteer submits a valid sign-up before the deadline, **then** the request is recorded as active for the selected 7:30 a.m. or 11:00 a.m. shift block. **Given** the task has reached its cap, **when** another volunteer requests it before the deadline, **then** the request is recorded as waitlisted and the active sign-up count does not exceed the cap. **Given** multiple requests arrive concurrently for the final place(s), **when** they are processed, **then** no more requests are active than the remaining capacity and the others are waitlisted in request order. **Given** the deadline has passed, **when** a volunteer opens the form, **then** new sign-ups are unavailable. The public form shows the two approved shift blocks for sign-up and records the request separately from the master volunteer profile sheet. |
| FR-04 | The system shall not allow a volunteer to request multiple tasks in the same week. **Given** a volunteer already has an active or waitlisted request for a task in a week, **when** they submit a request when a request is already in the system **then** the system does not create a second request and explains that the request already exists. **Given** a volunteer already has an active or waitlisted request for any task in a week, **when** they request a different task in that week, **then** the second request is rejected, whether or not the task times overlap, and the volunteer is told they are already signed up for the initial task. 
| FR-05 | The system shall automatically promote the first eligible request in a task's ordered waitlist when a place becomes available and notify the volunteer by email. | US-02, US-07 | **Given** a task has an available place and a non-empty waitlist, **when** the place becomes available, **then** the first waitlisted request in order becomes active, the active count remains at or below its cap, and the system attempts to email the volunteer. Because a volunteer may hold only one active or waitlisted request per week (FR-04), a waitlisted request never conflicts with another request from the same volunteer. **Given** the email fails, **then** the promotion remains visible to operators with a failed-notification status. All operators may edit caps. |
| FR-06 | The system shall send the weekly signup email to all volunteer email addresses in the master spreadsheet on Tuesday at about 2:30 p.m. local Eastern time, with a link to that week's signup form. | US-03 | **Given** a weekly schedule and volunteer email addresses exist, **when** the Tuesday send time arrives, **then** each volunteer is sent the message without revealing other recipients' email addresses, and the message includes a link to the corresponding week's form. **Given** no schedule is ready or email delivery fails, **then** the system reports that it was not sent and identifies the affected send. The time follows daylight-saving changes; email content remains open (OQ-06). |
| FR-07 | The system shall automatically send signup confirmation emails on Friday at 9:00 a.m. local Eastern time to volunteers with active sign-ups for that week. | US-03 | **Given** active sign-ups exist, **when** Friday at 9:00 a.m. arrives, **then** each affected volunteer receives a confirmation reflecting their task sign-ups. **Given** delivery fails, **then** the system displays sent or failed status for the affected recipient. The time follows daylight-saving changes; confirmation content remains open (OQ-06). |
| FR-08 | The system shall automatically connect to the approved donation payment system and record each incoming donation, including the donation amount, donor name, and donor email, without requiring an operator to enter or confirm the donation. | US-04 | **Given** the donation payment system receives a successful donation, **when** the payment webhook or sync event reaches the system, **then** the donation record shows the donor name, donor email, amount, and timestamp and contains no operator identity field or operator attribution. Whether the payment system is online-only or supports additional donor fields remains open (OQ-01). |
| FR-09 | The system shall let an operator record an expense date, amount, and expense category. | US-06 | **Given** an authenticated operator enters a valid expense date, amount, and selected category, **when** the operator saves the expense, **then** it appears in the expense list with those values and can be included in a report period. The category list, date meaning, and any additional required fields remain open (OQ-03). |
| FR-10 | The system shall generate a spending report and a budget report from recorded expenses and an operator-entered budget. | US-06 | **Given** expense records and a budget amount for the report period exist, **when** an operator requests the reports, **then** the spending report totals recorded expenses and the budget report shows the spending total against that budget. Period definitions, category breakdowns, and report layout remain open (OQ-03). |
| FR-11 | The system shall include a single compliance video link in the initial weekly signup email sent to volunteers and shall not create a separate onboarding or training requirement or completion status. | US-05 | **Given** a volunteer receives the initial signup email, **when** the email is sent, **then** it contains the approved compliance video link and does not imply that the volunteer must complete a separate onboarding process. **Given** a volunteer has not watched the video, **when** they submit or confirm a sign-up, **then** the system does not record a training completion status or block the signup on the basis of an untracked compliance requirement. |
| FR-12 | The system shall show operators a weekly schedule summary with task times, caps, active signup counts, and waitlist counts. | US-07 | **Given** a saved weekly schedule and sign-up requests exist, **when** an operator opens the schedule summary, **then** each task shows its confirmed time, cap, active count, and waitlist count. **Given** no sign-ups exist, **then** active and waitlist counts show zero. |
| FR-13 | The system shall let an operator publish a completed weekly schedule so its sign-up form can be accessed by volunteers. | US-02, US-03 | **Given** a valid schedule has been saved, **when** an operator publishes it, **then** its public sign-up form becomes available and can be linked in the Tuesday signup email. **Given** the schedule is not published, **when** a visitor opens its form link, **then** no task or volunteer information is exposed and sign-ups are unavailable. |
| FR-14 | The system shall automatically process a volunteer withdrawal request by email, remove the volunteer from the affected sign-up(s), and promote the next eligible volunteer in the waitlist. | US-02 | **Given** a volunteer emails a withdrawal request from the email address on file, **when** the system matches that email to the volunteer and the affected sign-up(s), **then** the volunteer is removed from the active sign-up(s) and the next eligible waitlisted volunteer is promoted automatically. **Given** a place becomes available from the removal, **when** the waitlist is processed, **then** the first eligible request is moved to active status, the volunteer receives an email notice, and the task count remains at or below capacity. **Given** the email cannot be matched to a known volunteer or sign-up, **when** the request is received, **then** it is flagged for operator review and no automatic withdrawal occurs. The internal email address and how requests identify the sign-up(s) remain open (OQ-05). |
| FR-15 | The public volunteer form shall collect a volunteer's name, email address, phone number, shift preferences, and weekly task choice. It shall never display stored volunteer information, including email addresses, to the person filling in the form. Matching a submission to an existing volunteer record by email happens only in the backend, for operator review, and the actual profile update remains operator-only. | US-01, US-02 | **Given** a volunteer submits a valid email address on the public form, **when** the system finds a matching record in the master spreadsheet, **then** the form shows no stored values and does not indicate whether the email is already on file; the match is visible only to operators. **Given** any submission, whether or not a row matches the email, **when** it is processed, **then** it creates a sign-up request without updating the master spreadsheet. **Given** an authenticated operator later reviews the submission, **when** the operator saves valid profile corrections, **then** the master spreadsheet is updated through the operator-only workflow. |
| FR-16 | The system shall prevent public form submissions from modifying volunteer profile records. Only authenticated operators may create or edit volunteer profile rows in the master spreadsheet. Any volunteer-submitted profile information may be shown to operators for review but must not be written to the spreadsheet without operator action. | US-01 | **Given** a volunteer submits profile information through the public form, **when** the system processes it, **then** it does not write those values to the master spreadsheet automatically. **Given** an authenticated operator reviews the volunteer record, **when** the operator saves valid changes, **then** the master spreadsheet updates and the change becomes part of the volunteer profile. **Given** a volunteer submits incomplete or invalid data, **when** the request is processed, **then** the system flags the issue and asks the volunteer to contact an operator or resubmit valid data. |
| FR-17 | The system shall make each approved public operational flow reachable from the existing Squarespace website without requiring a replacement or redesign of that website. | US-02 | **Given** the owner has approved the integration location and method, **when** a visitor follows the website entry point for volunteer sign-up, **then** the visitor can reach the production signup flow. The exact location and whether this uses a link, embed, or another approach remain open (OQ-16); no other Squarespace changes are implied. |

### Confirmed weekly operation

| Time | Signup task / activities | Volunteer cap |
| --- | --- | ---: |
| 6:30–7:15 a.m. | Pick up bread and supplementary groceries from Jetro/Restaurant Depot and She-Wolf. | 2 |
| 7:30–8:15 a.m. | Prepare soup and unload food deliveries; 1–2 volunteers may chop soup ingredients within the task cap. | 4 |
| 8:30–11:00 a.m. | Prepare food and set up service (bread, donated pizza, salads, trays, meal settings, coffee, water, and service area). | 6 |
| 11:00 a.m.–12:30 p.m. | Meal serving. | 5 |
| 11:00 a.m.–12:30 p.m. | Kitchen dishes and trays. | 3 |
| 11:00 a.m.–12:30 p.m. | Front-of-house bread, fruit, and pizza distribution. | 2 |
| 11:00 a.m.–12:30 p.m. | Cleanup and packaging may begin as service slows. | No separate cap specified. |
| 12:30–2:00 p.m. | Close in-house service, distribute packaged meals, clean, sort/remove waste, deliver extra meals, complete final walkthrough, and lock up. | 6 |

All operators may change task caps at any time. If a changed cap is below the number of active sign-ups, the handling is unresolved (OQ-04).

**Proposed cap-change rule for review (not approved):** reject a cap reduction that would put the active signup count above the new cap, explain the conflict, and leave the existing cap unchanged. This preserves the capacity limit and avoids moving volunteers without their knowledge. The owner may approve this rule or specify another resolution (OQ-04).

## 6. Screens / interface

All operator screens require an authenticated operator through the approved Google Workspace integration. The operator experience is built around the board's Google Workspace environment rather than a separate standalone authentication system. Public sign-up access is limited to the currently published weekly form. Errors must be shown in plain language; failed saves or sends must not appear successful.

### 6.1 Operator home / weekly overview

- **Purpose:** Provide an entry point and a compact summary of the upcoming weekly operation
- **Key elements:** Navigation to volunteers, weekly schedule, email status, donations/expenses/reports, and onboarding; current week's tasks and signup/waitlist counts when available.
- **Actions available:** Open each area; select a week to inspect its schedule.
- **Permissions:** Authenticated board members and the part-time helper. All are operators; no role-specific differences are defined.
- **Empty state:** Explain that no weekly schedule has been set up and link operators to schedule setup.
- **Error state:** Show that the overview could not load and offer a retry. Do not show stale counts as current without identifying them as unavailable.

### 6.2 Volunteer records

- **Purpose:** Maintain the volunteer list and each volunteer's shift preferences.
- **Key elements:** Name, email, phone number, shift preferences, and record actions. No additional volunteer fields are specified.
- **Actions available:** View and edit volunteer records. New volunteer information may be received through the public volunteer form for operator review, but public submissions do not directly write to the master spreadsheet. Record deletion is not specified; see OQ-07.
- **Permissions:** Authenticated operators may view and edit all volunteer records. Visitors cannot access this screen.
- **Empty state:** State that no volunteers are recorded.
- **Error state:** Identify whether the list failed to load or a record could not be saved; preserve entered values after a failed save.

### 6.3 Weekly schedule and sign-up management

- **Purpose:** Let operators prepare a week's task schedule and inspect sign-ups and waitlists.
- **Key elements:** Week, publication status, task, task time, capacity, active sign-ups, and ordered waitlist. The task names, times, and default caps in the confirmed weekly operation are approved; the operator may adjust caps.
- **Actions available:** Create or update a week's schedule; publish it; inspect sign-ups; edit caps; inspect automatic waitlist promotions.
- **Permissions:** All authenticated operators may access and edit all data. Visitors may not view this management screen.
- **Empty state:** For no schedule, show that the week is not configured. For an unpublished schedule, identify it as a draft. For a schedule with no requests, show zero active sign-ups and an empty waitlist.
- **Error state:** Identify schedule-load/save failures. On capacity conflict, do not accept a request that would exceed the cap; refresh the displayed active and waitlist counts.

### 6.4 Public weekly sign-up form

- **Purpose:** Let a volunteer select tasks for the published week without exposing other volunteers' information.
- **Key elements:** Week and the two public signup shifts, 7:30 a.m. and 11:00 a.m.; whether each shift has an available place or waitlist; fields for volunteer name, email, phone number, shift preferences, and task choices; the Thursday 6:00 p.m. Eastern time sign-up deadline. The detailed daily task breakdown remains part of the internal operating schedule and operator guidance, but the public sign-up form simplifies the choices to two shift options so volunteers sign up for the morning 7:30 a.m. work or the 11:00 a.m. service window.
- **Actions available:** Submit volunteer information; submit a request for one task for the week; join the waitlist if that task is full; receive a submission result. The form never writes to the master spreadsheet: submitted profile information is held for operator review, and only an authenticated operator updates the master profile (FR-15, FR-16). Returning volunteers are matched by submitted email; their weekly choice receives active or waitlisted status immediately, independently of any operator profile update. Requests to withdraw are emailed to the kitchen's internal inbox and routed to an operator.
- **Permissions:** Any visitor with the weekly form link may submit a request. A visitor cannot view volunteer lists, other people's requests, financial information, or operator screens. The access-link and abuse-control approach remains to be decided.
- **Empty state:** If no week is published, explain that sign-ups are not open.
- **Error state:** Identify invalid or incomplete fields; if capacity changes during submission, show whether the request was accepted or waitlisted. The public form does not write to the master spreadsheet; any profile review remains operator-only. Separate task requests remain recorded regardless of whether the operator later updates the master profile sheet.

### 6.5 Email schedule and delivery

- **Purpose:** Show the weekly signup and confirmation email schedule and delivery status.
- **Key elements:** Message type, scheduled time, recipient count, send status, and any delivery failure. Message copy remains open.
- **Actions available:** Inspect a scheduled batch and failed sends. Friday confirmations are sent automatically without an operator review gate.
- **Permissions:** All authenticated operators may access and edit all data.
- **Empty state:** State that no emails are scheduled because a week or eligible recipients are missing.
- **Error state:** Show failed or partially completed delivery, identify affected recipients where safe, and make the result clear. Do not silently report successful delivery.

### 6.6 Donations, expenses, and reports

- **Purpose:** Record incoming donations from the approved payment system and categorized expenses, then generate the requested reports.
- **Key elements:** Donation amount, donor name, donor email, and payment-system reference; expense date, amount, and category; report period, spending totals, and budget comparison. Donation records do not include the identity of the operator who entered them because the system should receive payment events automatically. Other donor fields, expense fields, categories, budget periods, and report breakdowns remain open.
- **Actions available:** Review incoming donations synced from the payment system; enter and view an expense; request a spending report and budget report.
- **Permissions:** All authenticated operators may access and edit financial data.
- **Empty state:** Show no donations/no expenses as applicable. If there is no entered budget for the selected period, explain that the budget comparison cannot yet be generated; do not substitute the nonprofit's approximately $30,000 in funds or the below-$300 project-budget assumption.
- **Error state:** Identify failed saves or report generation. A report that could not be calculated must not be presented as a valid zero.

### 6.7 Compliance video / orientation

- **Purpose:** Send the approved compliance orientation video with the initial signup email so volunteers receive the required guidance without creating a separate training workflow.
- **Key elements:** A single compliance video link included in the initial email; no volunteer completion tracking or onboarding status field is required.
- **Actions available:** Send the initial signup email with the video link; review email delivery status if the send fails.
- **Permissions:** Authenticated operators may configure send content; volunteers receive the email and link.
- **Empty state:** Show that no video link is available only if the owner has not approved the compliance video URL; otherwise include it in the email content.
- **Error state:** If the initial email cannot be sent, show the send failure and keep the underlying weekly sign-up record visible to operators without creating a training record.

## 7. Data model

Only fields required by confirmed screens and behaviors are listed. Fields whose purpose depends on unanswered questions are not added speculatively. The account identity representation, retention, and deletion rules remain open.

### Entity: `Operator`

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| id | identifier | yes | Identifies the board member or part-time helper who is signed in; exact account source is undecided. |
| display name | text | yes | Shown as the signed-in operator in operator-only screens. |

**Relationships:** operators may use operator-only screens.

### Entity: `Volunteer`

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| email | email address | yes | Unique identifier for the volunteer profile in the master spreadsheet; also used for signup and confirmation email. |
| name | text | yes | Volunteer name. |
| phone number | text | yes | Volunteer contact information. |
| shift preferences | list of task references or preference text | yes | The concept requires shift preferences; the exact preference format is undecided. |

**Relationships:** the profile is stored persistently only in the master spreadsheet. A volunteer may have separate persistent sign-up requests across many weeks, linked by email, with at most one active or waitlisted request in any one week. A volunteer may be referenced by donation records only if later donor/volunteer identity policy permits it; this relationship is not assumed.

**Master spreadsheet:** the volunteer record fields above are the volunteer profile information stored in the board's designated Google Sheets master profile tab. The board already owns an unoperational spreadsheet, and the project should make that existing spreadsheet operational unless the owner approves a different source. The public form does not write profile rows directly to the master profile tab. Instead, the public form records each sign-up in a separate weekly sign-up tab (or equivalent sign-up tracking sheet) within the same Google Sheets workbook, and the operator-only workflow is responsible for updating the master profile tab when needed. The master profile tab is the only persistent copy of volunteer profile data. Weekly sign-up and waitlist records are separate and live in the sign-up tracking tab, linked to a volunteer by email. The board's Google Workspace environment is the approved platform assumption. Operators and helpers should have access. No operator identity is part of the volunteer form data.

### Entity: `WeeklySchedule`

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| id | identifier | yes | Unique schedule identifier. |
| week | date or week identifier | yes | Identifies the scheduled kitchen operation. |
| status | `draft` or `published` | yes | Only a published schedule is available through the public sign-up form. |

**Relationships:** a weekly schedule contains weekly tasks and may be referenced by email batches.

### Entity: `WeeklyTask`

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| id | identifier | yes | Unique task identifier within a weekly schedule. |
| weekly schedule id | identifier | yes | Identifies the schedule that contains this task. |
| task name | text | yes | Task as confirmed by an operator. |
| start time | local time | yes | Local Eastern time, adjusting for daylight-saving changes. |
| end time | local time | yes for published tasks | Required before a task is published for sign-up so that volunteers and operators see the full task time. |
| volunteer cap | positive whole number | yes | Upper volunteer limit for the task. Confirmed caps include pickup 2, soup preparation/unloading 4, food/service setup 6, meal serving 5, kitchen/dishes 3, front-of-house service 2, and cleanup/distribution 6. All operators may change caps at any time. |

**Relationships:** each weekly task belongs to one weekly schedule and has sign-up requests. The owner confirmed the operating outline; task boundaries and caps for activities without a stated range remain open.

### Entity: `SignUpRequest`

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| id | identifier | yes | Unique request identifier. |
| volunteer email | email address | yes | Matches the volunteer profile by email in the master spreadsheet. |
| weekly task id | identifier | yes | Requested task. |
| status | `active`, `waitlisted`, or `withdrawn` | yes | Active count may not exceed the task cap. A new request receives its capacity status immediately, independently of profile synchronization. Withdrawal requests are processed according to FR-14. |
| request order | sequence value | yes | Preserves order for the waitlist. |

**Relationships:** each request belongs to one weekly task and references the volunteer by email, including when that volunteer's profile update is still pending. These request records may persist separately from the master spreadsheet; the volunteer profile itself is not duplicated as a persistent system record.

### Entity: `EmailBatch`

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| id | identifier | yes | Unique scheduled email batch. |
| weekly schedule id | identifier | yes | Signup week addressed by the batch. |
| type | `weekly signup` or `signup confirmation` | yes | Distinguishes Tuesday signup email from Friday confirmation. |
| scheduled local date/time | date and time | yes | Tuesday about 2:30 p.m. or Friday 9:00 a.m. local Eastern time, adjusting for daylight-saving changes. |
| send mode | `automatic` | yes | Scheduled messages are sent automatically without an operator review gate. |
| status | `scheduled`, `sent`, `partially failed`, or `failed` | yes | Allows operators to see whether it was sent. |

**Relationships:** an email batch belongs to one weekly schedule and has per-recipient deliveries.

### Entity: `EmailDelivery`

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| id | identifier | yes | Unique recipient delivery record. |
| email batch id | identifier | yes | The scheduled batch containing this message. |
| volunteer id | identifier | yes | Recipient; the address is read from the volunteer record. |
| message content | text | yes | The rendered message sent to the recipient. |
| status | `sent` or `failed` | yes | Displayed to operators for each recipient. |
| failure detail | text | no | Present only when delivery fails. |

**Relationships:** each delivery belongs to one batch and one volunteer. Exact message templates remain open.

### Entity: `Donation`

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| id | identifier | yes | Unique donation record. |
| amount | monetary amount | yes | Donation amount received from the payment system. Currency is not explicitly stated and must be confirmed. |
| donor name | text | yes | Name associated with the donation from the payment system record. |
| donor email | email address | yes | Email address associated with the donation from the payment system record. |
| payment system reference | text | yes | External reference identifying the incoming donation event; used for reconciliation and audit. |

**Relationships:** the donation record is created automatically from the approved payment system; no operator identity is stored in a donation record. Whether donor identity is linked to volunteer records is undecided.

### Entity: `Expense`

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| id | identifier | yes | Unique expense record. |
| amount | monetary amount | yes | Expense amount entered by an operator. |
| category | text or category identifier | yes | Selected from a category list; category definitions are open. |
| expense date | date | yes | Needed to include the expense in a report period; the date meaning remains open. |

**Relationships:** expenses are grouped into report periods by expense date. Additional expense fields and category definitions remain open.

### Entity: `Budget`

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| id | identifier | yes | Unique budget record. |
| amount | monetary amount | yes | Operator-entered amount against which expenses are compared. |
| reporting period | period identifier | yes | Period covered by the budget; period rules are open. |

**Relationships:** a budget is used by a budget report. Whether budgets are overall or category-specific is open.

### Compliance video / minimal onboarding trace

This project does not maintain a formal onboarding or training completion workflow. The system stores only a minimal compliance-video email log for operational visibility. The log records the volunteer's email, the volunteer's name, and the approved compliance video URL included in the initial weekly signup email. If the email provider supports it, the system may optionally record whether the email was opened, but open tracking is not a required completion state and does not block a volunteer from signing up. The system does not create a separate onboarding record, training record, or completion status.

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| volunteer email | email address | yes | Recipient of the initial signup email. |
| volunteer name | text | yes | Used for operator review of the email log. |
| compliance video URL | URL | yes | Approved video link included in the initial email. |
| email opened (optional) | boolean | no | Optional, provider-supported open tracking only; not a required completion check or approval gate. |

**Retention / deletion:** Keep this minimal compliance log only while the volunteer remains in the active volunteer list or until the project ends. Delete or archive it only under the board's approved retention policy. Do not create a volunteer completion record, onboarding status, or training history. The video link is informational and is sent in the initial signup email; it is not a required completion task.

## 8. Business rules and edge cases

- **Task cap:** active sign-ups for a weekly task must not exceed its configured cap. The owner-confirmed default caps and task blocks are listed in “Confirmed weekly operation.” Operators may change caps. Behavior for a cap reduction below the active signup count remains open (OQ-04).
- **Waitlist:** once a task is full, new requests are waitlisted in request order. When a place becomes available, the system automatically promotes the first waitlisted request in order and emails the volunteer.
- **Duplicate sign-up:** do not create a second active or waitlisted request for the same volunteer, task, and week; explain that the request already exists.
- **Multiple tasks:** a volunteer may sign up for only one active or waitlisted task per week. Reject any request when the volunteer already has another active or waitlisted task for that same week, even if the schedule does not overlap. A schedule cannot be published for sign-up until every task has a start and end time.
- **Email scheduling:** Tuesday's signup email is sent at about 2:30 p.m. local Eastern time to all volunteer email addresses in the master spreadsheet. Sign-ups close Thursday at 6:00 p.m. local Eastern time. Friday confirmations are automatically sent at 9:00 a.m. local Eastern time to volunteers with active sign-ups. These times adjust for daylight saving. Email content and failed-send retry behavior need confirmation.
- **Email mode:** Friday confirmations are sent automatically without an operator review gate.
- **Withdrawals:** volunteers may email the kitchen's internal address to request withdrawal. The system attempts to match the sender email against the volunteer spreadsheet and routes the request to an operator to manage; unmatched senders are also routed to an operator. The internal address and how requests identify the sign-up(s) remain open (OQ-05). A processed withdrawal that opens a place triggers automatic promotion of the next eligible waitlisted request.
- **Signup request handling:** assign each task's active or waitlisted status immediately and store the request separately from the volunteer profile. The public form does not directly modify the master profile sheet; any profile update is handled by an authenticated operator outside the public form flow.
- **Existing profile update:** a public form submission never updates a volunteer row in the master spreadsheet. The submitted email is used only in the backend to match the submission to an existing record for operator review; stored volunteer information, including email addresses, is never shown on the public form; separate verification of control of that email is not required, as chosen by the project owner. Only an authenticated operator may create or edit profile rows.
- **Donation processing:** incoming donation tracking is in scope and should be connected automatically to the approved donation payment system. The system records each donation's amount, donor name, and donor email without requiring operator entry; online donation acceptance remains subject to system approval and provider configuration.
- **Accounting reports:** spending and budget reports require dated expenses and a defined period; expense date, period, categories, currency, and report details must be confirmed before reports can be considered final.
- **Financial accuracy:** failed or incomplete saves/report calculations must be visibly reported and must not appear as successful zero totals.
- **Unavailable email service:** show send failure and retain a visible unsent/failed status. Whether and how to retry automatically is undecided.
- **Duplicate financial entry:** duplicate detection rules are not defined. The system must not silently merge financial records; handling suspected duplicates needs a decision.
- **Access:** visitors may submit sign-ups but must not see other volunteers' records or any financial information. All operators may access and edit all data; the authentication method and operator-account lifecycle need a decision.
- **Limits:** no record-count, upload, rate, or retention limits have been supplied.
- **Operator removal:** what happens to records entered by an operator who later leaves is undecided; preserve attribution until an approved retention policy says otherwise.

## 9. Non-functional requirements

| Category | Requirement |
| --- | --- |
| Performance | No response-time target has been agreed. Signup submission must return a clear outcome and must not report success until the request is saved. |
| Accessibility | No accessibility standard has been selected (OQ-13). Final accessibility acceptance is blocked until the owner approves a measurable standard. At minimum, test keyboard-only completion, programmatic labels, visible focus, and understandable field/submission errors against the approved standard; do not claim accessibility acceptance before the checks are recorded. |
| Devices / browsers | No supported device/browser list has been agreed (OQ-13). Final acceptance is blocked until target devices/browsers are confirmed and the signup flow is verified on them. |
| Privacy | Store only volunteer fields explicitly identified in the concept until the owner approves additional data. Do not expose one volunteer's contact details or requests to another volunteer. Retention and deletion rules are unresolved. |
| Security | Operator-only screens and financial data require an approved authentication approach before real data is used. All operators have the same access/edit permissions. Secrets must not be committed to the repository. Public signup must not expose operator records. A public submission must not modify a volunteer profile; only authenticated operators may. As chosen by the owner, a public submission is matched to an existing record by the submitted email alone, without separate proof of control of that email. |
| Cost | Working assumption is a low-to-zero budget with a planning cap below $300 until the board approves a higher limit. Recurring service charges must be confirmed against that limit before adoption. |
| Availability | No uptime target has been agreed. Scheduled email failures must be visible to operators; manual follow-up process remains to be decided. |
| Data integrity | Capacity checks and financial record saves must not silently fail or produce success-shaped results for records that were not saved. |

## 10. External dependencies

All required external services are assumed to use the approved Google Workspace environment. The project does not add a separate platform or vendor stack beyond the board-approved Google Workspace setup and existing operational tools already available to the team.

| Service | Used for | Account needed | Cost | Fallback if unavailable |
| --- | --- | --- | --- | --- |
| Google Workspace email (Gmail) | Tuesday signup messages, Friday confirmations, and receiving/routing volunteer withdrawal requests | Yes; board-approved Google Workspace account | Included in the approved Google Workspace environment; expected to fit the low-budget plan | Notify operators; use a manually approved communication process to be decided. |
| Google Workspace identity / access control | Restricting operator-only screens and operator access to records | Yes; Google Workspace authentication and sharing model | Included in the approved Google Workspace environment | Do not expose private or financial records; pause operator writes until access is restored. |
| Google Sheets (master spreadsheet) | Store the master volunteer profile data and operational records maintained by operators | Yes; board-approved Google Workspace account and spreadsheet sharing model | Included in the approved Google Workspace environment; expected to fit the low-budget plan | Do not claim a form submission succeeded if the spreadsheet update failed; recovery and notification process need confirmation. |
| Existing Squarespace website | Provide the public entry point to approved operational flows, starting with volunteer sign-up | The site already exists; whether project contributors need access is undecided | No new website purchase is assumed; integration capabilities or costs must be checked against the approved budget | Give the public operational flow a direct URL and have the owner add an approved link when site access/integration is available; keep signup decisions and records in the operational system. |
| Google Workspace / donor payment integration | Only if online donation acceptance is approved and the payment workflow is configured in the approved Google Workspace-supported environment | Undecided; depends on the board-approved donation system configuration | Unknown; must fit approved budget | Not applicable unless online donation acceptance is added to scope. |

## 11. Definition of done (for the whole v1)

- [ ] Every `Must` story has approved, testable functional requirements; US-05 is not complete until onboarding/training is defined.
- [ ] All agreed `Must` stories are implemented and demonstrated without exceeding confirmed volunteer caps.
- [ ] Signup emails and confirmation emails follow the approved schedule and automatic-send behavior, with failure states demonstrated.
- [ ] Donation and expense records and reports pass owner-approved accuracy examples.
- [ ] A person who has never seen the signup form can submit a request without viewing other volunteers' information.
- [ ] Operator access and privacy/retention rules are approved before real personal or financial data is used.
- [ ] Before enabling backend email matching of public submissions against real data, the owner has reviewed the email-only matching risk, approved abuse controls and a recovery process, and recorded explicit acceptance of the residual risk.
- [ ] Volunteers can reach the production signup flow from the existing Squarespace website through the owner-approved integration; the Squarespace website itself has not been replaced or redesigned.
- [ ] Recurring and one-time costs are confirmed to fit the approved project budget.
- [ ] The user-facing process supports a complete weekly kitchen operation as defined by the owner.
- [ ] README explains how to run it and how to contribute.
- [ ] No secrets in the repository.

The project does not build or redesign the existing Squarespace website. The operational public signup surface must nevertheless be deployed and reachable from that site. Whether it is linked, embedded, or connected another way remains undecided pending owner approval.

## 12. Open questions carried forward

| ID | Question | Owner | Needed by |
| --- | --- | --- | --- |
| OQ-01 | Should the donation capability accept online donations as well as record donations entered by board members? What donor information beyond donor identity should be stored? | Project owner | Before donation requirements and external services are finalized |
| OQ-02 | What onboarding/training content, steps, completion tracking, and volunteer access are required? | Project owner | Before US-05 can be implemented or accepted |
| OQ-03 | Which expense categories, expense fields, reporting periods, budget periods, report breakdowns, and currency should accounting use? Who sets/updates the budget? | Project owner / board | Before accounting screens and report acceptance criteria are finalized |
| OQ-04 | Should the system reject a cap reduction that would leave more active sign-ups than the new cap, or should it use another resolution? | Project owner / kitchen operators | Before cap editing is implemented |
| OQ-05 | Which internal email address should receive withdrawal requests, and how should a message identify the sign-up(s) to withdraw? | Project owner | Before withdrawal handling is implemented |
| OQ-06 | What should the Tuesday signup email and Friday confirmation contain? | Project owner | Before scheduled email behavior is finalized |
| OQ-07 | What privacy, retention, and deletion rules apply to volunteer, donor, and accounting data? | Project owner / board | Before real data is stored |
| OQ-08 | How should operators authenticate, and how should operator accounts be added, changed, or removed? All operators may access and edit all data. | Project owner / board | Before access control is implemented |
| OQ-09 | What project budget will the board approve? The current working assumption is a low-to-zero budget with a planning cap below $300 until the board approves a higher limit; the nonprofit's approximately $30,000 in funds is not the project budget. | Project owner / board | Before selecting paid services or committing to recurring costs |
| OQ-10 | What checklist defines completion of a “full operation,” and what is the first successful demonstration? | Project owner / kitchen operators | Before release acceptance |
| OQ-11 | What additional measurable outcomes, if any, matter beyond completing a full operation and demonstrating the capabilities? | Project owner / board | Before final success criteria are approved |
| OQ-12 | What behavior should the system use for suspected duplicate donation/expense records and email failures, including missed scheduled jobs, partial batches, retries, and preventing duplicate sends? | Project owner / board | Before financial and email edge cases are finalized |
| OQ-13 | Which devices/browsers and accessibility standard should v1 support? | Project owner | Before final non-functional acceptance criteria |
| OQ-15 | Which spreadsheet service will be used for the master spreadsheet? Google Workspace is being considered. Operators and helpers should have access. | Project owner | Before spreadsheet access is configured |
| OQ-16 | Where should approved operational flows appear on the existing Squarespace website, and should each flow be linked, embedded, or integrated another way? What access, platform capabilities, and costs are involved? | Project owner / board | Before implementing or accepting FR-17 |

## Planning approval and implementation-readiness

**Planning approval:** The project owner approved version 0.2.0 as the basis for `PLAN.md` on 2026-11-03, following approval of the current `CONCEPT-IDEA.md`. Open questions below remain implementation blockers and are not resolved by planning approval.

**Revision 0.2.1:** Owner-authorized documentation clarifications dated 2026-11-05. These clarify prototype timing, active planning assumptions (7–12 hours/week and a low-to-zero budget capped below $300 until the board approves more), success based on board review of a usable workflow, and measurable accessibility checks without selecting providers, changing the approved email-only matching rule, or resolving any open product decisions.

**Revision 0.2.2:** Owner-directed corrections dated 2026-11-13 that remove internal contradictions. (1) A volunteer may hold only one active or waitlisted task request per week; overlap-based wording was removed. (2) Only authenticated operators edit volunteer profiles; the public form never writes to the master spreadsheet. (3) The November 21, 2026 target is a demo production release of the M0/M1 scope. (4) The public form never displays stored volunteer information, including email addresses; email matching happens only in the backend and the earlier prefill behavior is removed. No open question was resolved by this revision.

**Implementation gates:** US-05 is not satisfied by FR-11's “not configured” state; onboarding must be defined and implemented before a release can claim all Must stories complete. Donation, expense, and report acceptance remains blocked until OQ-01/OQ-03 specify required fields, currency, periods, and expected example results. Real-data use remains blocked on OQ-07/OQ-08/OQ-15 and the explicit public-profile risk review above. Email automation acceptance remains blocked on approved message content and failure/retry behavior (OQ-05/OQ-06/OQ-12). Final accessibility acceptance remains blocked on OQ-13. A decision to proceed with a prototype or partial milestone does not close these v1 gates.

- [ ] Every `Must` story has at least one functional requirement.
- [ ] Every functional requirement has testable acceptance criteria.
- [ ] The data model covers everything the screens display.
- [ ] Empty states, error states, and edge cases are specified.
- [ ] Non-functional requirements are realistic for the time and budget available.
- [ ] Nothing here contradicts the owner-approved revision of `CONCEPT-IDEA.md`.
- [ ] Scope still fits the stated constraints — if not, say what gets cut.

**Owner approval:** On 2026-11-13 the project owner approved this specification (version 0.2.2) as a document. The approval does not resolve any open question in section 12, does not tick the checklist above, and does not clear the implementation gates; requirements that depend on an open question remain blocked.

**Verdict:** `Approved by the project owner on 2026-11-13; implementation readiness remains open`

**Reviewer notes:**

> The owner has resolved the overlapping-signup, pending-spreadsheet-capacity, email-only profile-matching, and end-time decisions for pickup and soup/unloading. Detailed accounting, onboarding, privacy, website integration (OQ-16), remaining schedule, withdrawal, and email details remain open; do not treat blocked requirements as implementation-ready until the owner resolves them. Confirm feasibility against the still-unapproved project budget before selecting services.
