---
sidebar_position: 1
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Installing GameManagementAPI
GMA is split into two different parts:
- GameManager:
    This is the Plugin that runs on your server, handling player interactions and events.
- GameManagementAPI (GMA):
    This is the actual core API you will be accessing from your projects.

### 1. Installing the GameManager plugin
This part is very straight forward:

- Simply download the GameManager plugin for the correct version from the [Github Repository](https://github.com/GameManagementAPI/GameManager/releases).
- Once that's done, just drag it into the `plugins` folder of your Minecraft server.

That's it. The GameManager plugin should be installed now!

### 2. Installing the GMA in your project
This is the fun part. To include the GameManagementAPI in your project you'll first need to import it in your build script.

First thing to do is adding the GMA maven repository. You can do this like this depending on your build system:
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



Now you can import the actual library:
<Tabs groupId="language">
  <TabItem value="gradlektl" label="build.gradle.kts (Gradle kotlin-dsl)">

```gradle
dependencies {
    implementation("de.c4vxl:gamemanagementapi:1.0.0")
}
```

  </TabItem>

  <TabItem value="gradle" label="build.gradle (Gradle)">
```gradle
dependencies {
    implementation 'de.c4vxl:gamemanagementapi:1.0.0'
}
```
  </TabItem>

    <TabItem value="maven" label="pom.xml (Maven)">
```maven
<dependencies>
  <dependency>
    <groupId>de.c4vxl</groupId>
    <artifactId>gamemanagementapi</artifactId>
    <version>1.0.0</version>
  </dependency>
</dependencies>
```
  </TabItem>
</Tabs>

reload your build script and that's it. Now you can access the api.


### 3. Specifying GameManager as a dependency
In order for your plugin to be loaded after GameManager has been enabled you need to add the GameManager plugin as a dependency in your plugin.yml. Simply add this line:
```yml title="plugin.yml"
softdepend:
  - GameManager
```


And that's it. Now both GMA and GameManager should be set up correctly.