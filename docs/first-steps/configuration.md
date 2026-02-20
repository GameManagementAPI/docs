---
sidebar_position: 2
---

# Configuring GameManager
Now that GameManager is set up correctly we can start to tweak some settings.

After starting the server for the first time with GameManager installed, you'll see a couple of files being created. One of them is `plugins/GameManager/config.yml`.
This is the main configuration file for GameManager.

Using this file you can tweak the behaviour of GameManager easily without needing to interfere with the code.

There are a couple main sections:


## 1. Language
GameManager has build-in support for multiple languages. In this section you can tweak the location of the translation files, default languages and databases.

```yml title='config.yml'
language:
  # The default language
  # used for console and players that don't have a specific language specified
  default: "english"

  # Path to file that stores player-languages
  db: "./languages.yml"

  # Path to directory where language translations will be stored
  translations-dir: "./gma-translations/"
```

## 2. Maps
In GMA maps are defined beforehand and loaded once a game starts. Since GMA supports multiple games running in parallel on one server instance, maps are being loaded into multiple in-game worlds.
<p>This configuration section allows for tweaking the name of these worlds and the directories where maps are located.</p>

```yml title='config.yml'
maps:
  # Every game creates its own world going by the name $world-prefix + $gameid
  # The prefix can be set here
  world-prefix: "map-"

  # Path to the directory containing the available maps
  db: "./maps/"
```

## 3. Queue
GameManager implements a basic waiting queue for games. Waiting times can be adjusted in this config section:
```yml title='config.yml'
queue:
  # Default waiting time in seconds
  wait-time: 60

  # Time to wait if a game is completely full
  full-wait-time: 5

  # If set to true: countdowns will be displayed in a boss bar to all players
  # If set to false: countdowns will still apply, but they won't be visible
  display-countdowns: true
```

## 4. Visibility
```yml title='config.yml'
visibility:
  # Tags to add to messages to send them in "public" game channel
  # Otherwise default chat will be just team chat
  public: [ "@a", "@all", "@e", "@everyone" ]

  # Determines if a team channel exists
  allow-team-chat: true
```

## 5. Team
This section allows for modifying basic in-team rules.
<p>Team prefixes can be changed by plugins later.</p>
```yml title='config.yml'
team:
  # Determines if friendly fire is enabled
  friendly-fire: false

  # Determines if player collisions count for teams
  team-collision: false

  # If set to false team prefixes won't be visible in front of player names
  display-prefix: true

  # The format in which prefixes will be rendered
  # Use "$label" as a placeholder for the team name
  prefix-format: "$label <gray>|</gray> "
```

## 6. Features
This section allows for quickly disabling unwanted features of GameManager. _But keep in mind that disabling a feature might cause unexpected behaviour!_
```yml title='config.yml'
# Enable / Disable different features of the plugin
features:
  commands:
    api: true
    join: true
    quit: true
    start: true
    forcemap: true
    language: true
    spectate: true
    map: true
    privategame: true

  handlers:
    queue: true
    connection: true
    gameEnd: true
    visibility: true
    respawn: true
    scoreboard: true
```