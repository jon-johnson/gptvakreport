# Vakaros RaceSense Report App

Static single-file HTML app for analysing a Vakaros RaceSense event.

Configured first for:

- Event: Cape 31 Porto Cervo
- Player URL: `https://player.vakaros.com/watch/Wz4a9bhZz4qmu3Li7Yrm/C31?race-day=3`
- Display label: Day 1, while the source URL uses `race-day=3`

## Features

- Start report
  - Distance to line at gun
  - Speed at gun
  - Acceleration over the final 20 seconds
  - Line position percentage, pin to committee boat, when start-line marks are available
  - OCS flag where available
  - Sortable composite ranking

- Race result report
  - Finish rank
  - Start rank at T+50
  - Places gained/lost
  - Distance sailed
  - Average speed

- Leg statistics
  - Average speed by leg
  - Distance sailed by leg
  - Average absolute heel by leg
  - Race and boat filters

- Start replay mini-map
  - T-60 to T+60 default window
  - T-30, T-10, gun, and T+30 quick buttons
  - Boat highlight
  - Start-line drawing when pin/committee marks are available

## Loading Vakaros data

The app first attempts direct loading from the Vakaros player URL and from candidate API endpoints in the `CFG.endpoints` array inside `index.html`.

Because Vakaros player telemetry may be private, tokenised, or blocked by CORS, the app also includes a fallback import workflow:

1. Open the Vakaros player page.
2. Open DevTools > Console.
3. In this app, click **Copy discovery snippet**.
4. Paste the snippet into the Vakaros player console.
5. Refresh or replay the race.
6. Inspect `window.__racesenseSeen` in the player console.
7. Copy the relevant JSON response or export a HAR file.
8. Paste it into the app under **Fallback import**.

If a stable direct endpoint is found, add it to the `CFG.endpoints` array.

## GitHub Pages

This is a static site. To publish:

1. Go to GitHub repo settings.
2. Pages.
3. Source: Deploy from branch.
4. Branch: `main` / root.
5. Save.

Then open:

`https://jon-johnson.github.io/gptvakreport/`

## Notes

The first version is designed to be robust with unknown RaceSense data shapes. The parser accepts common field names such as `lat`, `lon`, `timestamp`, `sog`, `heel`, `boatId`, `boatName`, `raceId`, and `startTime`, and recursively searches nested JSON/HAR responses.

When explicit course/mark data is unavailable, leg detection falls back to equal-time splits. Manual leg splits are available in the UI for race-by-race correction.
