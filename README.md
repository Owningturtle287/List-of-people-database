# Stranded · Island Register

A fictional survival-world database for a small American cruise stranded in the Pacific. Mobile-first, static, no paid API or real-time simulation.

## Open / install
Enable GitHub Pages in **Settings → Pages → Build and deployment → Source → GitHub Actions** if it is not already enabled. In Actions, run **Build and publish island register**. After a successful Pages deployment open the environment link (usually https://owningturtle287.github.io/List-of-people-database/) in Safari, then Share → Add to Home Screen. The workflow also produces a ZIP of the static site. A ZIP is not an iOS native app.

## Canonical story data
`world.json` is the source of truth for ChatGPT-directed updates. The opening snapshot is day 1 at 07:13, 315 people, no rescue. `minute` is elapsed minutes since day 1 midnight; 433 = 07:13. `revision` increases on every committed world update. Permanent IDs are never reused. Deceased characters remain in the database, with links and logs intact. `links[].type` is the relationship of the referenced person **to** the profile owner; reciprocal links are maintained. Coordinates use a 0–100 island grid with 50 metres per unit (5 km reference grid), not GPS. The south-shore survivor staging areas are within a few hundred metres of each other. The map supports pinch zoom, panning, person search and distance scales. The initial geography and positions are author-created and provisional.

The original manifest was imported in ID order, all original characteristics preserved except unspecified orientations changed to heterosexual by request. Biography expansions and initial thoughts/positions are fictional additions, not original facts.

## Updates through ChatGPT
For each user-directed story turn, read the latest `world.json`, establish the requested absolute day/time, apply the named events/overrides, then use the deterministic engine for unspecified characters or author richer, consistent actions manually. Update every affected person's state, coordinates, headspace and log, add world events, increment revision, and commit the new complete `world.json`. Do not advance time or intervene without instructions. Never invent rescue or erase prior logs. Preserve IDs and previously established canon. The app reads published snapshots; refresh on the Save tab to check. There is no time-control tab in the app: day and time are read-only and ChatGPT directs story updates.

Phone edits are saved locally, **not automatically pushed to GitHub**. Export JSON and send that snapshot to ChatGPT before a subsequent canonical update if you've made local edits. If a newer published revision arrives while there are local edits, the app offers an explicit replace choice, never silently overwrites the draft. Keep backups because iOS may clear website storage. The repository and any published Pages site are public; do not enter real private information.

## Local usage and validation
`node test.js` tests the manifest and deterministic engine. Run `python3 -m http.server 8000` from the root and open http://localhost:8000. No dependencies. The engine offers `advance(state, targetMinute, overrides, worldNote, weather)`, `add`, `patch`, `log`, `locate`, and `validate`. No time passes automatically; procedural activity is rule-based, not a live language model. Each advance is capped at 24 hours; no automatic fatality, resource discovery, or weather changes. Narrative notes are recorded verbatim and do not themselves cause custom AI events.