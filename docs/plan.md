# Trip Planner — Plan

> **When:** Week 3 (Sections 1–2), Week 4 (Sections 3–4) · **Owner:** Architecture Lead (Done by Delivery Lead: Kristiana Lulgjuraj) (in a team of 4, the Plan owner) · **Done when:** every item in the SVC Self-Check at the end is true.
>
> **Version:** 1.0
>
> **Approved on:** 11/12/26 **by:** Architecture Lead ___ · Product Owner MM · Delivery Lead KL
>
> **Filled-in Example:** `docs/examples/plan-example.md`

The Spec says *what* to build. The Plan says *how*, in what order, and what might go wrong.

---

## 1. Approach

A simple web app for users to organize and plan trips. Users log in to view their created trip itineraries, and can create new trips to add to their collection. Trips and itineraries can easily be edited or deleted. 

---

## 2. Key Decisions (ADRs)

*An ADR (Architecture Decision Record) is one row per real choice between options. ADR-00 is always your tech stack — decide it first, early in Week 3, because the database goes into `data-api-design.md` Section 0. The course defaults are filled in; change one only for a real reason, and say why in "Why this one."*

| ADR | Decision | Req IDs | Alternatives considered | Why this one |
|-----|----------|---------|-------------------------|--------------|
| ADR-00 | Tech stack — Frontend: Vue, no build (starter skill: collection-template) · Backend: Simulated · Database: ___ · Hosting: GitHub Pages (repo root) | | | |
| ADR-01 | Use a simulated login with email. | R5, R7 | Full login with email and password authentication | Application doesn't store sensitive information and omitting full login allows focus to remain on app functionality. |
| ADR-02 | Display user trips in order with soonest trips at the top and furthest trips at the bottom. Past trips appear in a separate section at the bottom, underneath all future trips. Include option to sort/filter trips | R5 | Organize in alphabetical order. | More intuitive for user to have the soonest trip appear first, rather than having to dig to find it among past and future trips. Gives user the option to sort as desired. |
| ADR-03 | Separate each day of itinerary in a "card" | R4 | Vertical Timeline | Easier to identify which events/activities/destinations belong to each day of the trip. | 

*Changed your mind later? Don't delete the old row — add a new ADR and write "Replaced by ADR-0X" in the old one.*

---

## 3. Screens & Build Order

*Every screen a user sees, plus any non-screen part (such as the data layer), in the order you'll build them — anything you leave out, the agent will invent. Carry over what worked in the Week 3 prototype test. P1 first, one scenario end to end before the next: first the one that shows your data (usually browsing), then the riskiest.*

| # | Screen or part | Route | Shows / does | Req IDs | Priority |
|---|----------------|-------|--------------|---------|----------|
| 1 | Data 'data.js' | - | Simulated Backend | R1-11 | P1 |
| 2 | Main/Welcome screen | /welcome | For users who aren't logged in, shows a sign in/sign up page with an brief intro to the web app's purpose. | R5 | P1 |
| 3 | Login/Signup screen | /welcome/login | Allows users to create an account and log in to their account using a simulated login. | R7 | P1 |
| 4 | "My Trips" Page | /mytrips | Shows logged in user's created trips, with upcoming trips appearing at the top. Allows users to create new trips and delete trips. This is the "main screen" for logged in users. | R5, R8| P1 |
| 5 | Create Trip Screen | /mytrips/new | Allows users to enter general details about a trip, such as destination and dates, before saving and allowing users to add detailed itinerary parts. | R1, R2, R3, R6, R10 | P1 |
| 6 | Trip Itinerary Screen | /mytrips/:id | Shows users detailed trip information, along with a vertical timeline itinerary with cards for each day, where users can add activities and notes to each day. Allows users to make edits to or delete activities, rearrange days, and add/remove days. | R3, R4, R5, R8 | P1 |
| 7 | Add activity/destination screen | /mytrips/:id/destination/new | Form to add a destination or activity to a trip itinerary. | R3 | P1 |
| 8 | Edit Trip Screen | /mytrips/:id/edit | Allows users to edit general details of an existing trip, similar to create trip screen. | R9, R10 | P2 |
| 9 | Error Screen | - | Alerts users when there are missing required fields, unsaved changes, or other errors. | R2, R6, R10 | P2 |

**Why this order:** Application build order is organized in the order that a user would interact with the application from start to finish for creating a simple trip itinerary. This allows us to ensure the main functionality of the app is prioritized prior to any additional features. 

---

## 4. Risks & Assumptions

*Anything that might go wrong, and anything you're taking on faith — including accounts, APIs, or tools you depend on but don't control. Rate Likelihood and Impact as Low / Medium / High.*

| Risk or assumption | Likelihood | Impact | Mitigation |
|--------------------|------------|--------|------------|
| Users may accidentally delete a trip. | Medium | High | Alert users when deleting a trip, alowing users to confirm the action. Include an "Undo" option for major changes that is available for at least 10 seconds. |
| Users may forget to save changes made to a trip. | High | High | Alert users of unsaved changes before leaving the page, and allow users to save before continuing. |
| Users may have trouble finding a specific trip among their created trips. | Low to Medium | Medium | Allow users to search their created trips with a search box. |
| Web app might not display properly on different screen sizes | High | Medium | Test app at various screen sizes to ensure layout is responsive. |

---

## SVC Self-Check

- [x] **Simple** — the approach reads in under a minute; each ADR states one decision.
- [x] **Valuable** — every ADR and screen has a requirement ID; every "Why this one" names a real trade-off, not "it was easier."
- [x] **Complete** — ADR-00 names the full stack, starter skill, and database; every P1 requirement is covered by a screen or part; P1 comes first, one scenario end to end at a time; every risk has a mitigation; the team has approved it before Tasks are written.
