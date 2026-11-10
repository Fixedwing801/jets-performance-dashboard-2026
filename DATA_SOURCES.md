# Data sources

## Core
- nflverse play-by-play: https://github.com/nflverse/nflverse-data/releases
- nflverse data dictionary: https://nflreadr.nflverse.com/articles/dictionary.html

## Optional enrichment
- nflverse snap counts, weekly rosters, player statistics and injury reports.
- FTN charting via nflverse, when the season/week is published.
- NFL Next Gen Stats public leaderboards for tracking-derived metrics; no assumed bulk API.
- Pro Football Reference and ESPN for supplementary context, subject to access and reuse terms.

## Constraints
Source availability and schema can change. Each downloaded feed is optional and its status is recorded in `data/raw/supplementary_manifest.json`. No access controls are bypassed and no unavailable charting fields are inferred from standard play-by-play. Use stable player IDs for joins.
