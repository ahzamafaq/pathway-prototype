# PathWay EdTech Dashboard Prototype
**Comprehensive Technical & Functional Report**

---

## 1. Executive Summary
PathWay is an AI-driven digital advisory SaaS prototype designed to disrupt traditional, expensive international education agencies. Built entirely as a modular Single-Page Application (SPA), the prototype guides European students through the process of applying for international graduate degrees. The platform executes a seamless transition from a "Typeform-style" Onboarding flow, to AI-driven Program Matching, and finally into a robust, multi-panel Application Management Dashboard.

## 2. Technical Architecture
The entire prototype is built as a **Single-File SPA** (`index.html`).

- **Frontend Tech:** Pure HTML5, Vanilla CSS3, and Vanilla JavaScript.
- **Design System:** Custom CSS variables define a coherent design language (glassmorphism overlays, deep navy dark mode, soft crisp borders, accent colors to represent status).
- **Dependencies:** The application has **zero** local dependencies or complicated build steps (like Webpack or Node.js). It strictly imports `lucide.min.js` via a CDN for modern, stroke-based scalable vector icons.
- **Responsiveness:** Managed via a global `@media (max-width: 900px)` query. CSS grids collapse to `1fr` columns, flex-direction pivots to vertical stacks, and the fixed sidebar dynamically converts into a slide-out drawer with a backdrop overlay.

## 3. Global State & Navigation (`S` Object)

Because there is no active backend, the prototype uses a global JavaScript object named `S` to track all session data and interface states.

```javascript
const S = {
  screen: 'onboard', // Macro view: onboard | matches | dashboard
  panel: 'overview', // Micro view: active widget on dashboard
  history: [],       // Breadcrumb stack for the Return/Back button
  theme: 'dark',     // Active color scheme
  applications: [...]// Local array of user data
};
```

### The DOM Router (`goTo` & `showPanel`)
The UI functions without URL changes. Instead, it alters DOM visibility classes.
*   `goTo(screen)`: Transitions between the three main macro-screens (Onboarding -> Matches -> Dashboard). It manages the `active` classes and hides/shows the floating back button.
*   `showPanel(name)`: Dedicated to the main Dashboard. It hides all `.pv` (panel view) elements, locates the target panel based on its ID, and applies `.ac` (active class) triggering a fade-up CSS animation.

---

## 4. Module-by-Module Functional Breakdown

### A. The Onboarding Flow (`#sc-onboard`)
The user's initial interaction is a centered, minimal onboarding sequence.
- **How it works:** DOM elements (`#obs1`, `#obs2`) are shown and hidden linearly using the `nextStep()` and `prevStep()` functions. 
- **Checkboxes:** Utilizing `toggleTag(el)`, users can select multiple academic interests via visually distinct pill buttons.

### B. Program Matches View (`#sc-matches`)
After the user "calculates" their path, they are presented with university matches.
- **Filtering (`filterCountry()`)**: A dynamic JavaScript function that iterates through all `.mc-card` elements, reading `data-country` attributes. Elements that fail the match are given a `hidden` CSS class, instantly filtering the view without page reloads.
- **Accordion Cards (`toggleMC()`)**: Clicking a university card expands it via CSS `max-height` transitions, exposing granular program requirements mapped to colored status text (`var(--green)` for valid, `var(--amber)` for pending).

### C. The PathWay Dashboard (`#sc-dash`)
The core hub. Contains a persistent left sidebar and a dynamically swapping right content area.

#### 1. Live Notification System
- **Functionality:** A notification bell icon lives in the top bar. `toggleNotif()` opens a drop-down reading from the DOM.
- **Click-Outside Listener:** A global event listener detects if a click occurs outside the `.notif-drop`, automatically closing it to simulate native OS behavior.

#### 2. Overview / Application Tracker
- High-level KPIs driven by static mock data. The application progress bars are pseudo-calculated using CSS `width: 62%` injections.

#### 3. Document Vault
- **Simulated Uploads:** Clicking the upload zone triggers a hidden `<input type="file">`. The `handleFiles(files)` listener mocks an upload delay.
- **Delete Mechanism:** Hovering over a document reveals a red 'X'. Clicking flags the DOM element. The `deleteDoc()` function prompts native `confirm()`. If approved, the DOM node (`node.remove()`) is instantly destroyed.

#### 4. CV & SOP Evaluator (AI Visualization)
- Displays radar charts and score breakdowns. Visually, it uses CSS pseudo-bars to represent an "AI Score."

#### 5. SOP Versioning (Master Sync Engine)
A pivotal productivity feature for applicants. Users edit *one* core document and automatically blast versions optimized for specific universities.
- **The Engine (`syncSOPVersions()`)**: This function retrieves the inner text from the `master-sop` textarea. 
- **Regex Mapping**: It uses standard string `.replace()` targeting macro-variables:
  - `[UNIVERSITY]` -> ETH Zurich / TU Munich
  - `[PROGRAM]` -> M.Sc Informatics / Data Science
  - `[PROFESSOR NAME]` -> Pulls context automatically
- **AI Improve (`aiImproveSOP()`)**: Disables the button to avoid double triggers, runs a mocked 2-second `setTimeout()`, and forcibly overwrites the textarea with structurally superior, highly detailed text before calling the auto-sync function.

#### 6. Portfolio Analyzer & AI Bullet Generation
Allows users to add extra-curriculars that AI will assess.
- **Form Injection (`addPortfolioEntry()`)**: Bypasses typical `.innerHTML` risks by programmatically constructing DOM elements via `document.createElement()`. It securely captures the user's title, description, and technology tags, dynamically mounting a new project card.
- **Bullet Generator (`genBullet()`)**: Simulates an LLM taking a raw project description and compressing it into an optimized, action-oriented resume bullet.

#### 7. Mock Interview Simulator
Provides interactive, timed AI interviews built specifically for university admissions.
- **State Gating**: Hidden behind a "Start Session" wall. The user selects a mode (Technical, Rapid Fire).
- **The Logic Loop:**
  1. `startInterview()` resets the master clock and cleans up the visual transcript.
  2. `askNextQuestion()` pulls a string from the global `QUESTIONS` array.
  3. `simulateAI()` types out the text forcefully simulating a real-time transcript streaming effect via rapid `setTimeout` intervals over a `split()` character array.

## 5. Security & Stability Considerations
- **No JS HTML Entity Bleed:** Functions dealing with user-creation data (like the Portfolio module) bypass inline template literals within the `<script>` tag. They utilize strict `dataset` attachments or DOM closures to prevent parser-breaking syntactic errors.
- **DOM Leaks:** The file contains exact CSS encapsulation. Early prototypes leaked `@keyframes` into the body; this was constrained entirely to the `<style>` block.

## 6. Path to Production (Next Steps)
While fully interactive, migrating this from prototype to production requires:
1. **Separation of Concerns:** Splitting `index.html` into React (`.jsx`) or Vue components.
2. **Backend Hooks:** Swapping the `.replace()` Regex engines with an actual LLM proxy endpoint (OpenAI API over a Node.js Express server).
3. **Database Integration:** Re-mapping the static `S` state tracker to pull arrays asynchronously from a PostgreSQL or MongoDB database via JWT authentication scopes, preserving user progress across sessions.
