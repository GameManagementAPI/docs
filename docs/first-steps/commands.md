---
sidebar_position: 4
---

# In-game commands
GameManager provides a list of commands to make accessing the API easier.

## /gamemanagementapi
This is the most important command. It provides an in-game interface for interacting with the GMA directly.
It allows you to register, list, start or stop and view data about games directly in-game.

### General Information
- Permission required: ```de.c4vxl.gamemanager.perms.command.api```
- Usage: ```/gamemanagementapi <game|player> <options>```

### Sub-command overview
Here's a list of all it's options:
- `/gamemanagementapi games list` – Displays a list of all currently registered games
- `/gamemanagementapi games register <size>` – Registers a new game with the specified size
- `/gamemanagementapi games start <id>` – Starts a queuing game with the given ID
- `/gamemanagementapi games stop <id>` – Stops a running game with the given ID
- `/gamemanagementapi games info <id>` – Shows detailed information about a specific game
- `/gamemanagementapi games list-players <id>` – Lists all players in a specific game with their teams
- `/gamemanagementapi games join <id>` – Allows a player to join a queuing game
- `/gamemanagementapi player <name> game` – Shows the game a specific player is currently in
- `/gamemanagementapi player <name> team get` – Shows the team of a specific player
- `/gamemanagementapi player <name> team join <team>` – Joins the specified team in the player’s game
- `/gamemanagementapi player <name> team quit` – Leaves the player’s current team
- `/gamemanagementapi player <name> quit` – Makes a player quit their current game
- `/gamemanagementapi player <name> send <id>` – Sends a player to a different queuing game
- `/gamemanagementapi player <name> jump` – Makes the sender join the same game as the specified player
- `/gamemanagementapi player <name> eliminate` – Eliminates a player from their current game
- `/gamemanagementapi player <name> revive` – Revives a previously eliminated player

:::tip
This command can be very useful when debugging.
:::


## /join
This command allows players to queue into a game of specific team dimensions.

- This command doesn't require any permission
- Usage: ```/join <teamAmount>x<teamSize>```

## /quit
Entering this command just makes the player that executed it leave the game they are currently playing.
- This command doesn't require any permission
- Usage: ```/quit```

## /spectate
This command allows players to spectate a game.

- Permission required: ```de.c4vxl.gamemanager.perms.command.spectate```
- Usage: ```/spectate <game|player> <gameId|playerName>```

## /start
This command starts the game the exector is currently queueing in.

Other than ```/gamemanagementapi games start <id>``` this command requires at least two teams being filled.

- Permission required: ```de.c4vxl.gamemanager.perms.command.start```
- Usage: ```/start```

## /privategame
Using this command, players can create "private games" that won't be discoverable for players using "/join" to join into a game.

- Permission required: ```de.c4vxl.gamemanager.perms.command.private_game```
- Usage: ```/privategame <create|invite|join> <size|player|owner>```

## /map
This command displays the currently loaded map.

- Usage: ```/map```

## /forcemap
This command forces a map for the game the executor is currently queueing in.

- Permission required: ```de.c4vxl.gamemanager.perms.command.forcemap```
- Usage: ```/forcemap <map>```

## /language
Using this command, players can customize their language preference.

- This command doesn't require any permission
- Usage: ```/language <language>```

---

:::warning
Commands can be unregistered by using the `features` section of the `plugin-config`.
<p>[Read more](../first-steps/configuration#6-features)</p>
:::