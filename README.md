# World Cup 2026 — Knockout Betting & Ratings Tool

A self-contained, single-file analytics tool for the 2026 FIFA World Cup knockout
rounds. Open `index.html` in any browser — there are **zero external dependencies**
(no CDNs, no API calls, no build step). All model code and data are baked in.

Live: `https://<username>.github.io/<repo>/`

## What's inside

- **Matches** — our Elo→Poisson fair line shown next to a third-party feed, with
  per-side EV, vig, a ★ where both models beat the market, a goals/BTTS breakdown,
  a to-advance line (incl. extra time + penalties), and a "log prediction" button.
- **Matchup Lab** — run the full model on *any* two of the 48 teams, with a
  neutral/home toggle (+100 Elo) and an EV + Kelly stake sizer.
- **Title Odds** — a 20,000-run Monte Carlo over the real, locked knockout bracket
  for each team's chance to reach every round and win the trophy, with no-vig fair
  outright prices.
- **Parlay** — correlation-aware ticket pricing (same-match legs use the true joint
  Poisson probability, not naive multiplication) with profit-boost math.
- **Calibrate** — log predictions before kickoff, settle by final score, and score
  the model honestly (Brier vs the feed, calibration curve, closing-line value).
  Persists to the browser (localStorage) once hosted; exports/imports JSON.
- **Method** — full, honest writeup of how every number is built and its limits.

## How the model works

Two pieces, each from the best source: **World Football Elo** (eloratings.net) sets
who's favoured via a result-expectancy curve split into win/draw/win; **attack/defence**
goal rates (regressed for the short sample) set the match total, which feeds a Poisson
scoreline grid that every market reads off of. To-advance adds extra time (Poisson at
~1/3 pace) and a 50/50 shootout.

## Honest limits

Neutral site on the Matches tab (hosts under-rated; use the Lab's home toggle).
Over/Under and BTTS are directional (3–4 game samples). The model leans on Elo gaps,
so it concentrates title probability on the top seeds more than the market does. It is
not back-tested yet — that's what the Calibrate tab is for. Decision support, not advice.

## Updating

It's one file. Edit `index.html`, commit, push — Pages redeploys automatically.

## Data sources

World Football Elo (eloratings.net, via footballratings.org), FBref squad goalkeeping /
standard / shooting tables, and the official FIFA knockout bracket (verified against the
Annex C third-place-assignment table). Current as of the 2026 Round of 32.
