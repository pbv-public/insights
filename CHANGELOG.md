# Insights Schema Changelog

## [v4.10.0](https://github.com/pbv-public/insights/releases/tag/v4.10.0) on 2026-May-02
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v4.8.0...v4.10.0?expand=1)
> * Version Checksums: Functional=8470e2fee482e4053e273bac018e34f2 Full=6098d50aa71e373cb2a6e05882806bf7

- Added `player_data.positional_performance` containing `forward_pressure` (team-level Push, [0, 1]) and `finishing_ability` (team-level Close, [0, 1]) — measures of how actively a team drove each shot toward a positional advantage and how efficiently they converted advantage into ending the rally, both independent of rally outcomes. Both teammates share the same value; team 1's value is the complement of team 0's. Omitted for singles or when too few supported rallies are available.
- Added `shot.quality.pressure` ([0, 1]) — positional pressure faced and imposed by the shot. Omitted for singles, serves, returns, or when positioning data is unavailable.
- Added `shot.shooter_positioning_score` and `shot.partner_positioning_score` ([0, 1]) — Stage 2 causal-frontier positioning quality scores at the moment of the shot. Omitted for singles, serves, returns, or when positions are outside the model's supported domain.
- Updated `shot.advantage_scale` semantics. In doubles it is now derived from a state-value model that estimates rally win probability from four-player positions (well-calibrated; ~0.3 win-prob at 0, ~0.7 at 1; teammates share, opponents are the complement). For singles, the legacy y-axis depth heuristic is preserved for ratings compatibility (server's value hardcoded to 0 on the serve, unused player slots null). Doubles scores are omitted when positions are outside the model's supported domain.
- Removed `scoring_info.likely_correct_score`. The field was obsoleted by the new FB-scoring confidence work and is no longer produced.

Documentation updates after initial release:

- Documentation: clarified `shot.is_putaway` to make it explicit that the field covers any clean rally-ending winner or strong/decisive attacker — including well-placed dink and drop winners — not only hard-hit shots.

-------------------------------------
## [v4.8.0](https://github.com/pbv-public/insights/releases/tag/v4.8.0) on 2026-Feb-26
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v4.7.0...v4.8.0?expand=1)
> * Version Checksums: Functional=a62a282983e7b0900417d95e91a48300 Full=830f8bef8a3080339817e6a9f0ab441b

- Added `team_kitchen_arrival` to player data with team-level kitchen arrival stats (numerator/denominator counts for serving and returning roles, where both teammates had a fair opportunity to arrive at the kitchen)

-------------------------------------
## [v4.7.0](https://github.com/pbv-public/insights/releases/tag/v4.7.0) on 2026-Jan-08
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v4.5.1...v4.7.0?expand=1)
> * Version Checksums: Functional=291a709535e29f5ced31fed3efc094b9 Full=5ebf77610575d74ee5f39e5b79f14887

- Added `stats` object for the general technical stats about each player

-------------------------------------
## [v4.5.1](https://github.com/pbv-public/insights/releases/tag/v4.5.1) on 2025-Dec-22
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v4.4.0...v4.5.1?expand=1)
> * Version Checksums: Functional=b497cf9cf744adb6f90b1fd615775a66 Full=cbb7bc1d480b843236c834c1fd6ed53e

- New field, `advantage_scale`, with a positional 0-1 advantage score for each of the players at the time of the shot.

-------------------------------------
## [v4.4.0](https://github.com/pbv-public/insights/releases/tag/v4.4.0) on 2025-Nov-12
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v4.1.0...v4.4.0?expand=1)
> * Version Checksums: Functional=8696830ac25d67633b2f0def7501f1b1 Full=fbb8618415ddd96c1b24a9738fc65817

- New structure, `kitchen_arrival_percentage`, with a new, improved algorithm for calculating the percentage of fair-chance kitchen arrivals.

-------------------------------------
## [v4.1.0](https://github.com/pbv-public/insights/releases/tag/v4.1.0) on 2025-Sep-18
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v4.0.0...v4.1.0?expand=1)
> * Version Checksums: Functional=3d2ab529f4c4298df9772505d49928e5 Full=dc4c21fc37f366c9fa668b1bfbe11d29

- Unforced errors and putaways are supported now

