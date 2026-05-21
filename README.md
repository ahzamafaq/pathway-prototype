# PathWay EdTech Dashboard Prototype

PathWay is an AI-driven digital advisory SaaS prototype designed to disrupt traditional, expensive international education agencies. Built entirely as a modular Single-Page Application (SPA), the prototype guides European students through the process of applying for international graduate degrees. 

## 🚀 Key Features

- **Interactive Onboarding Flow:** A seamless, "Typeform-style" onboarding sequence to build a student's profile and capture academic interests.
- **AI-driven Program Matching:** Instantly filter and discover university matches tailored to the student's profile, featuring expandable accordion cards with detailed requirements.
- **Comprehensive Application Dashboard:**
  - **Overview Tracker:** High-level KPIs and progress bars for active university applications.
  - **Document Vault:** Manage and upload application documents.
  - **CV & SOP Evaluator:** Visual radar charts evaluating the quality of application documents using "AI Scores".
  - **SOP Master Sync Engine:** Write one master Statement of Purpose and automatically blast tailored versions for specific universities and programs.
  - **Portfolio Analyzer:** Dynamically add extra-curriculars and use simulated AI to generate optimized resume bullets.
  - **Mock Interview Simulator:** Timed, interactive AI interview sessions designed specifically for university admissions.

## 🛠 Technical Architecture

The entire prototype is an incredibly lightweight, **Single-File SPA** (`index.html`) demonstrating complex functionality without the overhead of heavy frameworks.

- **Frontend Core:** Pure HTML5, Vanilla CSS3, and Vanilla JavaScript.
- **Design System:** A cohesive aesthetic utilizing CSS variables, glassmorphism overlays, and a deep navy dark mode.
- **No Build Dependencies:** Zero local dependencies, no Webpack, no Node.js required. (Icons sourced via CDN).
- **Fully Responsive:** Custom `@media` queries collapse complex CSS grid layouts into smooth vertical stacks for mobile devices.
- **State Management:** A global JavaScript object (`S`) acts as the state tracker, allowing smooth navigation and DOM updates without page reloads.

## 💻 How to Use

Since there are no build steps, running the prototype is as simple as possible:

1. Clone the repository:
   ```bash
   git clone https://github.com/ahzamafaq/pathway-prototype.git
   ```
2. Open `index.html` in any modern web browser (e.g., Chrome, Safari, Firefox). 
3. Interact with the onboarding flow, match with universities, and explore the dashboard!

## 📄 Detailed Documentation

For an in-depth, module-by-module technical breakdown, including security considerations and the roadmap for migrating this prototype to a production-ready React/Node stack, please refer to the [PROTOTYPE_REPORT.md](PROTOTYPE_REPORT.md).
