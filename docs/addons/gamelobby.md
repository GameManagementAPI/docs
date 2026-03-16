---
sidebar_position: 1
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# GameLobby
GameLobby is an extension plugin to `GameManager` that provides core lobby functionality for games built on the GameManager ecosystem. It adds player-friendly lobby mechanics like queues, map voting, and join signs.

## Feature overview
- Lobby spawn points
- Join signs for games
- Map voting system
- Custom queue system
- Custom spectator handling
- Fully customizable messages and sign layouts

## Installation
1. Download the [latest version](https://github.com/GameManagementAPI/GameLobby/releases/latest) of this plugin
2. Place it into your servers plugins folder
3. Restart your server

## Plugin config
GameLobby generates a `config.yml` file that allows for detailed customization of lobby behaviour. This config file can be found at `plugins/GameLobby/config.yml`.

```yaml
config:
  # The formatted text shown before all plugin messages in chat
  prefix: "<gray>[</gray><green>Lobby</green><gray>]</gray>"

  # If enabled, players will automatically receive a welcome message when joining the lobby
  send-welcome-message: true

  lobby:
    # The cooldown (in seconds) a player must wait before using the lobby boost again
    boost-cooldown: 5

    # The velocity multiplier of the booster
    boost-strength: 2.2

    # The cooldown (in seconds) between teleport uses in the lobby
    tp-cooldown: 3

    # The style of signs
    # Variables available: $size
    game-signs:
      line0: "<aqua>===============</aqua>"
      line1: "<gray>Join a game</gray>"
      line2: "<gold>$size</gold>"
      line3: "<aqua>===============</aqua>"

    # The file name used to store player visibility preferences
    visibility-db: "player-visibility.yml"

  queue:
    # The material used as the item for selecting a team in the queue
    team-selection-item: "WHITE_BANNER"

    # The material used as the item for voting on maps in the queue
    map-voting-item: "MAP"

    # The material used as the item that allows a player to leave the queue
    leave-item: "OAK_DOOR"

    # If set to false, players won't be able to choose a team in solo games
    use-team-selection-item-solos: true

    # If set to false, players won't be able to choose a team in multi-player-team games
    use-team-selection-item-multiple: true

# Specify custom team labels
team-labels:
  # If set to 'true', team labels specified in map-metadata files will be overwritten
  # If set to 'false', team labels from map-metadata will be used
  overwrite-labels: false

  # Custom prefixes for teams
  # 0: "Team 1"
  # ...
```

## Setting the spawn point
To set the lobby spawn point you can use the `/setspawn` command provided by the plugin.<br></br>
Any player joining the game from now on will spawn in the **exact** location that the user running the command was at.

:::caution
This command copies your location down to the decimal. Orientation will also be copied!
:::

## Game Signs
**GameLobby** provides the option for creating custom signs which allow players to join games of specified sizes when clicking them.

To create such a sign you can use the `/gamesign` command.

Usage: `/gamesign <create> <size>`<br></br>
Example: `/gamesign create 2x1`

This will give you a sign you can place anywhere you want.

## Accessing the Lobby API
While usually not required, **GameLobby** does provide an API for you to listen to lobby-bound events and react to them to refine lobby behaviour.

In order to import it, add the `GMA-maven-repository` as already described in [#Installing GameManagementAPI](../first-steps/installation.md):
<Tabs groupId="language">
  <TabItem value="gradlektl" label="build.gradle.kts (Gradle kotlin-dsl)">

```gradle
repositories {
    maven("https://mvn.c4vxl.de/gma/")
}
```

  </TabItem>

  <TabItem value="gradle" label="build.gradle (Gradle)">
```gradle
repositories {
    maven {
        url = uri("https://mvn.c4vxl.de/gma/")
    }
}
```
  </TabItem>

    <TabItem value="maven" label="pom.xml (Maven)">
```maven
<repositories>
  <repository>
    <id>GMA</id>
    <url>https://mvn.c4vxl.de/gma/</url>
  </repository>
</repositories>
```
  </TabItem>
</Tabs>

<br></br>

Now you can import the actual library:
<Tabs groupId="language">
  <TabItem value="gradlektl" label="build.gradle.kts (Gradle kotlin-dsl)">

```gradle
dependencies {
    implementation("de.c4vxl:gamelobby:1.0.0")
}
```

  </TabItem>

  <TabItem value="gradle" label="build.gradle (Gradle)">
```gradle
dependencies {
    implementation 'de.c4vxl:gamelobby:1.0.0'
}
```
  </TabItem>

    <TabItem value="maven" label="pom.xml (Maven)">
```maven
<dependencies>
  <dependency>
    <groupId>de.c4vxl</groupId>
    <artifactId>gamelobby</artifactId>
    <version>1.0.0</version>
  </dependency>
</dependencies>
```
  </TabItem>
</Tabs>

reload your build script and that's it. Now you can access the api.

### Lobby Events
Some of the events this api provides include:
- [LobbyPlayerSendEvent](https://github.com/GameManagementAPI/GameLobby/blob/main/src/main/kotlin/de/c4vxl/gamelobby/events/lobby/LobbyPlayerSendEvent.kt)
- [LobbyPlayerJoinEvent](https://github.com/GameManagementAPI/GameLobby/blob/main/src/main/kotlin/de/c4vxl/gamelobby/events/queue/LobbyPlayerQueueJoinEvent.kt)
- [LobbyPlayerSignClickEvent](https://github.com/GameManagementAPI/GameLobby/blob/main/src/main/kotlin/de/c4vxl/gamelobby/events/signs/LobbyPlayerSignClickEvent.kt)

A full list of all events can be viewed [here](https://github.com/GameManagementAPI/GameLobby/tree/main/src/main/kotlin/de/c4vxl/gamelobby/events).