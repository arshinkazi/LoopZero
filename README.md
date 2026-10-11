# LoopZero - Repeated Sightings Are Evidence

**One sighting is a signal. Repeated sightings are evidence.**

LoopZero is a citizen-powered environmental intelligence prototype that turns repeated observations of local environmental issues into organised, evidence-backed hotspots.

Instead of treating every complaint as an isolated incident, LoopZero connects observations by locality, issue category and landmark to help make persistent problems easier to identify, understand and communicate.

<p align="center">
  <a href="https://arshinkazi.github.io/LoopZero/">Live Demo</a> ·
  <a href="https://builder.aws.com/content/3KYnHcRqo1v6mwgPB3zl9nI7wdM/i-built-loopzero-because-one-complaint-doesnt-tell-the-whole-story">Read the Blog</a>
</p>

---

## The problem

An open drain that remains uncovered, a garbage pile that repeatedly returns, or a leaking water pipe can become a persistent neighbourhood problem.

Individual reports may describe what happened at one moment, but they don't always communicate the bigger picture: how long the issue has persisted, how often it has been observed, or how severe it has become.

**LoopZero explores a simple idea: what if repeated environmental observations were treated as evidence of a persistent problem rather than as separate complaints?**

The project aims to help residents, community volunteers and civic groups organise environmental observations into something more useful than a list of reports.

## How it works

### 1. Report

Residents can submit an environmental observation with:
- Locality and landmark
- Issue category
- Severity level
- Date observed
- Description
- Optional photograph and location coordinates

No account is required to use the prototype.

### 2. Match

LoopZero groups observations using a normalised combination of locality, issue category and landmark.

Related observations become part of a single hotspot, allowing users to explore recurring issues together.

### 3. Prioritise

Each hotspot receives a transparent priority score from 0 to 100, based on persistence, recurrence and severity.

### 4. Communicate evidence

Users can inspect the hotspot's observation timeline, review its score breakdown, update its status, export observations as CSV, and print an evidence report.

## Features

- Environmental issue reporting with form validation
- Hotspot grouping based on locality, category and landmark
- Transparent priority scoring
- Observation timelines and duplicate-review flags
- Dashboard filters for locality, issue type, severity and status
- Overview charts and locality summaries
- Optional photograph and geolocation input
- CSV export for further analysis
- Printable hotspot evidence reports
- Responsive interface with keyboard-focus styling
- Fictional demonstration data for exploring the application

## Understanding the priority score

The score combines three factors:

| Factor | Weight | Purpose |
|---|---:|---|
| Persistence | 25% | Measures how long the issue has been observed |
| Recurrence | 25% | Measures the number of independent observations |
| Severity | 50% | Reflects the highest reported severity among counted observations |

The score is calculated as a weighted combination of normalised factors:

`Score = 100 × (0.25P + 0.25R + 0.50S)`

Here, `P`, `R` and `S` represent the persistence, recurrence and severity factors, respectively, each normalised between 0 and 1.

Persistence is capped at 30 days, and recurrence is capped at six independent observations. Potentially duplicate reports are flagged for review rather than automatically treated as independent evidence.

The score is intended to help organise priorities. It is **not** an official urgency rating, a verified environmental assessment or a health-risk prediction.

## Tech stack

| Technology | Purpose |
|---|---|
| HTML5 | Application structure and forms |
| CSS3 | Layout, responsive styling and visual design |
| Vanilla JavaScript | Routing, hotspot grouping, scoring and interactions |
| Browser local storage | Persisting observations and hotspot status |
| GitHub Pages | Static hosting and public demo |

The application is intentionally built without a framework or build step, keeping the prototype lightweight and easy to run.

## Run locally

No package installation or build command is required.

1. Clone the repository:

   ```bash
   git clone https://github.com/arshinkazi/LoopZero.git
   ```

2. Open the project directory:

   ```bash
   cd LoopZero
   ```

3. Open `index.html` in a modern web browser.

You can also serve the directory using a local static HTTP server if preferred.

## Demo data and limitations

The dashboard includes fictional demonstration observations so visitors can explore the workflow immediately.

Please keep the following limitations in mind:

- **Browser-local storage:** Reports are stored in the current browser and are not shared across users or devices.
- **No backend:** The application does not currently have a server or shared database.
- **No automatic escalation:** Reports are not sent to municipal authorities or other external organisations.
- **Location and photographs:** These are optional inputs; their inclusion does not independently verify a report.
- **Grouping:** Hotspots depend on the current locality, category and landmark matching rules. Different descriptions of the same place may not be grouped together.
- **Scoring:** The score is a prototype ranking mechanism and has not been validated against real-world outcomes.
- **Community impact:** The application has not yet been validated through a real community pilot.

These are known areas for improvement, not capabilities the current prototype claims to provide.

## Future scope

