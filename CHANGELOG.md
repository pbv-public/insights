# Insights Schema Changelog

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

