# Trip Planner — Tasks

> **When:** Week 5, with updates in Weeks 6–8 · **Owner:** Delivery Lead
>
> **Approved on:** Pending team review · **by:** Delivery Lead ___ · Architecture Lead ___ · Product Owner ___

This task list follows the Trip Planner specification, build plan, and Data & API Design. Each task includes a requirement reference and a clear way to verify the result. The team will review the draft before the Week 6 build.

## 1. Task List

| ID | Task | Priority | Traces to (R# / ADR) | Depends on | Done when | Status |
| --- | --- | --- | --- | --- | --- | --- |
| T0 | Set up the Vue app using the collection-template starter | P1 | ADR-00 | — | The starter pages open in a browser without errors in the console. | Not started |
| T1 | Prepare simulated data for users, trips, destinations, days, and activities. Note: use sample user for created trips until T2. | P1 | ADR-00, R1, R3, R4, R5 | T0 | `data.js` can save and load a sample trip with its destinations and activities. | Not started |
| T2 | Create the welcome page and simulated email login/account creation | P1 | ADR-01, R5, R7, R12 | T0, T1 | Users can open `/welcome` and enter an email on `/welcome/login` to either login or be prompted to create a new account without a password. Upon successful account creation, user is logged in and can reach `/mytrips` placeholder page | Not started |
| T3 | Create the My Account page | P1 | R13, ADR-04 | T2 | A logged-in user can open `/myaccount` and see their email; a logged-out user cannot access the page. | Not started |
| T4 | Show saved trips on the My Trips page | P1 | R5, R8, ADR-02 | T1, T2 | `/mytrips` shows saved trips, with the nearest upcoming trip first. | Not started |
| T5 | Build the new-trip form | P1 | R1 | T1, T4 | A trip named “NYC 2027” with dates January 15–21, 2027 can be saved and appears on My Trips. | Not started |
| T6 | Validate required trip details before saving | P1 | R2 | T5 | A trip without an end date does not save, and the missing field is highlighted. | Not started |
| T7 | Create the detailed daily itinerary view | P1 | R4, ADR-03 | T1 | `/mytrips/:id` shows the days of a trip in separate cards, once the team confirms the layout. | Not started |
| T8 | Add destinations with start and end dates | P1 | R3 | T5, T6, T7 | Manhattan (January 15–17) and Buffalo (January 18–21) both appear on the saved trip. | Not started |
| T9 | Add activities to the selected itinerary day | P1 | R4 | T7, T8 | “Empire State Building Tour” added to January 16 appears under January 16 after saving. | Not started |
| T10 | Load saved trip details when users return | P1 | R5 | T4, T7, T8, T9 | Reopening a trip shows its saved name, dates, destinations, days, and activities. | Not started |
| T11 | Handle save errors without losing entered information | P1 | R2, R6 | T5, T9 | Save error when "End" date is before "Start" date keeps the entered information on screen and allows the user to try again. | Not started |
| T12 | Warn users before leaving with unsaved changes | P1 | R10 | T11 | Leaving a page after making changes asks whether to save or discard them. | Not started |
| T13 | Conduct first-time user testing | P1 | R7 | T10, T11 | At least four people test the app; at least three of four complete a trip without assistance, and the results are recorded. | Not started |
| T14 | Verify page loading performance | P1 | R8 | T4, T10 | Browser tests show the My Trips and trip-details pages each load in under 10 seconds. | Not started |
| T15 | Support edits to trips and activities | P2 | R9 | T10 | Changing a trip's end date from January 21 to January 22 is still saved after reopening the trip. | Not started |
| T16 | Provide an Undo option for deleted activities | P2 | R11 | T15 | After deleting an activity, Undo stays available for at least 10 seconds and restores the activity when clicked. | Not started |

**Status note:** Statuses are provisional until the team confirms development progress. Update any task already in progress or completed before approval.

## 2. Cross-Check (Week 5)

The table traces each P1 requirement from the Specification to the Data & API Design, the Plan, and the proposed development tasks.

| Req ID | Data & API (entity / endpoint) | Plan (ADR / screen #) | Task(s) |
| --- | --- | --- | --- |
| R1 | Trip; `POST /v1/trips` | Screens 1, 5; ADR-00 | T1, T5 |
| R2 | Trip required fields; validation error (400) | Screen 5; screen 9 also handles errors | T6 |
| R3 | Destination; `POST /v1/trips/{id}/destinations` | Screens 1, 5, 6, 7 | T1, T8 |
| R4 | Day and Activity; endpoints for adding days and activities | Screens 1, 6; ADR-03; screen 7 needs R4 listed | T1, T7, T9 |
| R5 | User and Trip; `GET /v1/me`, `/v1/trips`, `/v1/trips/{id}` | Screens 1–4, 6; ADR-01, ADR-02 | T1, T2, T4, T10 |
| R6 | Save-error message and retry handled in the app | Screen 5; screen 9 is currently P2 | T11 |
| R7 | Simulated login; `POST /v1/login`; usability test | Screen 3; ADR-01 | T2, T13 |
| R8 | Trip-list and trip-detail data; browser loading test | Screens 4, 6 | T4, T14 |
| R12 | User; `POST /v1/users` | Screen 3; ADR-01 | T2 |
| R13 | User email display; My Account page | Screen 10; ADR-04 | T3 |

**Result:** All ten P1 requirements have proposed task coverage. The document references are identified, but the issues below must be reviewed before the cross-check can be considered complete.

### Cross-check findings requiring team review

1. **Database choice:** The Plan leaves the database blank in ADR-00. The Data & API Design says PostgreSQL through Supabase, but also says the backend is simulated. The team should confirm whether Supabase is only the intended future database or part of the Week 6 implementation.
2. **Activity date in R4:** The Specification says an activity added to January 16 appears on January 17. The Spec owner should confirm the intended date and update the acceptance test. **Complete 11/25/26 KL**
3. **Itinerary layout:** ADR-03 says to use daily cards, while the screen description mentions a vertical timeline. The Plan should use consistent terminology for the selected layout.
4. **Save errors:** R6 is P1, but the separate Error Screen is listed as P2 in the Plan. Save-failure handling must remain in the P1 build even if a separate error screen is deferred.
5. **Activity screen:** Screen 7 is for adding destinations *and* activities, but only lists R3. It should also reference R4 if it handles activities.
6. **Login requirement:** The Plan includes simulated email login, but the Specification doesn't list login as its own requirement. The team should clarify whether login is a supporting design decision or needs an explicit requirement.
7. **Approvals:** The Architecture Lead approval is still blank in the Plan and Data & API Design. The Tasks document also needs team approval.
8. **Usability testing:** R7 needs results from at least four testers. The task should remain open until the results are recorded.
9. **Required destination details:** R2 lists destinations as required for saving, while R1 allows users to create a trip before adding destinations. The team should clarify at which stage destination details become mandatory.
10. **Editing and Undo:** The P2 tasks must retain the specified unsaved-change warning and 10-second Undo behavior.

## 3. Gap Log (Weeks 6–7)

Complete this section during Weeks 6–7 when build or testing results identify unclear or missing instructions.

| What the agent got wrong or guessed | Which document & section caused it | Fix applied | Fixed in re-run? |
| --- | --- | --- | --- |
| Unclear implementation boundary in T1: create trip requires User ID, but login behavior associated with T2. | tasks.md Section 1: Task List | Added note to T1 to associate created trips with a sample user until T2. | — |
| Unspecified behavior for known email when logging in | tasks.md Section 1: Task List | Included R12 in specification.md and new API Endpoint for R12 in data-api-design.md | - |
| Agent displayed logged-in user email at top of page in navbar | Agent assumption not specified in documents | Created ADR-04 in plan.md | - |
| Failure to save triggers not specified in order to complete T11 | tasks.md Section 1: Task List | Changed "Done When" condition to be more specific | - |

## 4. Build Notes (Week 8)

- **Live URL:** Pending publication.
- **Simulated:** Pending build verification; the current design specifies simulated login and backend behavior.
- **Not built:** Pending final build review.

## SVC Self-Check

- **Simple:** Each task begins with an action and includes a verifiable completion check. The team should confirm that every task is small enough to finish within one day.
- **Valuable:** Every task links to a requirement or architecture decision.
- **Complete:** All ten P1 requirements have proposed tasks. The cross-check findings and approval remain open.
