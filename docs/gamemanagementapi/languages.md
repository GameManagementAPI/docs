---
sidebar_position: 4
---

# Multi-Laguage support
The `Language` class provides a centralized translation system for the GameManagementAPI. It allows for supporting multiple languages, with dynamic language loading, per-player preferences, and plugin-specific language extensions.

:::note
All text sent to players should use Language.get or Language.getCmp for proper translation and styling.
:::

## Overview
The language system exists to:
- Provide translations for core messages and gameplay.
- Persist player-specific language preferences.
- Allow plugins to add their own language extensions.
- Support argument substitution and cross-key references.

## Loading and Managing Languages
### Listing available languages
The Language object provides a list of all available languages gma recognizes.
```kotlin title="example"
val langs = Language.availableLanguages
```

### Loading a language by name
- Returns the Language object for the requested name.
- Falls back to null if the file does not exist.
```kotlin title="example"
val french = Language.get("french")
```

### Default fallback language
The default fallback language used when a player has no preference or the translation file is missing can be accessed like this:
```kotlin title="example"
val fallback = Language.default
```

## Player Language Preferences
### Getting a players language preference
Language provides a static method for retrieving the players prefered language from db:
```kotlin title="example"
val langName = Language.getPlayerLanguage(player)
```

But it is reccommended to use
```kotlin title="example"
val language = player.gma.language
```
or
```kotlin title="example"
val language = commandSender.language
```

### Setting player language preferences
Player language preferences are usually set via the GamePlayer instance:
```kotlin title="example"
player.gma.language = Language.get("english")
```

## Getting Translations
### Get a plain text translation
To simply retrieve the translation value of a translation key:
```kotlin title="example"
val msg = language.get("game.starting")
```

### Get a styled text translation as a text component
This function uses MiniMessage for directly parsing the translation into a component:
```kotlin title="example"
val component = language.getCmp("game.starting")
player.sendMessage(component)
```

### Arguments
Both functions support passing custom arguments to the translations:
```kotlin title="example"
val msg = language.get("game.starting", arg1, arg2, arg3, ...)
```

or

```kotlin title="example"
val component = language.getCmp("game.starting", arg1, arg2, arg3, ...)
```

## Providing language extensions for plugins
You can just use the GMA language implementation instead of implementing one for your plugin.
This is done by so called language `extensions`.

You can load these extensions when your plugin starts by executing the following method:
```kotlin title="example"
Language.provideLanguageExtension(
    namespace = "MyPlugin",
    language = "english",
    languageFileContent = """
        myplugin.greet: "Hello, $0!"
        myplugin.farewell: "Goodbye, $0!"
        ...
    """.trimIndent()
)
```

:::note
Please load the languageFileContent from disk and don't store it as a string in your project...
:::

---

### Accessing extensions
These language extensions can then be accessed by using the `.child` method of a language:
```kotlin title="example"
val pluginLang = language.child("MyPlugin")
val greeting = pluginLang.get("myplugin.greet", player.name)
```