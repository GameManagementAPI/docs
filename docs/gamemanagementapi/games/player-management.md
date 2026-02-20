---
sidebar_position: 4
---

# Player management
`PlayerManager` is responsible for managing all players within a Game.

It handles joining, quitting, spectating, elimination, and revival, while also integrating with the GameManagementAPI event system.

## Overview
PlayerManager exists to:
- Track active players, eliminated players, and spectators.
- Enforce join conditions.
- Handle player lifecycle events (join, quit, eliminate, revive, spectate).

## Properties
- `players: List<GMAPlayer>` – Returns all current players (excluding spectators).
- `eliminatedPlayers: List<GMAPlayer>` – Returns players who have been eliminated.
- `alivePlayers: List<GMAPlayer>` – Returns all players still in the game.
- `spectators: List<GMAPlayer>` – Returns all players currently spectating.

## Managing players
While this class contains the implementation of functions such as `.join`, `.quit`, `.spectate`, `.eliminate`, etc. it is reccommended to use the [GamePlayer](../game-player.md) functions.