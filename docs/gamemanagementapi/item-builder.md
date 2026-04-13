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

## Editing ItemMeta Directly
You can apply custom modifications to the `ItemMeta` using `editMeta`.
```kotlin title="example"
val item = ItemBuilder(Material.DIAMOND_SWORD)
    .editMeta {
        setCustomModelData(123)
    }
    .build()
```

## Event Handling (Item-Bound Events)
Items can have **instance-specific** event listeners. These only trigger if the event involves the exact built item.

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

### Event Priority
You can define event priority (default: NORMAL):
```kotlin title="example"
.onEvent(PlayerInteractEvent::class.java, handler, EventPriority.HIGH)
```

### Supported Events
The following events are supported out of the box:
- ```InventoryClickEvent```
- ```PlayerInteractEvent```
- ```PlayerDropItemEvent```
- ```PlayerItemBreakEvent```
- ```PlayerItemDamageEvent```
- ```PlayerItemConsumeEvent```
- ```BlockPlaceEvent```

Each event maps to specific item sources (e.g. cursor item, hand item, dropped item, etc.).

### Registering / Unregistering Event Types
You can dynamically control which event types are supported.

#### Registering Events
To register an event type you need to provide a function that returns a list of all items that can trigger the event:
```kotlin title="example"
ItemBuilder.registerEvent(PlayerInteractEvent::class.java) { event ->
    listOf(event.item)
}
```

#### Unregistering Events
```kotlin title="example"
ItemBuilder.unregisterEvent(PlayerInteractEvent::class.java)
```

Removes it from the supported event list.

## Building the Final Item
After configuring your item, call `build()` to create the ItemStack:
```kotlin title="example"
val finalItem = builder.build()
```
<br></br>
#### What build() does:
- Creates new ItemStack
- Applies name, lore, enchantments, etc.
- Stores unique item ID in PDC
- Applies meta editors
- Returns final item