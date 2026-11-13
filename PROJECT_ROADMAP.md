# Jets Performance Lab 2026 — Project Roadmap

_Last reviewed: 13 November 2026 (UTC)_

## Current delivery status

- The private analytics repository and separate public dashboard publishing workflow remain in place.
- Latest verified full refresh before this review: [GitHub Actions run 43393191893](https://github.com/Fixedwing801/jets-performance-lab-2026/actions/runs/43393191893), completed successfully on 13 November 2026 at 08:26 UTC.
- The workflow's data build, historical coverage, forecast, pressure, player/personnel, dashboard assembly, private artifact and public dashboard publication stages completed successfully.
- The workflow runs metric-denominator and player-identity unit tests before downstream analytics.

## Data quality snapshot

From `data/processed/build_metadata.json` generated 13 November 2026 at 08:26 UTC:

- 24,002 source play-by-play rows across weeks 1–10.
- 16,864 eligible run/pass scrimmage plays.
- Zero missing EPA values and zero missing success values among eligible scrimmage plays.
- 274 rows with missing EPA are classified as unknown/non-scrimmage play type and are excluded from EPA/play.
- Zero duplicate game/play keys.
- 18 Jets game-side records, representing nine Jets games through week 9; week 10 is present in the league feed but not as a Jets game.

The NFL team comparison contains all 32 teams. Its current season-to-date ranks place the Jets 15th in offensive EPA/play and 22nd in defensive EPA allowed/play (lower defensive EPA allowed is better). Ranks are descriptive of the available play sample, not opponent-adjusted standings.

All 14 tracked core/enrichment feeds were marked available in the latest source-status manifest. An unchanged feed is not assumed to be freshly republished: each source retains its own last-successful timestamp.

## Historical coverage intelligence

- Participation/play-by-play joins are available for 2016–2025.
- Directly charted man/zone and coverage-shell labels are present from 2018–2025.
- The 2016 and 2017 joins contain no usable coverage labels; those seasons must not be represented as labelled coverage evidence.
- The latest labelled season is 2025. No 2026 coverage calls are available from the free public participation feed before the postseason release.
- Coverage labels are never inferred from ordinary play-by-play. The 2023 provider transition (NFL Next Gen Stats to FTN Data via nflverse) is a methodological break.
- The coverage build now records `labelled_seasons` and `available_but_unlabelled_seasons` separately and explains the distinction in the dashboard.

## Reliability and analytical safeguards

- EPA/play uses run/pass scrimmage plays with non-null EPA only.
- Rates are aggregated using their own valid denominators.
- Team offensive EPA ranks high-to-low; defensive EPA allowed ranks low-to-high.
- Player ID resolution uses exact normalized names first. Initial+surnname fallback is restricted to genuinely abbreviated snap names and remains disabled when the alias is ambiguous.
- The EPA chart panel's existing layout and styling remain locked. No chart-panel layout changes are authorised by this roadmap.

## Completed in this review

1. Verified the latest full workflow run and checked the earlier failed test run.
2. Confirmed that the earlier player-crosswalk test failure is resolved on the current main branch; the latest completed workflow test stage passed.
3. Tightened initial+surnname matching so a full player name cannot be assigned to another player merely because their first initial and surname match.
4. Added regression tests for abbreviated-name matching, full-name false matches, and ambiguous initial+surnname aliases.
5. Added explicit coverage-label season availability to the historical coverage manifest and dashboard note.

## Next priorities

1. Add automated assertions for all-32-team completeness, team-rank completeness, weekly/game denominator consistency and expected Jets game counts.
2. Reconcile offensive and defensive player identity coverage against roster, weekly stats and snap-count data; report unresolved IDs rather than forcing matches.
3. Review Jets offensive and defensive performance by game, down, field zone, score state and opponent baseline. Keep opponent adjustment descriptive.
4. Review PFR pressure/drop/missed-tackle metrics and ESPN QBR against primary nflverse player/game data, documenting sample and identifier coverage.
5. Validate the published dashboard at mobile and desktop widths without changing the locked EPA chart panel.
6. Continue assessing free charting/participation sources for 2026 coverage and personnel. Do not ingest data unless licensing permits the intended automated use and redistribution.

## Model caveats and blockers

- The current team EPA forecast is a descriptive baseline, not a calibrated probability model. Its latest backtest does not beat the league-average baseline consistently across offense and defense; retain the league baseline comparison and avoid claiming a predictive edge.
- The current 2026 free play-by-play feed lacks explicit defensive coverage assignments and complete on-field player participation. No individual defender responsibility, coverage call, or personnel-package attribution should be inferred.
- Paid NFL Pro/NFL+ data and sources without suitable reuse rights remain excluded.
- No purchase, subscription, trial, or paid API is authorised.

## Next validation gate

A full scheduled/manual workflow must pass after the current regression-test and coverage-manifest changes. Only then should new dashboard metrics be promoted from experimental to standard reporting.
