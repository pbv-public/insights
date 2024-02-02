# Insights Schema Changelog

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