-------------------------------------
## [v4.0.0](https://github.com/pbv-public/insights/releases/tag/v4.0.0) on 2025-Aug-07
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v3.2.0...v4.0.0?expand=1)
> * Version Checksums: Functional=df12e7f526fcf8958c541b16aa3d18f6 Full=2369c3227e7d5d60a2f44e01f05c6306

- Multi-session videos support
- Most important change is in the URL structure, now it contains the session ID: instead of /{video_id}/stats.json it is now /{video_id}/{session_id}/stats.json, where session_id is 0-based index of the session in the video. Client can iterate through sessions using the session_id until it gets 404 Not Found.

- `avatar_id` field is added to player_data, and it uses in the player avatar URL: /{video_id}/{ai_engine_url}/player{avatar_id}-[1-4].jpg are the four avatars for this player

-------------------------------------
## [v3.2.0](https://github.com/pbv-public/insights/releases/tag/v3.2.0) on 2025-Jul-14
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v3.0.0...v3.2.0?expand=1)
> * Version Checksums: Functional=6ac23651ef1a88f71d8695d1a4cdbc34 Full=be0bac0a6d4c0b916265dc47207fa695

- Replaced `ms_to_kitchen` with `kitchen_arrivals` array containing detailed kitchen line periods with `since_ms`, `until_ms`, and `ft_moved` vector data
- Added `team_stats` array to rallies with `average_ft_between_players_along_x` and `x_distance_optimality` metrics for doubles games
- Added `shooter_movement_from_last_shot` vector to track player movement between shots, using the new 2d `vector` type
- Added `player_positions` array with x/y coordinates for all players at shot timestamp
- Docs updates: dead_dink is "not supported, not planned", for the `kitchen_arrival` we specify that we consider only "rallies with at least 3 shots"

-------------------------------------
## [v3.0.0](https://github.com/pbv-public/insights/releases/tag/v3.0.0) on 2025-Jun-02
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v2.9.0...v3.0.0?expand=1)
> * Version Checksums: Functional=d4c0ff2080d78309f29dddb1ceb9b438 Full=45c2392114d7552766f960577df50dd0

- Add ratings data structures for players' ratings and their trends

-------------------------------------
## [v2.9.0](https://github.com/pbv-public/insights/releases/tag/v2.9.0) on 2025-May-17
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v2.7.0...v2.9.0?expand=1)
> * Version Checksums: Functional=7eb56e3b1df0f99ed717edcc6cc6a7a2 Full=9096be46e17cf16b981bd2f54497a34a

- Running score properties moved to rallies[*].scoring_info.running_score, with server_number added for doubles games
- Added start_ms and end_ms timestamps to track shot duration for shots without the resulting_ball_movement
- Updated popup error definition with more specific criteria
- Changed description of average_x_coverage_percentage to clarify it's only relevant for doubles games, made it optional
- Added corrected boolean flag to worldPosition3D to indicate post-CV corrections

-------------------------------------
## [v2.7.0](https://github.com/pbv-public/insights/releases/tag/v2.7.0) on 2025-Mar-12
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v2.6.0...v2.7.0?expand=1)
> * Version Checksums: Functional=b483a45020c6d31b7c782f354e2f8a49 Full=c2a595e98e836f111a87afd94e7272ae

- .running_score and the related properties have been moved to rallies[*].scoring_info.running_score, there's also .server_number there for the doubles games

-------------------------------------
## [v2.6.0](https://github.com/pbv-public/insights/releases/tag/v2.6.0) on 2025-Jan-23
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v2.5.0...v2.6.0?expand=1)
> * Version Checksums: Functional=0b322cd2cf0745aea8ae46ad0859c78b Full=d625ecc9493936cf77728e2e1b6b1522

- Rally scoring is now supported. Game data contains new attributes, `scoring` and `min_points`, that define the scoring rules for the game.
- New attribute for the rally, running_score, that computes the running score according to the scoring rules chosen.

-------------------------------------
## [v2.5.0](https://github.com/pbv-public/insights/releases/tag/v2.5.0) on 2025-Jan-15
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v2.4.0...v2.5.0?expand=1)
> * Version Checksums: Functional=9724ecf81c1a14ded5502331cdf7d4ea Full=ae5cd03c59147ffe2430176f3da09848

