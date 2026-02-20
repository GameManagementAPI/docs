---
sidebar_position: 1
---

# Registering & Managing Games
The `GMA` object is the central access point for creating, registering, querying, and managing games within the GameManagementAPI. It maintains an internal registry of all active games and provides convenience methods for common workflows like finding open queues or creating new matches.

## Overview

GMA acts as a singleton service that:
- Keeps track of all active games
- Provides lookup utilities
- Handles game lifecycle registration/unregistration
- Helps find or create queueable games
- Exposes metadata like available game sizes

## Accessing Registered Games

### All Registered Games
Returns a snapshot list of every game currently in the registry.
```kotlin title="example"
val games = GMA.registeredGames
```

### Private Games
Returns only games marked as private (created with an owner).
```kotlin title="example"
val games = GMA.privateGames
```

### Possible Game Sizes
Provides a list of all available game sizes as strings, based on the world configuration.
```kotlin title="example"
val sizes = GMA.possibleGameSizes
```

### Getting Games
#### By ID
Fetch a specific game using its GameID.
```kotlin title="example"
val game = GMA.getGame(id)
```

Returns `null` if no game exists with that ID.

## Creating Games
To create and register a new game you can use the following methods:

### Creating a public game
```kotlin title="example"
val game = GMA.createGame(2, 4)
```

### Creating a private game
In order to make a game private all that needs to be done is providing an owner:
```kotlin title="example"
val game = GMA.createGame(2, 4, owner = player)
```

## Queueing for games
Typically you want to look for an existing game that is still in a queuing phase and only if it doesn't exist create one.
<p>Exactly this is what `GMA#getOrCreate` does.</p>

```kotlin title="example"
val game = GMA.getOrCreate(size)
```

## Registering Games manually
Adds a game to the registry manually.
```kotlin title="example"
GMA.registerGame(game)
```

## Unregistering a Game
By default, the game is stopped before removal.
```kotlin title="example"
GMA.unregisterGame(game)
```

You can disable this behaviour by setting the `stop`-flag to `false`:
```kotlin title="example"
GMA.unregisterGame(game, stop = false)
```