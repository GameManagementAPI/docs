---
sidebar_position: 3
---

# Game  object
`Game` represents a single match or session within the GameManagementAPI. It manages players, teams, world state, and game lifecycle events such as starting, stopping, and broadcasting messages.

It is the core object of the API, orchestrating all game-related functionality.

:::warning
Do not instantiate Game manually if you rely on centralized game management. Always use the provided game creation utilities or managers to ensure proper registration and event handling.
[Registering & Manageing Games](../gma)
:::

## Overview

The Game object exists to:
- Track the state and lifecycle of a game.
- Manage players, teams, and spectators.
- Handle world and map loading.
- Broadcast messages.

## Instantiation
```kotlin title="example"
val game = Game(
    size  = GameSize(4, 2),
    id    = GameID.random(),
    owner = player.gma
)
```

## Properties
- `teamManager: TeamManager` – Manages teams and team assignments for this game.
- `worldManager: WorldManager` – Handles map selection, loading, and world state.
- `playerManager: PlayerManager` – Manages players and spectators.
- `scoreboard: Scoreboard` – Game-specific scoreboard instance for tracking objectives.
- `state: GameState` – Current state of the game (QUEUING, STARTING, RUNNING, STOPPING, STOPPED).
- `players: List<GMAPlayer>` – All players, including spectators, currently in the game.
- `isQueuing: Boolean` – Returns true if the game is in the QUEUING state.
- `isRunning: Boolean` – Returns true if the game is in the RUNNING state.
- `isStopped: Boolean` – Returns true if the game has finished and stopped.
- `isFull: Boolean` – Returns true if the game has reached its maximum player capacity.
- `isPrivate: Boolean` – Returns true if the game has an owner.

## Lifecycle Methods
### Starting
- Assigns players without a team to a random team.
- Loads the chosen or random map.
- Prepares players (resets state, teleports to spawn, sets scoreboard).

```kotlin title="example"
val success = game.start()
```

### Stopping
- Removes all players from the game.
- Optionally kicks players from the world.
- Unloads the game world.

```kotlin title="example"
val success = game.stop()
```

### Broadcasting messages
- Sends a message to all players in the game.
- Accepts a language key and optional formatting arguments.

```kotlin title="example"
game.broadcastMessage("game.start", "Team A")
```