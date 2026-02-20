---
sidebar_position: 6
---

# World management
`WorldManager` handles the loading and unloading of game maps for a Game. It manages map selection, game world creation, and enforces consistent world rules during gameplay.

## Overview
WorldManager exists to:
- Track available maps for a game size.
- Load maps into the server.

## Companion Properties
- `mapsDirectory: File` – Directory (set in config) containing all maps. Defaults to ./gma-maps/ or the path in config.yml.
- `worldPrefix: String` – Prefix (set in config) for dynamically created world names. Defaults to "gma-".

## Properties
- `availableMaps: List<String>` – All map names available for this game size.
- `map: Map?` – The currently loaded map for the game, if any.
- `forcemap: String?` – Optional map name to force loading.

## Loading Maps
:::note
Note that you rarely have to interfere with this function, as the game logic takes care of this most of the time!
:::

Loading a map can be done via the `.load` function:
```kotlin title="example"
game.worldManager.load("DesertArena")
```

## Forcing maps
If you want to decide beforehand what map will be loaded for a game, you can use the forcemap attribute.
```kotlin title="example"
game.worldManager.forcemap = "DesertArena"
```
The game will default to loading this map if it has been set.

## Accessing Map metadata
Once a map get's loaded it becomes availabe at `game.worldManager.map`.
This Map object contains important functions:

### Accessing the bukkit world object
The actual `world` object is exposed via `game.worldManager.map.world`.
```kotlin title="example"
val world = game.worldManager.map.world
```

### Accessing the map metadata config
As mentioned before in [Providing maps](../../first-steps/providing-maps.md), each map contains a `metadata.yml`-configuration file.
This file can be used by plugins to store map-specific information.

The config is available in this map object under
```kotlin title="example"
val config = game.worldManager.map.metadata
```

For organization purpose, it's better to use 
```kotlin title="example"
val config = game.worldManager.map.getMetadata("plugin-name")
```
to access only your plugins part of the config.

For this example you'll need to modify the `metadata.yml` of each map like this:
```
plugin-name:
    attribute1: true
    attribute2: false
```


#### Example use:
```kotlin title="example"
val config = game.worldManager.map.getMetadata("plugin-name")
println("attribute1: " + config.getBoolean("attribute1")) // true
println("attribute2: " + config.getBoolean("attribute2")) // false
```