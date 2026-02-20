---
sidebar_position: 5
---

# Events
GMA provides a custom event system for games, players, and teams. Plugins can listen to these events to react to game state changes, player actions, team events, or world changes.

All events are Bukkit events and can be handled in the usual way via the `@EventHandler` annotation.

```kotlin title="Example listener"
class GameListener : Listener {
    @EventHandler
    fun onGameEnd(event: GameEndEvent) {
        Bukkit.broadcastMessage("Game ${event.game.id} has ended!")
    }
}
```

Game events are split into multiple types:
- Game events
- GamePlayer events
- GameTeam events
- PrivateGame events

A list of all events can be found [here](https://github.com/GameManagementAPI/GameManager/tree/main/src/main/kotlin/de/c4vxl/gamemanager/gma/event).