- Exposed "Coach advice" in the Insights, an array of advice for each player, ordered by their relevance.

-------------------------------------
## [v2.4.0](https://github.com/pbv-public/insights/releases/tag/v2.4.0) on 2024-Dec-03
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v2.3.0...v2.4.0?expand=1)
> * Version Checksums: Functional=8c6827137c0d55e74d409cb6fe0fb007 Full=80733506977ad40ea6ff3ffd8be29547

- Added `likely_bad` attribute to a rally to indicate that it shouldn't be used for calculating running scorie.
- In general, scoring is available now, so the scores will be reported numerically in `game_outcome`.

-------------------------------------
## [v2.3.0](https://github.com/pbv-public/insights/releases/tag/v2.3.0) on 2024-Nov-20
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v2.3.0...v2.3.0?expand=1)
> * Version Checksums: Functional=930d478af5b91cae8ed3692e6b489b21 Full=b0b782c0afabfe613e411ae3f1100f9b

- Back to the clean version of the schema

-------------------------------------
## [v2.3.0](https://github.com/pbv-public/insights/releases/tag/v2.3.0) on 2024-Nov-20
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v2.0.2...v2.3.0?expand=1)
> * Version Checksums: Functional=5df30212fd212b8189bcd17f96e1a054 Full=b4682f7b86a457592fb79167e6308b2b

- Deploy a dummy version to be able to bump the version number

-------------------------------------
## [v2.0.2](https://github.com/pbv-public/insights/releases/tag/v2.0.2) on 2024-Nov-04
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v2.0.1...v2.0.2?expand=1)
> * Version Checksums: Functional=930d478af5b91cae8ed3692e6b489b21 Full=b0b782c0afabfe613e411ae3f1100f9b

- added `session` to indicate game vs. drill and how many participants
- added optional `is_ball_machine` in `player_data`

-------------------------------------
## [v2.0.1](https://github.com/pbv-public/insights/releases/tag/v2.0.1) on 2024-Oct-24
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v2.0.0...v2.0.1?expand=1)
> * Version Checksums: Functional=3bcee1a2cb27e8b63eea4a3e29b79b35 Full=862225a86a48f93bf7939f58db0f5f74

- New fault type: `short`, when the ball fails to cross the net and ends on the server's side.
- Errors are now enum-valued: potential vs exploited.
- Outs are simplified/normalized into a enum that avoids contradictory values.
- Descriptions of errors are updated for the upcoming simplified heuristics

-------------------------------------
## [v2.0.0](https://github.com/pbv-public/insights/releases/tag/v2.0.0) on 2024-Sep-03
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v1.0.2...v2.0.0?expand=1)
> * Version Checksums: Functional=4fb2e9d06f1bafc1a116c5135e300579 Full=93bb77fb9b27fe84cd5960f96f3314e2

- transitioned insights to more purposeful app use
- `rallies` now contains a list of `shots` instead of a list of `moments`
- renamed `game_stats` to `game_data`
- renamed `player_stats` to `player_data`
- `player_data` now contains far fewer key-value pairs

-------------------------------------
## [v1.0.2](https://github.com/pbv-public/insights/releases/tag/v1.0.2) on 2024-Jul-14
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v1.0.1...v1.0.2?expand=1)
> * Version Checksums: Functional=1cba4dc18880f3f04da2aaba302475d2 Full=ee282f8e65a1cea0f12fe74746a77c6e

* add hands battle highlight

-------------------------------------
## [v1.0.1](https://github.com/pbv-public/insights/releases/tag/v1.0.1) on 2024-Jul-07
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v1.0.0...v1.0.1?expand=1)
> * Version Checksums: Functional=f249d9582ff350b9365fb164d65bef20 Full=f4d2b8c72564a926bcb6e10553130a22

- removed unnecessary `shot_zones` from `player_stats`

-------------------------------------
## [v1.0.0](https://github.com/pbv-public/insights/releases/tag/v1.0.0) on 2024-Jun-01
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v1.0.0^...v1.0.0?expand=1)
> * Version Checksums: Functional=65aa09038155ebe0da01cf003c14ebb6 Full=004f27c714b26093898accbdea533e60

initial release

from dev 0.0.12

