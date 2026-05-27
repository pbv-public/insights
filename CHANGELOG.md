# Insights Schema Changelog

## [v0.0.36](https://github.com/pbv-public/insights/releases/tag/v0.0.36) on 2026-May-02
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.35...v0.0.36?expand=1)
> * Version Checksums: Functional=8470e2fee482e4053e273bac018e34f2 Full=6098d50aa71e373cb2a6e05882806bf7

- Added `player_data.positional_performance` containing `forward_pressure` (team-level Push, [0, 1]) and `finishing_ability` (team-level Close, [0, 1]) — measures of how actively a team drove each shot toward a positional advantage and how efficiently they converted advantage into ending the rally, both independent of rally outcomes. Both teammates share the same value; team 1's value is the complement of team 0's. Omitted for singles or when too few supported rallies are available.
- Added `shot.quality.pressure` ([0, 1]) — positional pressure faced and imposed by the shot. Omitted for singles, serves, returns, or when positioning data is unavailable.
- Added `shot.shooter_positioning_score` and `shot.partner_positioning_score` ([0, 1]) — Stage 2 causal-frontier positioning quality scores at the moment of the shot. Omitted for singles, serves, returns, or when positions are outside the model's supported domain.
- Updated `shot.advantage_scale` semantics. In doubles it is now derived from a state-value model that estimates rally win probability from four-player positions (well-calibrated; ~0.3 win-prob at 0, ~0.7 at 1; teammates share, opponents are the complement). For singles, the legacy y-axis depth heuristic is preserved for ratings compatibility (server's value hardcoded to 0 on the serve, unused player slots null). Doubles scores are omitted when positions are outside the model's supported domain.
- Removed `scoring_info.likely_correct_score`. The field was obsoleted by the new FB-scoring confidence work and is no longer produced.

Documentation updates after initial release:

- Documentation: clarified `shot.is_putaway` to make it explicit that the field covers any clean rally-ending winner or strong/decisive attacker — including well-placed dink and drop winners — not only hard-hit shots.

-------------------------------------
## [v0.0.35](https://github.com/pbv-public/insights/releases/tag/v0.0.35) on 2026-Feb-26
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.34...v0.0.35?expand=1)
> * Version Checksums: Functional=a62a282983e7b0900417d95e91a48300 Full=830f8bef8a3080339817e6a9f0ab441b

- Added `team_kitchen_arrival` to player data with team-level kitchen arrival stats (numerator/denominator counts for serving and returning roles, where both teammates had a fair opportunity to arrive at the kitchen)

-------------------------------------
## [v0.0.34](https://github.com/pbv-public/insights/releases/tag/v0.0.34) on 2026-Jan-08
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.33...v0.0.34?expand=1)
> * Version Checksums: Functional=291a709535e29f5ced31fed3efc094b9 Full=5ebf77610575d74ee5f39e5b79f14887

- Added `stats` object for the general technical stats about each player

-------------------------------------
## [v0.0.33](https://github.com/pbv-public/insights/releases/tag/v0.0.33) on 2025-Dec-22
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.32...v0.0.33?expand=1)
> * Version Checksums: Functional=b497cf9cf744adb6f90b1fd615775a66 Full=cbb7bc1d480b843236c834c1fd6ed53e

- New field, `advantage_scale`, with a positional 0-1 advantage score for each of the players at the time of the shot.

-------------------------------------
## [v0.0.32](https://github.com/pbv-public/insights/releases/tag/v0.0.32) on 2025-Dec-22
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.31...v0.0.32?expand=1)
> * Version Checksums: Functional=6e6b723125715c123c1233e0f2f8dfb9 Full=93b8b3e118089b4e26a5457af22666f2

- New field, `advantage_scale`, with a positional 0-1 advantage score for each of the players at the time of the shot.

-------------------------------------
## [v0.0.31](https://github.com/pbv-public/insights/releases/tag/v0.0.31) on 2025-Nov-12
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.30...v0.0.31?expand=1)
> * Version Checksums: Functional=8696830ac25d67633b2f0def7501f1b1 Full=fbb8618415ddd96c1b24a9738fc65817

