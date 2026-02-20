---
sidebar_position: 3
---

# Providing maps
As mentioned before, GMA expects a folder containing all of the possible maps that can be loaded.
This folder is specified in the `config.yml` (See [Configuring GameManager](../first-steps/configuration)).

## File structure
The maps folder contains subfolders for each size of game. Game sizes are always formatted as `${teamAmount}x${teamSize}` (for example `2x1`).
<p>These subfolders then contain all of the different maps as simple minecraft worlds.</p>

Say this folder was set to `./maps` for example.
The expected folder structure would look something like this then:

:::info Expected structure
```text
./server-root
└─ maps/
   └─ 2x1/
   |   └─ map1/
   |   └─ map2/
   |   └─ map3/
   └─ 2x2/
   |   └─ map1/
   |   └─ map2/
   |   └─ map3/
   └─ etc.
```
:::

## Map configuration
Every map-folder contains a specific `metadata.yml`-config file.
<p>This file is required for providing data such as spawn positions, builders of the map and more.</p>
Plugins using the GMA can read sections of this file as well to read game-specific information.


A `metadata.yml` can look something like this:
```yml title='metadata.yml'
builders:
  - c4vxl

team:
  0:
    spawn: [ x, y, z, yaw, pitch ]
    prefix: "<red>Team A</red>"
  1:
    spawn: [ x, y, z, yaw, pitch ]
    prefix: "<blue>Team B</blue>"
```

:::note
These are the minimal arguments GMA requires!
<p>If your plugin requests more information, you need to add it as well.</p>
:::