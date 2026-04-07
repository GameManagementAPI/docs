---
sidebar_position: 2
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# GameStats
**GameStats** is an extension plugin for GameManager that provides comprehensive statistic tracking for individual players.

## Feature overview
- Custom holograms
- Statistic command
- Statistic tracking

## Installation
1. Download the [latest version](https://github.com/GameManagementAPI/GameStats/releases/latest) of this plugin
2. Place it into your servers plugins folder
3. Restart your server

## Plugin config
GameStats generates a `config.yml` file. This config file can be found at `plugins/GameLobby/config.yml`.
<p>In this config file you'll be able to set the path of the stats database:</p>
```yaml
config:
  # Directory for database
  db-path: "./stats/"
```

## Hologram Command
The `/hologram` command allows you to create or remove holograms that display player statistics.

Usage: `/hologram <create|remove> [leaderboard|custom] [statistics...]`
Permission: `de.c4vxl.gamemanager.perms.command.stats-hologram`

:::note
- When the hologram is created or removed, it is automatically updated for all online players.
:::

### Creating a custom hologram
Creates a statistics hologram at your current location.<br></br>
Usage: `/hologram create custom <statistics...>`

The hologram will be placed at the player's location who runs the command.<br></br>
You can specify multiple statistics that will appear as hologram lines.<br></br>
_Only valid statistic identifiers will be used._

Example: `/hologram create custom kills deaths wins`

### Creating a leaderboard hologram
Creates a leaderboard-hologram at your current location.<br></br>
Usage: `/hologram create leaderboard`

The hologram will be placed at the player's location who runs the command.<br></br>

### Removing a hologram
Removes the nearest hologram within a 5 block radius around the player.<br></br>
Usage: `/hologram remove`


## Stats Command
The stats command allows players to view their tracked statistics.<br></br>
Usage: `/stats [statistic]`


This command displays statistics that are tracked by **GameStats**.
- If no statistic is specified, the command will display all available statistics for the player.
- If a specific statistic is provided, only that statistic will be shown.

## Top Command
The top command allows players to view the current top players of a specific statistic.
Usage: `/top [statistic]`