- New structure, `kitchen_arrival_percentage`, with a new, improved algorithm for calculating the percentage of fair-chance kitchen arrivals.

-------------------------------------
## [v0.0.30](https://github.com/pbv-public/insights/releases/tag/v0.0.30) on 2025-Sep-18
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.29...v0.0.30?expand=1)
> * Version Checksums: Functional=3d2ab529f4c4298df9772505d49928e5 Full=dc4c21fc37f366c9fa668b1bfbe11d29

- Unforced errors and putaways are supported now

-------------------------------------
## [v0.0.29](https://github.com/pbv-public/insights/releases/tag/v0.0.29) on 2025-Aug-07
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.28...v0.0.29?expand=1)
> * Version Checksums: Functional=df12e7f526fcf8958c541b16aa3d18f6 Full=2369c3227e7d5d60a2f44e01f05c6306

- Multi-session videos support
- Most important change is in the URL structure, now it contains the session ID: instead of /{video_id}/stats.json it is now /{video_id}/{session_id}/stats.json, where session_id is 0-based index of the session in the video. Client can iterate through sessions using the session_id until it gets 404 Not Found.

- `avatar_id` field is added to player_data, and it uses in the player avatar URL: /{video_id}/{ai_engine_url}/player{avatar_id}-[1-4].jpg are the four avatars for this player

-------------------------------------
## [v0.0.28](https://github.com/pbv-public/insights/releases/tag/v0.0.28) on 2025-Jul-14
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.27...v0.0.28?expand=1)
> * Version Checksums: Functional=6ac23651ef1a88f71d8695d1a4cdbc34 Full=be0bac0a6d4c0b916265dc47207fa695

- Replaced `ms_to_kitchen` with `kitchen_arrivals` array containing detailed kitchen line periods with `since_ms`, `until_ms`, and `ft_moved` vector data
- Added `team_stats` array to rallies with `average_ft_between_players_along_x` and `x_distance_optimality` metrics for doubles games
- Added `shooter_movement_from_last_shot` vector to track player movement between shots, using the new 2d `vector` type
- Added `player_positions` array with x/y coordinates for all players at shot timestamp
- Docs updates: dead_dink is "not supported, not planned", for the `kitchen_arrival` we specify that we consider only "rallies with at least 3 shots"

-------------------------------------
## [v0.0.27](https://github.com/pbv-public/insights/releases/tag/v0.0.27) on 2025-Jun-02
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.26...v0.0.27?expand=1)
> * Version Checksums: Functional=d4c0ff2080d78309f29dddb1ceb9b438 Full=45c2392114d7552766f960577df50dd0

- Add ratings data structures for players' ratings and their trends

-------------------------------------
## [v0.0.26](https://github.com/pbv-public/insights/releases/tag/v0.0.26) on 2025-May-17
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.25...v0.0.26?expand=1)
> * Version Checksums: Functional=7eb56e3b1df0f99ed717edcc6cc6a7a2 Full=9096be46e17cf16b981bd2f54497a34a

- Running score properties moved to rallies[*].scoring_info.running_score, with server_number added for doubles games
- Added start_ms and end_ms timestamps to track shot duration for shots without the resulting_ball_movement
- Updated popup error definition with more specific criteria
- Changed description of average_x_coverage_percentage to clarify it's only relevant for doubles games, made it optional
- Added corrected boolean flag to worldPosition3D to indicate post-CV corrections

-------------------------------------
## [v0.0.25](https://github.com/pbv-public/insights/releases/tag/v0.0.25) on 2025-Mar-12
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.24...v0.0.25?expand=1)
> * Version Checksums: Functional=b483a45020c6d31b7c782f354e2f8a49 Full=c2a595e98e836f111a87afd94e7272ae

- .running_score and the related properties have been moved to rallies[*].scoring_info.running_score, there's also .server_number there for the doubles games

