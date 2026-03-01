---
sidebar_position: 0
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Quick start using GMA-Template
<p>In this section you will find out on how to quickly set up a new project using the [GMA-Template](https://github.com/GameManagementAPI/GMA-Template) repo.</p>
For a more in-depth guide on how to setup a project, I recommend reading the [Installing GameManagementAPI](../first-steps/installation.md)-Section.

## Installation
### 1. Cloning the template
Clone this repository:
```sh
git clone https://github.com/GameManagementAPI/GMA-template
```
and open it in the IDE of your choice.


### 2. Download GameManager
Download the [latest release](https://github.com/GameManagementAPI/GameManager/releases/latest) of GameManager and place it into `run/plugins`.
For better testing it is recommended to download [GameLobby](https://github.com/GameManagementAPI/GameLobby/releases/latest) as well.

If you are on linux/macOS you can do this automatically by using the `downloadGMA.sh`-script provided in the template-repo:
```sh
sh downloadGMA.sh
```


### 3. Accept Server EULA
Accept the minecraft server eula in `run/eula.txt`.


### 4. Customize Metadata
It is recommended to
- Change the project name in the `settings.gradle.kts`
- Customize the plugin data in the `build.gradle.kts`
- Rename the root path from `de.c4vxl.gmatemplate` to your own group id
- Update the language namespace in the `Main`-class

### 5. Reinitializing the git repo
1. Delete the old repo:
   On Windows:
    ```sh
   rmdir /s /q .git
    ```

   On linux/mac:
    ```sh
   rm -rf .git
    ```

2. Initialize a new one:
    ```sh
   git init
   git add .
    ```

3. Push an initial commit:
    ```sh
   git commit -am "Initial Commit"
   git remote add origin "<your repo url>"
   git checkout -b main
   git push origin main
   ```

### That's it.


## Testing locally
For testing your plugin locally use the `runServer`-gradle task:
```sh
./gradlew runServer
```