# Trip Planner — Specification

> **When:** Week 1 (Section 0), Week 2 (the rest), refined in Week 3 · **Owner:** Product Owner - Mi Meh · **Done when:** every item in the SVC Self-Check at the end is true.
>
> **Version:** 1.0
>
> **Approved on:** ___ **by:** Product Owner ___ · Architecture Lead ___ · Delivery Lead ___
>
> **Filled-in Example:** `docs/examples/specification-example.md`

The Spec is the source of truth for *what* you're building. Write it so a teammate — or an AI agent — could build from it without asking you a question.

---

## 0. Constitution

*2–3 rules this product must never break, no matter what feature is added. If a rule wouldn't stop any feature, it isn't doing its job.*

| # | Principle | Why it exists |
|---|-----------|---------------|
| 1 |First time users can finish planning a trip without needing help| How we will measure success for the project |
| 2 |Actions and edits can be saved or undone| An accidental mistake or deletion should not cost users loss of planning information |

---

## 1. Problem & Evidence

**Problem and success:** *Users with an upcoming trip having the need to plan for multiple days, where documents are spread out on spreadsheets, and notes app, making planning less organized and stressful. Success: By week 8, all of the main features work, and 70% of test users are able to plan a trip to completion on their own. *

**Evidence:** *(3–5 short conversations or observations with people like your user, outside your team, plus the Week 3 prototype test. Real quotes or what you saw, not opinions.)*

| ID | What we heard or saw | From whom |
|----|----------------------|-----------|
| E1 |"I usually use my notes app to plan trips, but sometimes it's not as efficient as making edits or changes to it involves a lot of retyping and I can't pull it up on my laptop | Friend |
| E2 |"I like using Google Sheets as it more organized but it's hard to access and view on my phone so I often use Notes as well. Having 2 documents makes it difficult to reflect changes on both. |Friend |
| E3 |"I'd download and use a trip planning app if it were free and user friendly" |Co-Worker |


**Riskiest assumption:** *Users will find the app easier and better to plan a trip than their notes app or spreadsheet. We will find out by asking a few people how they plan their trip, than have them test the application. If they complete the protype test, and still prefer their older method of using spreadsheet and the notes app, than the assumption failed.*

---

## 2. Scope

**In scope:** *Planning a trip, which includes creating and naming the trip with start and end dates. Ability to add multiple destinations, with their start and end date, and the itinerary for the days with the ability to change or edit the activities.*

**Out of scope:** *Collaboration feature, map view, offline access, recommended activities, budgeting, bookings.*

---

## 3. User Scenarios

*3–5 short stories of someone using the product. Tag each with a priority:*
- ***P1** — must have. Without it, the product doesn't solve the problem. Keep P1 to 1–2 scenarios that make a complete journey.*
- ***P2** — should have. The product still works without it.*
- ***P3** — nice to have. Cut first if time runs short.*

**S1: Plan a trip** — Priority: P1 
- Actor: Users
- Trigger: Has an upcoming trip and need to start planning.
- Steps: Creates a new trip with the name and dates -> Add 2+ destinations with their dates -> Adds the itinerary for the destinations on a day by day basics
- Success outcome: The trip is created and saved with the destinations and itineraries planned.
- Failure outcome: The trip is missing information, such as destination dates, name, or activities.

**S2: Exiting and returning to a trip to continue** — Priority: P1 
- Actor: Users
- Trigger: Open the app to continue planning the trip.
- Steps: Locates the upcoming trip on the home screen -> Opens the trip -> View or edit the trip details, such as dates, name, destinations, or itineraries.
- Success outcome: Users open to a saved trip they previously created, with all the correct details showing.
- Failure outcome: The trip the User had previously created was not saved correctly, therefore no trip was found.

**S3: Rearranging or editing the trip ** — Priority: P2 
- Actor: User
- Trigger: There is a change in plans.
- Steps: Open the trip -> Make the edits needed to the trip, such as changing the dates, or destinations -> Rearrange the activity from one day to another, remove the activity, or add a new activity.
- Success outcome: The trip reflects the edits made to the plan after saving.
- Failure outcome: The edits get deleted before it was able to save.

*(Repeat for each scenario: S2, S3…)*

---

## 4. Requirements & Acceptance Tests

