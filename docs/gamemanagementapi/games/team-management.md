---
sidebar_position: 5
---

# Team management
`TeamManager` handles all team-related logic within a Game. It tracks team composition, alive teams, and facilitates joining, leaving, and random team assignment.

## Overview
TeamManager exists to:
- Track all teams in a game.
- Maintain alive team state during gameplay.
- Handle team assignment (specific or random).
- Trigger team-related events.

## Properties
- `teams: MutableMap<Int, Team>` – Maps team IDs to their Team objects.
- `aliveTeams: List<Team>` – Returns all teams that still have at least one alive player.

## Managing Teams
### Getting a player’s team
- Returns the `Team` the player belongs to.
- Returns `null` if the player is not in a team or in another game.
```kotlin title="example"
val team = game.teamManager.get(player.gma)
```

### Getting a random team
- Returns a random team.
- `joinable = true` (default) filters out full teams.
- Returns null if no suitable team exists.
```kotlin title="example"
val team = game.teamManager.random()
```

### Joining a team
- Assigns the player to a specific team by ID.
- Returns true if the join was successful.
- Fails if the player is in a different game, the team is full, or the join event is cancelled.
- `force = true` removes the player from their previous team automatically.
```kotlin title="example"
game.teamManager.join(player.gma, teamId = 1)
```

### Quitting a team
- Removes the player from their current team.
- Returns true if successful.
- Fails if the player is not in a team or the event is cancelled.
```kotlin title="example"
game.teamManager.quit(player.gma)
```