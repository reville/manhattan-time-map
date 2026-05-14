# Manhattan Time-Distance Map

An interactive map of Manhattan where distances are measured in **minutes**, not miles.

Pick a starting point. Pick a way to travel (walk, subway, bike, drive). Pick a time budget. Watch how much of the island you can actually reach.

## Live demo

[https://reville.github.io/manhattan-time-map/](https://reville.github.io/manhattan-time-map/)

## What's in it

- **Four travel modes:** walking, subway, biking, driving — each rendered as a separate small map and selectable as the main map.
- **Time-budget slider** with a play/pause button that animates 0 → 60 minutes in a continuous sweep.
- **Traffic estimate** segmented control with five canonical windows: late night, AM rush, midday, PM rush, evening. Driving speeds and subway platform waits both vary with time of day.
- **Click any point** on the map (named origin or subway station) to recompute reach from that point.
- **Hover** to see the model's chosen route from origin to cursor with a per-segment breakdown.

## How it works

Dijkstra's shortest-path algorithm runs over a multi-modal graph:

- ~9,200 nodes: a 70 × 130 grid of cells covering Manhattan plus one node per modeled subway-line-at-station platform.
- Walking, driving, biking, boarding, riding, alighting, and transfer edges, each with a cost in minutes.
- Edges that vary with time of day (drive, subway boarding/transfer) store five window-specific costs.
- Per-(origin, mode, window) Dijkstra results are cached so re-renders during animation reuse computation.

Full methodology is documented inside the page itself.

## Tech

- Single self-contained HTML file. No build step, no backend, no external routing API.
- Pure SVG rendering.
- IBM Plex Sans via Google Fonts is the only external dependency.

## Data sources

- Subway station coordinates and line connectivity: hand-curated from the MTA public station list.
- Per-stop run times: derived from posted MTA schedules.
- Driving speeds: aggregated NYC TLC trip-record averages, NYC DOT and INRIX speed studies.
- Biking speeds: aggregated Citi Bike trip-level averages, NACTO Cycling Design Guide.
- Manhattan polygon: hand-traced from open-source basemaps.

## License

Visual experiment by Nicholas Reville. MIT.
