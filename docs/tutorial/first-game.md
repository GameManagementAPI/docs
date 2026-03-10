---
sidebar_position: 1
---

# Building your first game
This section will guide you through creating a very simple game using GMA.

To keep things easy to understand, we will start with a minimal example:  
every player receives a **diamond sword** and a few **golden apples** when the game begins.

Before continuing, make sure your project is already set up as described in either the [Quick start using GMA-Template](../first-steps/quick-start.md) or the [Installation](../first-steps/installation.md) section.

## The GameHandler

Most games need some form of central class that listens to game events and reacts to them.  
In GMA terminology this is commonly called a **GameHandler**.

The handler is simply a Bukkit event listener that registers itself when it is created.

```kotlin title="GameHandler.kt"
class GameHandler : Listener {
    init {
        Bukkit.getPluginManager().registerEvents(this, Main.instance)
    }

    // Events here
}
```

### Equipping players
When a game starts, GMA fires a `GamePlayerEquipEvent`.
We can listen to this event to give players their starting items.

In this example we give each player:
- a diamond sword
- 5 golden apples

```kotlin title="GameHandler.kt"
@EventHandler
fun onEquip(event: GamePlayerEquipEvent) {
    val dropHandler = object : ItemBuilder.ItemEventHandler<PlayerDropItemEvent> {
        override fun handle(event: PlayerDropItemEvent) {
            event.isCancelled = true
        }
    }

    val player = event.player.bukkitPlayer

    player.inventory.setItem(0, ItemBuilder(
        Material.DIAMOND_SWORD,
        name = player.language.child("example").getCmp("game.sword.name"),
        unbreakable = true
    )
        .onEvent(PlayerDropItemEvent::class.java, dropHandler)
        .build())

    player.inventory.setItem(1, ItemBuilder(
        Material.GOLDEN_APPLE,
        amount = 5
    )
        .onEvent(PlayerDropItemEvent::class.java, dropHandler)
        .build())
}
```

### Customizing the game world
After a map is loaded, GMA fires a `GameWorldLoadedEvent`.
This event is useful for configuring the world before players start playing.

For example, you may want to enable the Keep Inventory gamerule:
```kotlin title="GameHandler.kt"
@EventHandler
fun onWorldLoad(event: GameWorldLoadedEvent) {
    event.map.world?.setGameRule(GameRules.KEEP_INVENTORY, true)
}
```

### Eliminating players on death
By default, GMA allows players to **respawn after dying**.  
For many game modes, however, you may want players to be **eliminated after their first death**.

To achieve this, you can listen to the `GamePlayerRespawnEvent` and eliminate the player manually:
```kotlin title="GameHandler.kt"
@EventHandler
fun onRespawn(event: GamePlayerRespawnEvent) {
    event.player.eliminate(event.killer)
}
```

### Custom game-specific logic
In the end, you might also want to add your own logic such as **block breaking listeners**.
When doing so, just always make sure the event actually happened inside of a game to not interfere with lobby behaviour:
```kotlin title="GameHandler.kt"
@EventHandler
fun onBlockBreak(event: BlockBreakEvent) {
    // Return if event didn't happen in a game
    if (!event.player.gma.isInGame)
        return

    event.isCancelled = true
}
```

## Other useful events
Other useful events you might want to listen to are:
- [GameStartedEvent](https://gma.c4vxl.de/javaDocs/-game-manager/de.c4vxl.gamemanager.gma.event.game/-game-started-event/index.html)
- [GameStopEvent](https://gma.c4vxl.de/javaDocs/-game-manager/de.c4vxl.gamemanager.gma.event.game/-game-stop-event/index.html)
- [GamePlayerQuitEvent](https://gma.c4vxl.de/javaDocs/-game-manager/de.c4vxl.gamemanager.gma.event.player/-game-player-quit-event/index.html)

More in [#Events](../gamemanagementapi/events.md)

## Source
You can find the source code of this example at:<br></br>
[https://github.com/GameManagementAPI/ExamplePlugin](https://github.com/GameManagementAPI/ExamplePlugin)