*Write each requirement as one sentence using one of these [EARS](https://alistairmavin.com/ears/) patterns:*

| Pattern | Use it for | Template |
|---|---|---|
| Always | Rules that are always true | The system shall … |
| When | A user action or event | When [trigger], the system shall … |
| While | Behavior during a state | While [state], the system shall … |
| If … then | Errors and unwanted situations | If [condition], then the system shall … |

*Each requirement takes the priority of its scenario, and each scenario's failure outcome gets its own* If … then *requirement. Requirements that apply on every screen — speed, privacy, accessibility — get their own priority and a number you can test ("loads in under 3 seconds," not "fast"). Its acceptance test says what to do and what should happen, with real values — if you can't write one, the requirement is too vague. Every P1 requirement cites its evidence (E#) or a standard it must meet (such as WCAG), or says ASSUMPTION. Requirement IDs never change once assigned.*

| ID | Requirement | Priority | Acceptance test (do → expect) | Evidence |
|----|-------------|----------|-------------------------------|----------|
| R1 |When a users create a new trip with the name and dates, the system shall create and saves it |P1 |User enters "NYC 2027" and "January 15-January 21" -> Trip is created and will appear on the home screen | E2 |
| R2 |If trip details are missing, such as name, dates, destinations, the system shall not save it and will highlight the missing details for users to fill in before saving. |P1 |User puts in "NYC 2027" and "January 15-" with no end date -> Nothing will save and system will highlight the missing end date. |ASSUMPTION |
| R3 |When a user adds the destination with the name, and start and end date, the system shall add it to the trip |P1 |User adds "Manhattan, January 15-17" and Buffalo, January 18-21" -> Both added to trip details |ASSUMPTION |
| R4 |When users add an activity to a day, the system will add it to that day's itinerary |P1 |Add "Empire State Building Tour" to January 16 -> Appears under January 17 Itinerary |ASSUMPTION |
| R5 |When user open that app, the system should show the saved trip, with upcoming trip listed first. After opening trip, the system should show the trip details. |P1 |User create trips for January and March -> January trip is listed first, trip detailed is saved and correct after reopening the app | E2 |
| R6 |If trip fails to save, the system will pop up an error, keep the entered data on screen and let the user retry to save. |P1 |User trip failed to save -> Error screen pop up, data is still there, User is able to try to save it again |ASSUMPTION |
| R7 |When a first time user is trying to create a trip to completion, the system should let them finish without trying to help  |P1 |Test prototype with 4+ users -> 70% plan a trip to completion without assistance |E3 |
| R8 |The system should display the home screen and the trip details in under 10 seconds. |P1 |Open app and Trip details -> Home screen loaded in under 10 seconds |ASSUMPTION |
| R9 |When the user make edits to the trip details, rearrange activities, or add new activities, the system shall save those changes. |P2 | User edits the dates from "January 15-21" to "January 15-22" -> New date is saved and shown when reopening the trip details | |E1|
| R10 |When a user leaves the screen with unsaved edits, the system will prompt user to either save or discard changes. |P2 |Edit the trip activities, click back button -> System show "Save Changes?" with yes or no buttons. |Constitution 2|
| R11 |When user deletes or change an item, the system shall let the user Undo action for at least 10 seconds. |P2 |Delete an activity -> Undo button shown for 10 seconds -> Activity restored |Constitution #2 |



---

## 5. Open Questions

*The team's one list of unresolved questions — from any document or task. Don't let a builder or an AI guess. If the answer changes a document, update that document before marking the question Resolved.*

| ID | Question | Raised by | Owner | Status |
|----|----------|-----------|-------|--------|
| Q1 | | | | Open / Resolved: [answer] |

---

## SVC Self-Check

- [x] **Simple** — each requirement is one sentence in one EARS pattern; no jargon a new teammate wouldn't know.
- [x] **Valuable** — the Constitution has 2–3 principles that would actually stop a feature; the Evidence table has 3+ rows from real people outside the team, plus the prototype test; each P1 requirement cites evidence or a standard, or says ASSUMPTION; the riskiest assumption is named.
- [] **Complete** — 3–5 scenarios, each with actor, trigger, steps, and both outcomes; P1 is 1–2 scenarios that make a complete journey; every requirement has a unique ID, a priority, and an acceptance test; no open question blocks a P1 requirement; the team has approved it.