-------------------------------------
## [v0.0.24](https://github.com/pbv-public/insights/releases/tag/v0.0.24) on 2025-Jan-23
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.23...v0.0.24?expand=1)
> * Version Checksums: Functional=0b322cd2cf0745aea8ae46ad0859c78b Full=d625ecc9493936cf77728e2e1b6b1522

- Rally scoring is now supported. Game data contains new attributes, `scoring` and `min_points`, that define the scoring rules for the game.
- New attribute for the rally, running_score, that computes the running score according to the scoring rules chosen.

-------------------------------------
## [v0.0.23](https://github.com/pbv-public/insights/releases/tag/v0.0.23) on 2025-Jan-15
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.22...v0.0.23?expand=1)
> * Version Checksums: Functional=9724ecf81c1a14ded5502331cdf7d4ea Full=ae5cd03c59147ffe2430176f3da09848

- Exposed "Coach advice" in the Insights, an array of advice for each player, ordered by their relevance.

-------------------------------------
## [v0.0.22](https://github.com/pbv-public/insights/releases/tag/v0.0.22) on 2024-Dec-03
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.21...v0.0.22?expand=1)
> * Version Checksums: Functional=8c6827137c0d55e74d409cb6fe0fb007 Full=80733506977ad40ea6ff3ffd8be29547

- Added `likely_bad` attribute to a rally to indicate that it shouldn't be used for calculating running scorie.
- In general, scoring is available now, so the scores will be reported numerically in `game_outcome`.

-------------------------------------
## [v0.0.21](https://github.com/pbv-public/insights/releases/tag/v0.0.21) on 2024-Nov-12
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.20...v0.0.21?expand=1)
> * Version Checksums: Functional=930d478af5b91cae8ed3692e6b489b21 Full=b0b782c0afabfe613e411ae3f1100f9b

- Fix the problem with Nullable types

-------------------------------------
## [v0.0.20](https://github.com/pbv-public/insights/releases/tag/v0.0.20) on 2024-Nov-11
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.19...v0.0.20?expand=1)
> * Version Checksums: Functional=8cca28e5c390867dcfc758baea9d8d4a Full=97fb1a07dd915cf620ef8a511e29e443

- fix `player_data` type to avoid the problem with the docs

-------------------------------------
## [v0.0.19](https://github.com/pbv-public/insights/releases/tag/v0.0.19) on 2024-Nov-04
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.18...v0.0.19?expand=1)
> * Version Checksums: Functional=930d478af5b91cae8ed3692e6b489b21 Full=b0b782c0afabfe613e411ae3f1100f9b

- added `session` to indicate game vs. drill and how many participants
- added optional `is_ball_machine` in `player_data`

-------------------------------------
## [v0.0.18](https://github.com/pbv-public/insights/releases/tag/v0.0.18) on 2024-Oct-24
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.17...v0.0.18?expand=1)
> * Version Checksums: Functional=3bcee1a2cb27e8b63eea4a3e29b79b35 Full=862225a86a48f93bf7939f58db0f5f74

- New fault type: `short`, when the ball fails to cross the net and ends on the server's side.

-------------------------------------
## [v0.0.17](https://github.com/pbv-public/insights/releases/tag/v0.0.17) on 2024-Sep-09
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.16...v0.0.17?expand=1)
> * Version Checksums: Functional=26409b227f40a459fbb6210ffdd00b04 Full=2054c1ad37c2ec10ca362c99a5a23ad7

- Errors are now enum-valued: potential vs exploited.
- Outs are simplified/normalized into a enum that avoids contradictory values.
- Descriptions of errors are updated for the upcoming simplified heuristics

-------------------------------------
## [v0.0.16](https://github.com/pbv-public/insights/releases/tag/v0.0.16) on 2024-Sep-02
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.15...v0.0.16?expand=1)
> * Version Checksums: Functional=4fb2e9d06f1bafc1a116c5135e300579 Full=93bb77fb9b27fe84cd5960f96f3314e2

- transitioned insights to more purposeful app use
- `rallies` now contains a list of `shots` instead of a list of `moments`
- renamed `game_stats` to `game_data`
- renamed `player_stats` to `player_data`
- `player_data` now contains far fewer key-value pairs

