# Jets Game Review and Matchup Intelligence

## Purpose

This workflow creates a repeatable, source-backed review after every Jets game and records what the team actually did against a pregame statistical reference. It supplements, rather than duplicates, the existing offensive, defensive, player-production and matchup pages.

## Data products

- `jets_game_review.csv`: one row per Jets game and side (offence / defence), including actual overall, passing and rushing EPA/play; success and explosive-play rates; third-down and shotgun context; pregame component baselines; expected EPA/play; and actual-minus-expected differences.
- `jets_game_review_players.csv`: leading offensive production and defensive disruption contributors for the latest completed Jets game, with recorded snap exposure and source-presence fields.
- `jets_game_review_status.json`: build timestamp, coverage counts and explicit limitations.

## Pregame baseline methodology

For each Jets game in week N, use only team-week rows from weeks earlier than N. For the Jets offence, calculate the play-weighted season-to-date Jets offensive EPA/play and opponent defensive EPA allowed/play, then take their equal-weight mean. Repeat separately for passing and rushing, using the corresponding play denominators.

For the Jets defence, combine the Jets' prior defensive EPA allowed/play with the opponent's prior offensive EPA/play. This produces a descriptive matchup benchmark, not a calibrated prediction of game score or win probability. Week 1 has no prior-season sample and therefore has no pregame baseline.

The comparison direction is explicit:
- Offence: actual EPA/play above the baseline is favourable.
- Defence: actual EPA allowed/play below the baseline is favourable.

No future game data is included in a game's baseline.

## Player and personnel attribution

Player production tables show leaders and recorded snap exposure. They do not claim causal impact. A missing weekly player-stat row is not converted to zero. Existing snap deployment and position-group outputs remain descriptive and must not be presented as exact on-play personnel combinations.

## Known limits

- Game-level EPA, success and explosive rates are sourced from the Jets play-by-play build.
- The current game summary does not attribute each play to a specific coverage call, individual defender, formation or exact personnel grouping.
- Down-by-down rates currently exist as season-level aggregates; this report does not relabel them as single-game splits.
- Red-zone efficiency and scoring-drive attribution require validated game-level red-zone/drive fields and are not fabricated from total yardage or final score.
- If a required source or game record is missing, the dashboard states that the review is unavailable rather than filling values with zero or carrying forward stale numbers.

## Dashboard and deployment

The review is inserted into the existing Game Analysis page and published through the current private analytics to public dashboard workflow. It does not modify the locked EPA chart panel.
