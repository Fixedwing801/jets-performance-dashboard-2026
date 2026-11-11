# Data sources and reuse review

## Open data used by the pipeline

### nflverse play-by-play
- Releases: https://github.com/nflverse/nflverse-data/releases
- Data dictionary: https://nflreadr.nflverse.com/articles/dictionary.html
- Core 2026 PBP is checked on every scheduled refresh. Downloads are validated before atomic replacement; the last known-good file is retained on source failure.
- nflverse datasets are released with source-specific terms. The project attributes nflverse and underlying providers as required.

### nflverse participation — historical coverage charting
- Documentation: https://nflreadr.nflverse.com/reference/load_participation.html
- Release: https://github.com/nflverse/nflverse-data/releases/tag/pbp_participation
- Play-level fields include `defense_man_zone_type`, `defense_coverage_type`, `defense_personnel`, `number_of_pass_rushers`, `defenders_in_box`, `was_pressure` and primary receiver `route`.
- Seasons currently available: 2016–2025. 2016–2022 participation is attributed to NFL Next Gen Stats via nflverse; 2023 onward to FTN Data via nflverse.
- The participation data is CC BY-SA 4.0. Attribute the relevant upstream provider and nflverse, and ensure adaptations meet the share-alike requirement.
- Crucially, 2023 onward participation is published only after all postseason games are completed. The 2026 play-level coverage labels are not available during the current regular season.
- The workflow joins participation to nflverse PBP by game and play identifiers, then calculates all-team and Jets-specific tendencies and outcomes. Only non-null, directly charted labels are included.

### Other free nflverse feeds
- PFR snap counts: weekly player participation and snap share.
- Weekly rosters: position, team and stable player-ID crosswalks.
- Injury reports: practice and game availability.
- NFL Next Gen Stats: quarterback, receiving and rushing tracking metrics where published.
- FTN in-season charting: personnel/context fields such as motion, play action, RPO, blitzers and pass rushers.
- PFR weekly advanced statistics: passing, rushing, receiving and defensive player-level context.
- ESPN Total QBR: a separate quarterback metric for context alongside passer rating, EPA and tracking data.

## Sources reviewed but not ingested

### NFL Pro / Next Gen Stats Coverage Responsibility
NFL documentation describes assignment-level coverage responsibility and disguise metrics. SportsDataverse documents the NFL Pro endpoints as secured endpoints, and NFL Pro requires NFL+ Premium access. This is not a free, unauthenticated data source and is excluded.
- Overview: https://www.nfl.com/news/next-gen-stats-new-advanced-metrics-you-need-to-know-for-the-2025-nfl-season
- Access/product documentation: https://sportsdataverse-py.sportsdataverse.org/docs/nfl/reference/nflpro

### NFL All-22 / game replays
NFL full and condensed game replays require NFL+ Premium. The project does not use subscription footage, unofficial copies, or automated downloads of copyrighted broadcasts.
- Replay access: https://support.nfl.com/hc/en-us/articles/35869783015444-How-do-I-watch-game-replays

### Sharp Football Analysis
Its terms prohibit automatic or manual monitoring/copying of website material without prior written consent and reserve all content rights. A previous scheduled capture was removed from this project; no Sharp Football values are retained as an ongoing data feed.
- Terms: https://www.sharpfootballanalysis.com/terms-of-service/

### Sports Info Solutions DataHub Free
SIS confirms that a separate free NFL DataHub remains available. Public player pages expose useful defender coverage outcomes such as coverage snaps, targets, completions, completion rate, yards allowed, yards per target, touchdowns allowed, pass breakups, interceptions and Total Points Saved. This is useful as a human-readable cross-check for individual player performance, but it does not provide a verified play-level man/zone or Cover 2/3/4 label on the public player pages.
- Free portal: https://www.sisdatahub.com/
- SIS overview of the free DataHub: https://www.sportsinfosolutions.com/football/
- Example public player page: https://www.sisdatahub.com/players/6367
- DataHub Pro is separate and paid; its seven-day trial is not treated as a continuing free source.
- No automated collection or bulk redistribution is used. The main SIS website terms prohibit automated access and reproduction without permission; the separate free DataHub portal's data-reuse terms were not established in the public documentation reviewed. Use it for manual reference only unless SIS confirms broader reuse rights in writing.

### Second Level Analytics
Its public 2026 defensive leaderboards show player-level targets allowed, completion percentage, yards per target, passer rating allowed, defensive snaps and related coverage outcomes. This can be used as a manual comparison for Jets defensive backs, but it does not identify play-level man/zone or Cover 2/3/4 assignments. No explicit reuse/redistribution licence was established, so it is not scraped or ingested.
- Public leaderboards: https://secondlevelanalytics.com/

### NFL Savant
A useful interactive interface for exploring historical nflverse plays by coverage, personnel and other play-level filters. It is an alternate viewer for existing open data, not an independent 2026 coverage feed.
- Explorer: https://www.nflsavant.com/explore

### Third-party public dashboards
A public page or CSV export is not automatically an open licence. Sites without clear reuse/redistribution terms are treated as human-readable research references only, not ingested into the scheduled pipeline.

## Update cadence and validation
The workflow checks the open nflverse releases every six hours during the NFL season. Upstream feeds have different publication schedules, and no pipeline can provide fields before the provider releases them. Each source's retrieval time, schema, size, status and error are recorded in `data/processed/source_status.json`; historical coverage status is in `data/processed/coverage_source_status.json`.

No access controls are bypassed, no paid subscriptions or trials are used, and no provider quota or account restriction is evaded.