The next development stages could include:

1. Shared storage so multiple residents can contribute to the same hotspot.
2. Improved location matching and duplicate detection.
3. Community verification and evidence review.
4. Privacy-conscious image and location handling.
5. A responsible workflow for sharing evidence with local civic bodies.
6. Pilot testing with real observations to evaluate usability and usefulness.

The long-term goal is to explore whether connecting repeated observations can help communities communicate persistent environmental problems more effectively.

## Deployment and AWS disclosure

The current public demo is hosted on GitHub Pages:

**Live application:** https://arshinkazi.github.io/LoopZero/

The submitted version does not currently use AWS services and has not been deployed on AWS. AWS deployment and shared cloud infrastructure remain possible future improvements.

## Project write-up

I wrote about the motivation, implementation choices and limitations behind this project on AWS Builder Center:

**[I Built LoopZero Because One Complaint Doesn't Tell the Whole Story](https://builder.aws.com/content/3KYnHcRqo1v6mwgPB3zl9nI7wdM/i-built-loopzero-because-one-complaint-doesnt-tell-the-whole-story)**

## Closing thought

LoopZero started with a question about how we communicate persistent environmental problems.

The prototype is an early step towards exploring an answer: connect the observations, show the pattern, and make the evidence easier to understand.

**One sighting is a signal. Repeated sightings are evidence.**

---

*Built as a hackathon prototype using HTML, CSS and vanilla JavaScript. AI-assisted tools were used during development.*# LoopZero

*One sighting is a signal. Repeated sightings are evidence.*

LoopZero turns repeated community observations of garbage, open drains, leaks and dust into prioritized, evidence-backed hotspots. Initial locality: Fatehpur Shekhawati, Rajasthan.

## Problem and solution
A single complaint is easy to ignore. LoopZero groups reports by normalized locality, issue category and landmark, so persistent neglect becomes a visible timeline with a printable evidence report.

## Features
Dashboard with filters, ranked hotspots, report form (validation, optional geolocation after permission, optional photo), hotspot detail with timeline and status control (Open, Under Review, Resolved), add-observation flow, CSV export, print-ready evidence report, overview charts and a schematic locality map, reset demo data.

## Run locally
No build step. Open `index.html` in a browser, or run `npx serve .` in this folder.

## How grouping, duplicates and the priority score work
**Grouping:** a report joins a hotspot when its locality, category and landmark match exactly after lowercasing and removing punctuation. There is no fuzzy matching, so a differently spelled landmark creates a separate hotspot. The report form lets you pick an existing hotspot to avoid this.

**Counted observations:** reports on the same date as an earlier report, with the same text as an earlier report, or with no valid date are flagged for review and not counted toward recurrence or span. They stay in the timeline and CSV. The app has no accounts, so it cannot tell whether reports come from different people.

**Measurements shown separately:**
- Observation span: days between the first and latest counted observation.
- Age: days from the first observation to today.
- Days since the latest observation.
Span shows how long reports continued. It does not prove the problem still exists today.

**Score:** `100 x (0.25 x span + 0.25 x recurrence + 0.50 x severity) / 1.0`
- span factor = min(span days, 30) / 30, so a single observation earns 0 here, however old it is.
- recurrence factor = min(counted observations, 6) / 6.
- severity factor = highest counted severity (low 1, medium 2, high 3) / 3.
Weights live in `WEIGHTS` at the top of the script. The result is rounded and bounded to 0 to 100. Resolved hotspots are listed last, shown greyed, and excluded from the open and high-priority counts. The score is a ranking aid, not a validated health risk or official urgency rating.

## Locality support
Locality options come from three defaults plus every locality in saved reports, so any place can be entered. The overview map is schematic and does not show real positions.

## Testing
Automated jsdom checks cover loading, submission, persistence, grouping, duplicates, scoring, filters, CSV, status changes, reset, bad URLs, denied geolocation and unavailable storage. Not tested: photo upload, real browser print preview, real geolocation, and mobile layouts. Run the manual checklist for those.

## Tech
Single-file HTML, CSS and vanilla JavaScript. Data lives in localStorage under `loopzero.v1`. The data layer (`load`, `save`, `buildHotspots`) is separate from rendering so a shared backend can replace it.

## AWS deployment
Not yet deployed. To deploy: zip this folder (or push to a Git repo), open AWS Amplify Hosting, choose "Deploy without Git" or connect the repo, and upload. No build settings are needed.

## Known limitations
Data is per browser and per device. No shared backend, authentication, or authority integration. Demo data is fictional and labelled. Originally planned as React, TypeScript, Vite and Tailwind; this version is plain JavaScript to ship a complete demo quickly.

## Next steps
Shared backend (DynamoDB behind API Gateway), image storage in S3, a ward-level pilot with local volunteers, and a review queue for duplicate flags.