-------------------------------------
## [v0.0.15](https://github.com/pbv-public/insights/releases/tag/v0.0.15) on 2024-Aug-21
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.14...v0.0.15?expand=1)
> * Version Checksums: Functional=3a357194b183ae1f16827ecaa1e23d7a Full=d18e9abf0551bad5e88ad86fdaaa831b

* added new highlight type, "sequence", with a more complex schema. Eventually
  this new kind should subsume and obsolete all the others,
  as it coalesces interesting moments into longer sequences.

-------------------------------------
## [v0.0.14](https://github.com/pbv-public/insights/releases/tag/v0.0.14) on 2024-Jul-26
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.13...v0.0.14?expand=1)
> * Version Checksums: Functional=d28c0f4736bca8349ff15a21f3b2025e Full=709a23c5adfc60e1832358b622d9160e

- added the `poach` highlight type, same fields as the `shot` one

-------------------------------------
## [v0.0.13](https://github.com/pbv-public/insights/releases/tag/v0.0.13) on 2024-Jul-07
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.12...v0.0.13?expand=1)
> * Version Checksums: Functional=f249d9582ff350b9365fb164d65bef20 Full=f4d2b8c72564a926bcb6e10553130a22

- removed unnecessary `shot_zones` from `player_stats`

-------------------------------------
## [v0.0.12](https://github.com/pbv-public/insights/releases/tag/v0.0.12) on 2024-May-16
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.11...v0.0.12?expand=1)
> * Version Checksums: Functional=65aa09038155ebe0da01cf003c14ebb6 Full=004f27c714b26093898accbdea533e60

- added `is_speedup` shot property
- added `speedup_percentage` to each players' stats
- added `resets_percentage` to each players' stats

-------------------------------------
## [v0.0.11](https://github.com/pbv-public/insights/releases/tag/v0.0.11) on 2024-May-03
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.10...v0.0.11?expand=1)
> * Version Checksums: Functional=113684b54ca1aa73908dab36e9068b74 Full=960ee64bad2bd4c612ac45c0c488cfbb

* introduced two new highlight kinds. `atp` and `erne`

-------------------------------------
## [v0.0.10](https://github.com/pbv-public/insights/releases/tag/v0.0.10) on 2024-Apr-28
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.9...v0.0.10?expand=1)
> * Version Checksums: Functional=381888455f0c34f010f9ea5684f59442 Full=9f2144b8edace050e8df7c9e7e024081

- median speed, median height above net, and median baseline distance now available from shot stats
- names and descriptions for shot stats improved
- height above net is now measured from the estimated top of the net instead of the ground

-------------------------------------
## [v0.0.9](https://github.com/pbv-public/insights/releases/tag/v0.0.9) on 2024-Apr-10
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.8...v0.0.9?expand=1)
> * Version Checksums: Functional=68bde186c17ba96ceb1fb289547af573 Full=ed788c016c1f1758ee822dc2c741e68c

- included game rallies in insights
- restructured shot data and available fields
- quality now has two components (execution and selection) and an overall score
- highlights are generalized and exist now at the top level
- expanded shot information with information about errors, faults, poaching, resets, stroke side, vertical type, stroke type, winner type, shot type, and various resulting ball movement fields
- a shot type can now be one of: smash, lob, dink, drop, drive, atp, erne, tweener
- each shot type has different associated criteria for execution quality

-------------------------------------
## [v0.0.8](https://github.com/pbv-public/insights/releases/tag/v0.0.8) on 2024-Mar-23
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.7...v0.0.8?expand=1)
> * Version Checksums: Functional=940fd2f663eb7498e07ba56b6ab23f86 Full=115cd3cc03264d151ef47cfa2dcbc3e4

- the `version` field is now a string matching x.x.x, where x represents one or more digits

-------------------------------------
## [v0.0.7](https://github.com/pbv-public/insights/releases/tag/v0.0.7) on 2024-Mar-19
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.6...v0.0.7?expand=1)
> * Version Checksums: Functional=04c1cecf6d3c89c3330a1bea3fdfabe6 Full=b0789c2064010f4fdfde45d771c87817

