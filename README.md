# LoopZero

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
