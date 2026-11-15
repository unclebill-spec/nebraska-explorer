> **Before any work here:** read /workspace/RESOURCES.md (team rules), your /workspace/bot-tools/<slug>.md tool list, and the game order in /workspace/NAMES.md. (Will, Nov 1, 2026)

# Nebraska Explorer — agent handoff

Static Leaflet map, same shared app as the other state explorers. This folder was copied from Utah (which was copied from Idaho) on Nov 14 2026 and then filled with Nebraska base data. `explorer/build.py` `STATE` comes from `scripts/port_build.py --restate` (marker PORT_ST). The state in every script is the folder name via `scripts/common.py` (NE, FIPS 31, 93 counties, `ls` prefix `nex_`, service-worker prefix `nex-`).

Not published. No GitHub repo was created. `scripts/sync_shared.sh` was not run: Kentucky `explorer/app.js` was not edited. Shared `BST_NAME` already includes Nebraska.

Live check when published: `share/county-douglas.html`. Lock: `/tmp/nex_publish.lock`. Repo slug would be `nebraska-explorer`.

## Caps
5+ acres, 1+ acre, and near-hospital: under $550,000. Houses/Towns (`nlh` / `tha`): $350,000. No cabin category.

## Blocks
93 counties (`data/statewide/raw/ne_blocks_500k.zip`).

## What is built (Nov 14 2026, ~16:33 ET)
Preliminary `python3 explorer/build.py` succeeded: 93 counties, 91 hospitals (87 in-state + 4 border), 1,094 schools, 41 colleges, 70 activities, 6 airports, 35 attractions, appeal for 93 counties, climate, compare areas for Omaha, Lincoln, Grand Island, Kearney, and North Platte. Homes, permanent jobs, travel jobs, for-sale, history, ski, border, Target, big-land, and cave/falls layers are not in this build.

Trauma source: Nebraska DHHS "Nebraska Trauma Designated Hospitals" PDF (updated 1/10/2025) plus 2026 news that Regional West Medical Center, Scottsbluff, moved II → III. Children's Hospital & Medical Center, Omaha, is Pediatric Level II and is not pinned. Details and skips: `/workspace/nebraska/STATUS.md`.

## How to rerun
Pandas and geopandas scripts need a venv. `/workspace/kentucky/.venv/bin/python` is not on this machine. The run on Nov 14 used `/tmp/plains/venv` (`python3 -m venv --system-site-packages` plus `pip install geopandas`). Other scripts use `/usr/bin/python3`.

Do not run `forsale`, `perm_jobs`, `travel_jobs`, `listings_build`, or `publish.sh` until those jobs are assigned. Do not import `perm_jobs` (it loads counties and hospitals) or `travel_jobs` (it reads `explorer/data/data.js`) just to check them. `scripts/build_hospital_systems.py` has an early exit for this folder that groups `data/hospitals.json` and does not import Vermont `spec.py`.

RN wages: O*NET May 2025 state median only (`data/statewide/raw/rn_oews2025.csv`). BLS county HTML returned HTTP 403. Do not invent county or metro wages.

Nominatim cache used here was `/tmp/plains/nominatim.json`. A 403/429 must stop further Nominatim calls. Gazetteer place centers are the fallback.
