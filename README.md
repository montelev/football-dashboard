# Football Player Analytics Dashboard

A single-page, zero-dependency web dashboard that turns raw football player
data into visual insights. It runs entirely in the browser from a CSV file and
can optionally pull live player statistics from the [API-Football](https://www.api-football.com/)
REST API.

**Live demo:** https://YOUR-USERNAME.github.io/football-dashboard/
*(replace with your GitHub Pages URL)*

<!-- Add a screenshot: drop an image named screenshot.png in the repo, then this will display it -->
![Dashboard screenshot](screenshot.png)

---

## What it does

Pick a player and the dashboard shows their profile, key stats, and a visual
breakdown, plus an auto-generated written analysis of their strengths and
weaknesses. A searchable, sortable table lists every player in the dataset.

### Features

- **Player profile** — name, club, colour-coded position badge, and an
  auto-generated initials avatar.
- **Stat cards** — goals, assists, appearances, minutes, and pass accuracy.
- **Stat visualisation** — a bar chart (normalised across the dataset) and a
  radar chart, with a toggle to switch between them.
- **AI insights panel** — a rule-based engine that compares each player's stats
  against the squad averages and generates position-aware sentences (e.g. a
  defender's goals are judged differently from a forward's). No API key or
  external model required — it runs offline.
- **Live search** — filter players by name, team, or position in real time.
- **Sortable table** — click any column header to sort ascending/descending.
- **Live data fetch (optional)** — pull real player stats from API-Football,
  with a clean fallback to the bundled CSV if the request fails.
- **Dark theme** — built with CSS variables for easy re-theming.

---

## Tech stack

| Layer        | Choice                                             |
|--------------|----------------------------------------------------|
| Markup/Style | HTML5, CSS3 (custom properties, no framework)      |
| Logic        | Vanilla JavaScript (ES6+), no build step           |
| Charts       | Hand-built SVG (no charting library)               |
| Data         | Local CSV file, optional REST API                  |
| Hosting      | Static — deployable on GitHub Pages                |

The entire app is a single `index.html` file with no dependencies, no bundler,
and no backend. This keeps it portable and easy to host anywhere that serves
static files.

---

## Running it locally

Because the app loads `players.csv` with `fetch()`, it must be served over HTTP
— opening `index.html` directly with a `file://` path will be blocked by the
browser and the data won't load. Use any static server:

```bash
# Python (built in on most systems)
python -m http.server 8080
# then open http://localhost:8080

# or, if "python" isn't found:
python3 -m http.server 8080
```

Leave the terminal running while you use the dashboard; closing it stops the
server.

---

## Using live data (optional)

The dashboard can replace the sample CSV with real player statistics from
API-Football.

1. Create a free account at
   [dashboard.api-football.com/register](https://dashboard.api-football.com/register)
   (no credit card required).
2. Copy your API key from the dashboard.
3. In the app, paste the key into the **API-Football key** field, choose a
   league and season, and click **Fetch Live Data**.

The fetch pulls the season's top scorers and top assists, merges and
de-duplicates them, and rebuilds the dashboard with that live data.

**Notes on the free tier:**
- ~100 requests per day; one fetch uses 2 requests.
- Available seasons are limited (roughly the last few completed seasons). If you
  pick a season outside the allowed range, the app shows the error message and
  falls back to the CSV data rather than breaking.

### A note on the API key

The key is **never written to any file or committed to this repository.** It is
entered at runtime and stored only in your browser's `localStorage`. Do not hard-code
API keys into source files or share them — if a key is exposed, rotate it from
the API-Football dashboard.

---

## Data format

`players.csv` uses the following columns. To use your own data, match this
header row exactly:

```
name,team,position,goals,assists,appearances,minutes,pass_accuracy
```

| Column          | Type    | Notes                                  |
|-----------------|---------|----------------------------------------|
| `name`          | text    | Player full name                       |
| `team`          | text    | Club name                              |
| `position`      | text    | Forward, Midfielder, or Defender       |
| `goals`         | number  |                                        |
| `assists`       | number  |                                        |
| `appearances`   | number  |                                        |
| `minutes`       | number  | Total minutes played                   |
| `pass_accuracy` | number  | Percentage, 0–100                      |

---

## Project structure

```
football-dashboard/
├── index.html      # The entire app: markup, styles, and logic
├── players.csv     # Sample dataset (20 players)
└── README.md       # This file
```

---

## How it was built

This project was built as a hands-on exercise in turning data into a working
application. AI-assisted development tooling (IBM Bob) was used to scaffold and
iterate quickly; all generated code was reviewed, tested, and validated before
deployment.

---

## License

Free to use and adapt. Sample player data is fictional.
