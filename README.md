# Astrolytics: Flame in Freefall

An interactive dashboard for the NASA Space Apps Challenge **Flame in Freefall**. It compares NASA's space-fire experiments with the air in Earth, ISS and Moon habitats, and shows **what has been tested and what is missing**.

**Live site:** `https://bndraljedani.github.io/<repository-name>/`

## The problem

Moon bases will likely run on 30% oxygen or more, and materials burn more easily in that air. NASA's fire results are spread across 24 investigations in NASA's PSI database, so it is hard to see what has actually been tested.

## What it does

1. **Pick a place:** Earth, ISS, Moon base, or your own habitat.
2. **See what NASA tests match it:** a Fire Map, the nearest real tests, and ranked investigation cards.
3. **See what's missing:** a Gap Panel at the top of each place page, marked Missing, Thin or Covered.

Pages:

| Page | What is on it |
|---|---|
| Fire Map (home) | Intro, timeline of past space fires, and the Fire Map: oxygen % against pressure (psi), one dot per test. Hatched areas have no test. |
| Earth, ISS, Moon base | Gap Panel, "What this means", 20 investigation cards with score breakdowns, outcome by oxygen level, closest real tests. |
| Custom habitat | Sliders for oxygen, pressure and gravity, presets, live "oxygen to breathe", a purple "Your habitat" star on the map, and a live Gap Panel and ranking. |
| Sources & cleaning | All 20 investigations with PSI links and DOIs, the cleaning log, assumptions, and what was left out. |

Every test can be selected to see its measurements and traced to its PSI investigation, table file, CSV line number and original row. Tests can be filtered by study and outcome, and the filtered list can be downloaded as CSV.

## Run it

It is one self-contained file with all data embedded and no external requests.

- **Locally:** open `index.html` in a browser.
- **GitHub Pages:** put `index.html` in the root of the repository, then go to Settings → Pages → Deploy from a branch → `main` / `(root)` → Save.

## Data

Built from NASA Physical Sciences Informatics (PSI) experimental tables, read on 13 November 2026.

| Plotted on the Fire Map | PSI ID | Tests |
|---|---|---|
| FLEX (droplet flames) | PSI-69 | 274 |
| CFI-G normal flames (gas flames) | PSI-159 | 179 |
| BASS-II (real materials) | PSI-25 | 129 |
| Saffire-I and II (real materials) | PSI-98, PSI-99 | 11 |

Cleaning and assumptions (full list on the Sources & cleaning page):

- Pressure is converted to psi (FLEX from mmHg, CFI-G from bar).
- Missing values show "no value recorded" and are never turned into 0. One FLEX test has a pressure of 0 mmHg, which is impossible, so it is treated as missing and is in the table but not on the map.
- Outcomes are grouped by us from each table's own end codes: went out, broke apart, kept burning, did not ignite. The original word is always shown in the inspector.
- BASS-II and Saffire have no pressure column, so they are drawn at the nominal 14.7 psi cabin pressure and marked with an asterisk. BASS-II outcomes are free text and are not scored.
- CFI-G inverse flames, ACME daily ignition counts and other investigations are not plotted. See the Sources page.

## How the investigation score works

Score out of 10 = **Part A** (does it match this place? 3) + **Part B** (is it useful for fire safety? 7). It is a visible formula, not an AI judgement.

- Oxygen (0–1) and Pressure (0–1): how close the tests are to this place's oxygen and pressure.
- Gravity (0–1): microgravity tests match the ISS, only Earth-gravity data matches Earth. No PSI test was run at Moon or partial gravity, so on those pages no investigation gets this point.
- What burned (0–3): real material 3, fuel droplet 1, gas flame 0.
- Air moving (0–2): moving air 2, still air 0.
- Real data (0–2): a result for every test 2, test data without results 1, log, plan or summary 0.

The breakdown is shown on every card. The full wording is under "How the score works" on each place page.

## AI use

Claude (Anthropic) helped clean the PSI tables, wrote the investigation summaries and wrote the "What this means" text. A team member checked all 20 investigation summaries against PSI and NASA sources (the ✓ tag on each card). Scores and gap counts are plain formulas run on the data, not AI.

## Limitations

- A gap means "not in PSI", not "nobody has ever tested it".
- All plotted flame tests are droplet or gas flames in microgravity. Real-material outcomes are not scored.
- The Fire Map groups of oxygen and pressure use our own tolerance (within 4 points of O₂ and 1.5 psi) for "near this air". Gap labels use a 20-test threshold for Covered.
- Moon gravity is untested in PSI. NASA's FM2 experiment is planned to test it.
- Timeline events are public history, not PSI data.

## Sources

- NASA PSI: `https://psi.nasa.gov/physci/repo/data/investigations/PSI-<ID>`
- Ferkul, Kralik & Liao, "Material Flammability at Lunar and Martian Gravity" (2026), NTRS 20260000646.
- Saffire VI results, ICES 2024, NTRS 20240007488.

## Team

Astrolytics, NASA Space Apps Challenge 2026, Jeddah.
