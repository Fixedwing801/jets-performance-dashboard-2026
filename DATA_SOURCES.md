# Data sources

## Core play-by-play
- nflverse play-by-play: https://github.com/nflverse/nflverse-data/releases
- nflverse data dictionary: https://nflreadr.nflverse.com/articles/dictionary.html
- Core 2026 PBP is checked on every scheduled refresh. Downloads are validated before atomic replacement; the last known-good file is retained on source failure.

## Free supplementary feeds retrieved by the pipeline
- PFR snap counts: weekly player participation and snap share.
- Weekly rosters: position, team and stable player-ID crosswalks.
- Injury reports: practice and game availability.
- NFL Next Gen Stats: quarterback, receiving and rushing tracking metrics, including separation/cushion and yards over expected where published.
- FTN charting via nflverse: charted personnel, formations, motion, play action, pressure and coverage fields when released.
- PFR weekly advanced statistics: passing, rushing, receiving and defensive player-level context.
- ESPN Total QBR: a separate quarterback metric for context alongside passer rating, EPA and tracking data.

## Availability and update cadence
The pipeline checks these releases every six hours during the NFL season. Upstream feeds have different publication schedules: cleaned PBP is updated after game days and may receive midweek corrections; FTN charting and PFR snap/advanced-stat feeds are polled several times daily; NGS, rosters and injuries generally update daily. The dashboard cannot show a feed before its provider publishes it.

## Coverage limitations
- Historical coverage labels are available where directly charted, but the public FTN participation release from 2023 onward is published after the postseason rather than live during the regular season.
- No 2026 play-level coverage shell or man/zone field is inferred from standard PBP.
- Public team-level coverage summaries are kept separate from play-level EPA and are not treated as coverage effectiveness data.

## Validation and licensing
Source files are schema-checked before replacing cached copies. Failed optional feeds are marked unavailable; an existing valid copy is retained and marked as last-known-good. Each source's retrieval time, schema, size, status and error are recorded in `data/processed/source_status.json`.

Source availability and schema can change. nflverse distributes datasets under its stated terms and source-specific attribution/licensing conditions. In particular, FTN charting data retains FTN's attribution and licence requirements. Do not treat the general nflverse software licence as a blanket licence for every underlying source. No access controls are bypassed.
