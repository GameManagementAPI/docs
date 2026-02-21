---
sidebar_position: 5
---

# Item Builder
The `ItemBuilder` class is a utility for creating ItemStacks with custom attributes, including names, lore, event handling, etc. It simplifies item creation and allows registering event listeners specifically for the generated item.

## Creating an Item
You can create a basic item by specifying a material:
```kotlin title="example"
val diamondSword = ItemBuilder(Material.DIAMOND_SWORD).build()
```

## Adding Attributes
You can add attributes by passing them as arguments to the constructor:
```kotlin title="example"
val namedSword = ItemBuilder(
        Material.DIAMOND_SWORD,
        name = Component.text("Excalibur")
    )
    .build()
```

Attributes that are not in the constructor need to be set manually!

## Event Handling
`ItemBuilder` allows attaching event listeners to items. These listeners only trigger for the specific item instance.
### Registering an Event
You can register events using the `.onEvent` method.
```kotlin title="example"
val sword = ItemBuilder(Material.DIAMOND_SWORD)
    .onEvent(PlayerInteractEvent::class.java, object : ItemBuilder.ItemEventHandler<PlayerInteractEvent> {
            override fun handle(event: PlayerInteractEvent) {
                event.player.sendMessage(Component.text("You used your special sword!"))
            }
        })
    .build()
```

This can be done for multiple events!


## Building the Final Item
After configuring your item, call `build()` to create the ItemStack:
```kotlin title="example"
val finalItem = builder.build()
```