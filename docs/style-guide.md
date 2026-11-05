# [Product/Service Name] — Style Guide

> **When:** Week 2, alongside the Spec · **Owner:** Delivery Lead (whole team approves) · **Done when:** every item in the SVC Self-Check at the end is true.
>
> **Version:** 1.0
>
> **Approved on:** 11/4/26 **by:** Delivery Lead KL · Product Owner MiM · Architecture Lead ___
>
> **Filled-in Example:** `docs/examples/style-guide-example.md`

The Style Guide tells every screen — and every AI agent — exactly how the product looks and sounds, so nobody has to guess. It targets **WCAG 2.2 AA** accessibility.

---

## 1. Brand & Voice

- **Brand principles:** Simple, calm design with minimal distractions. User focus should be on trip itinerary cards. Users should be able to immediately view their created trips upon login.
- **Tone:** Friendly, cool, adventurous. 
- **Button example:** "Create New Trip" rather than "Add New" or a plus sign icon. 
- **Error example:** "Log in to create a new trip itinerary."
- **Logo:** No logo, use "Trip Planner" as application name for now. 

---

## 2. Colors

*3–7 colors. Check each one against the background with the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) and record the ratio. Targets: at least 4.5:1 for normal text; 3:1 for large text (24px, or about 19px bold) and for borders of buttons and form fields.*

| Name | Hex | Use | Contrast vs. background |
|------|-----|-----|-------------------------|
| Primary | #7B80B7 | Main brand color, primary buttons | 3.53 : 1 |
| Text | #000000 | Body text | 18.08:1 |
| Background | #fff8ea | Page background | - |
| Error | #7a7a7a | Error messages | 4.06:1 |
| Accents and Headings | #10111E | Dividers, links, heading text, button text, borders | On Background: 17.72:1 / On Primary: 5:1 |

---

## 3. Type & Spacing

*No more than 2 font families, and one spacing scale built from a base unit — nothing in between.*

| Role | Font | Size | Weight |
|------|------|------|--------|
| Heading 1 | Arial/Sans serif | 48px | Bold |
| Heading 2 | Arial/Sans serif | 32px | Regular |
| Main Text | Arial/Sans serif | 24px | Regular |
| Body Text/Notes | Arial/Sans serif | 16px | Regular |

- **Spacing scale:** 8 / 16 / 24 / 32 / 48px, from an 8px base unit.
- **Max content width:** 1200px. View "My Trips" page as a grid on wide/desktop screens, and as a single column on mobile. 

---

## 4. Components

*The reusable pieces every screen uses. Include how each one looks on hover, keyboard focus, and when disabled or showing an error — an AI agent will guess these if you don't say. Every button, link, and field must be reachable with the keyboard and show a visible focus outline.*

| Component | Rules |
|-----------|-------|
| Button (primary) | Primary background, Accents and Headings text and border, bold text, 15px corner radius, 5px border width. On hover: Accents and Headings background, Background text. |
| Button (secondary) | Background color background, Accents and Headings text and border, bold text, 15px corner radius, 5px border width. On hover: Accents and Headings background, Background text. |
| Card | Background color background, Accents and Headings border and heading color. 15px corner radius, 5px border width. Use for individual day cards within itinerary. |
| Trip Card | Primary background, 15px corner radius. Use for trip cards on "My Trips" page. |
| Form field | Primary background, Text color text, Accents and Headings form border, and current/active form field border. 15px corner radius and 2px border width. |
| Navigation | Primary background, Accents and Headings web app title. Secondary buttons for all buttons in navigation bar. App title on left side and navigation buttons on the right of navigation bar. |

---

## SVC Self-Check

- [x] **Simple** — 3–7 colors, no more than 2 font families, one spacing scale.
- [x] **Valuable** — every rule would change how a screen gets built; the brand principles actually rule things out.
- [x] **Complete** — every section is filled or marked "N/A because…"; every color meets its contrast target; components include hover, focus, disabled, and error states; the whole team has approved it.
