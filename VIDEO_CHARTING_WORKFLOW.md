# Video charting workflow (Jets Performance Lab 2026)

## Purpose
Use legally accessible Coaches Film supplied by the project owner to produce a structured, auditable manual/AI-assisted charting layer. Video is not uploaded to GitHub or redistributed. Only derived charting metadata and play references are stored.

## Operating model
1. Owner supplies a screen recording or other permitted local video file. The pipeline never signs into DAZN, bypasses DRM, downloads protected streams, or attempts to extract offline app files.
2. A local video-processing step reads the supplied file, samples frames, detects likely shot/camera transitions, and creates a timestamped clip index. The two Coaches Film angles are one play, not two plays.
3. Match the sequence to the game's play-by-play using team possession, play order, event type and distinctive events. Record a match confidence and retain ambiguous matches for review.
4. AI-assisted visual review proposes pre-snap shell, likely coverage family, man/zone/match/unclear, defensive personnel, rush count and visible execution. These are provisional observations, not authoritative play-call labels.
5. Join PBP outcomes (EPA, success, pressure/sack, explosive play, down/distance and result) by game_id + play_id.
6. Export a charting CSV and QA summary. Never fill unknown coverage labels by inference from PBP.

## Important constraints
- GitHub Actions cannot access a user's DAZN session or local phone files. Video analysis must run on an explicitly supplied file in a local/approved processing environment.
- Current ChatGPT video understanding is not a guaranteed fully automated video-classification service. Frame extraction and scene segmentation can be automated; tactical interpretation must retain confidence and review flags.
- Do not upload copyrighted game footage to the repository. Keep video local; publish only derived metadata, subject to the source terms.
- No DRM circumvention, credential sharing, scraping, or paid service is used.

## Pilot: 2026 Week 9 NYJ at KC
The supplied 2m13s Coaches Film recording is associated with the opening Kansas City possession. The first three scrimmage plays are matched by sequence to:
- play_id 465, Q1 06:37, 1st-and-10: Kenneth Walker run for 3 yards, EPA -0.343.
- play_id 487, Q1 06:00, 2nd-and-7: Patrick Mahomes completion to Kenneth Walker for 6 yards, EPA +0.662.
- play_id 523, Q1 05:40, 3rd-and-1: Justin Fields run for no gain, fumble recovered by New York, EPA -5.302.

This confirms a reliable PBP anchor for the drive and its turnover. Exact video in/out timestamps and coverage classifications remain blank until frame-level segmentation and review are completed; they are not fabricated.

## Charting fields
- video_file, video_start_seconds, video_end_seconds
- game_id, play_id, qtr, time, down, ydstogo, play description
- angle_1_assessment, angle_2_assessment
- pre_snap_shell, coverage_family, coverage_type
- defensive_personnel, rushers, blitz
- pressure, result, EPA, success, explosive
- confidence, review_required, notes

## Confidence policy
- High: clear structure and assignment evidence across the relevant angles.
- Medium: likely family is visible but one or more responsibilities are obscured.
- Low/uncertain: camera angle, resolution, cut or disguise prevents reliable classification.
Unknown is a valid value. Do not force a label.