- added new `percentage_of_served_rallies_won` optional stat
- added new `avg_distance_from_baseline` optional stat
- `avg_speed` and `avg_height_over_net` are now optional
- `drive` and `serve` shot speeds are now optional

-------------------------------------
## [v0.0.6](https://github.com/pbv-public/insights/releases/tag/v0.0.6) on 2024-Mar-01
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.5...v0.0.6?expand=1)
> * Version Checksums: Functional=e9fe5cad26875ebd3141ad079378ff4b Full=2af478a42d3c992137164678d291e075

- `game_outcome` is now an array with two elements (one for each team). The elements can be of type `null`, `string`, or `integer`. If `null`, the outcome is unknown. If `string`, the outcome is `won` or `lost`. If it's an `integer` the outcome entry represents the score.
- Added a quality score to each ball trajectory, which is a `double` between [0,1]. 1 is the best score, 0 is the worst score.

-------------------------------------
## [v0.0.5](https://github.com/pbv-public/insights/releases/tag/v0.0.5) on 2024-Feb-28
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.4...v0.0.5?expand=1)
> * Version Checksums: Functional=5f8f393cef184b686156d363ab4dd67f Full=c59a1826f656628e80dc1d328d6b7585

- updated speed stats to be specific to drives and serves
- improved speed groupings (fastest, average, median)

-------------------------------------
## [v0.0.4](https://github.com/pbv-public/insights/releases/tag/v0.0.4) on 2024-Feb-15
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.3...v0.0.4?expand=1)
> * Version Checksums: Functional=471650b712612bc1ed06964da00a4dd1 Full=71c75b0477aa12b98981efaabeca0bb8

* removed `rally_start_times`
* updated how heatmap data is encoded
* added median serve and shot speed
* change shot zone data to counts from percentages

-------------------------------------
## [v0.0.3](https://github.com/pbv-public/insights/releases/tag/v0.0.3) on 2024-Feb-02
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.2...v0.0.3?expand=1)
> * Version Checksums: Functional=d777dc2f0fc648a5c885379185aea1fd Full=492e710ca8f06112f8e036d9d58cf301

* changes to `third_shot_stats`:
  * added `ball_trajectories`
  * removed `count` (can get this from `ball_trajectories.length` instead)
  * fixed grammar error in description of this field

-------------------------------------
## [v0.0.2](https://github.com/pbv-public/insights/releases/tag/v0.0.2) on 2024-Jan-25
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.1...v0.0.2?expand=1)
> * Version Checksums: Functional=7a10024a27bdd821d4ea37a51525472e Full=f2acc5144586a825b687348e1089819d

* Renamed `global_stats` to `game_stats`
* Removed `game_stats.num_rallies`; get this from `rally_start_times.length` instead
* Added top-level key `rally_start_times` - this is an array that specifies which time each rally starts. Times are in milliseconds relative to the start of the video.
    * You can use this to figure out when a highlight starts (`game_stats.highlights` has rally indexes).
* Removed `kitchen_arrival_percentage`
    * Added `player_stats.role_stats` which provides stats about the player in various. You can use this to calculate the kitchen arrival percentages for a player when they're on the serving side (the old `kitchen_arrival_percentage` value):

```
kitchenArrivalPercentageAsServingSide = 
    (role_stats.server.oneself.kitchen_arrival + role_stats.server.partner.kitchen_arrival) / 
    (role_stats.server.oneself.total + role_stats.server.partner.total)
```

-------------------------------------
## [v0.0.1](https://github.com/pbv-public/insights/releases/tag/v0.0.1) on 2024-Jan-25
> * [Compare to Previous Version](https://github.com/pbv-public/insights/compare/v0.0.1^...v0.0.1?expand=1)
> * Version Checksums: Functional=228b591b5508cbf215cf5a8b86e24d64 Full=0c21e934a88013aafdd8c1b40be5d6ab

fix dev and release docs merging

