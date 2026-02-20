---
sidebar_position: 2
---

# GamePlayer
`GMAPlayer` is a wrapper around Bukkit’s `Player`-object that adds game-related state, metadata, and utility helpers for interacting with the GameManagementAPI.  

It ensures a **single wrapper instance per player**, provides convenient accessors, and exposes high-level actions like joining games, spectating, eliminating, and resetting player state.

## Overview

The wrapper exists to:

- Store runtime metadata (game, language, team state)
- Provide convenience methods for common player actions
- Centralize player lifecycle logic

:::warning
Do **not** instantiate `GMAPlayer` directly. Always use `GMAPlayer.get(player)` or the `Player.gma` extension property.
:::

## Getting the GamePlayer instance
### Using the extension property (recommended)
```kotlin title="example"
val gmaPlayer = player.gma
```

### Using the companion `get` method
```kotlin title="example"
val gmaPlayer = GMAPlayer.get(player)
```

Both methods return the cached instance for that Bukkit player.


## Properties
- `bukkitPlayer: Player` - Returns the underlying Bukkit Player.
- `language: Language` - The player's preferred language. Automatically defaults to Language.default if none is set.
- `game: Game?` - The current game the player is participating in. null if not in a game.
- `isInGame: Boolean` - Returns true if the player is currently in a game.
- `team: Team?` - The team the player is currently part of. null if not in a team or not in a game.
- `isInTeam: Boolean` - Returns true if the player is part of a team.
- `isEliminated: Boolean` - Returns true if the player has been eliminated in the current game.
- `isSpectating: Boolean` - Returns true if the player is currently spectating a game.
- `privateGame: Game?` - Returns the private game owned by the player, if any.

## Joining a game
To make a player join a specific game you can use the `.join` method:

```kotlin title="example"
gmaPlayer.join(game)
```

This will fail if the player is already in a game. If you want this action to overwrite the current game, set the `force`-flag to `true`:
```kotlin title="example"
gmaPlayer.join(game, force = true)
```

## Leaving a game
To make a player leave their current game, you can use the `.quit` method:

```kotlin title="example"
gmaPlayer.quit()
```

## Spectating a game
To make a player spectate a given game, you can use the `.spectate` method:

```kotlin title="example"
gmaPlayer.spectate(game)
```

## Eliminating from a game
To finally eliminate a player from a game use the `.eliminate` method:
```kotlin title="example"
gmaPlayer.eliminate()
```

Note that you can later revert that action by using `.revive`:
```kotlin title="example"
gmaPlayer.revive()
```

As soon as the last player is eliminated, the game stops.