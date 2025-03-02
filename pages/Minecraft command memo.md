
:

```
/give nishio_hirokazu minecraft:stone_hoe{CustomModelData:2}
```


:

```
/summon minecraft:item_frame -672 69 -54 {Facing: 1, Item: {id:"minecraft:stone_hoe", Count:1, tag:{CustomModelData:1}}}
```

- `Facing: 1`: UP

:

```
> data get entity @e[type=minecraft:item_frame, limit=1, nbt={TileX:-672,TileY:69,TileZ:-54}]

[19:26:04 INFO]: Item Frame has the following entity data: {Paper.SpawnReason: "DEFAULT", Invisible: 0b, Bukkit.updateLevel: 2, ItemDropChance: 1.0f, Item: {id: "minecraft:stone_hoe", tag: {Damage: 0, CustomModelData: 1}, Count: 1b}, ItemRotation: 0b, OnGround: 0b, Air: 300s, UUID: [I; -1081805783, -982563900, -1264162454, -1255602847], Invulnerable: 0b, Spigot.ticksLived: 7021, Paper.Origin: [-671.5d, 69.03125d, -53.5d], Fixed: 0b, FallDistance: 0.0f, WorldUUIDLeast: -6869986146997678055L, Motion: [0.0d, 0.0d, 0.0d], Paper.OriginWorld: [I; 1163289896, 1213743593, -1599543297, -2141630439], Facing: 1b, Rotation: [0.0f, -90.0f], TileZ: -54, Fire: 0s, Pos: [-671.5d, 69.03125d, -53.5d], WorldUUIDMost: 4996292060300984809L, PortalCooldown: 0, TileY: 69, TileX: -672}
```

:

```
> data get entity @e[type=minecraft:item_frame, limit=1, nbt={TileX:-672,TileY:69,TileZ:-54}] Item

[19:30:39 INFO]: Item Frame has the following entity data: {id: "minecraft:stone_hoe", tag: {Damage: 0, CustomModelData: 1}, Count: 1b}

> data get entity @e[type=minecraft:item_frame, limit=1, nbt={TileX:-672,TileY:69,TileZ:-54}] Item.tag

[19:30:53 INFO]: Item Frame has the following entity data: {Damage: 0, CustomModelData: 1}

> data get entity @e[type=minecraft:item_frame, limit=1, nbt={TileX:-672,TileY:69,TileZ:-54}] Item.tag.CustomModelData

[19:31:00 INFO]: Item Frame has the following entity data: 1

> data modify entity @e[type=minecraft:item_frame, limit=1, nbt={TileX:-672,TileY:69,TileZ:-54}] Item.tag.CustomModelData set value 2

[19:32:40 INFO]: Modified entity data of Item Frame
```



[https://gaming.stackexchange.com/questions/375477/minecraft-command-to-set-item-frame-content-from-a-chest-content](https://gaming.stackexchange.com/questions/375477/minecraft-command-to-set-item-frame-content-from-a-chest-content)
:

```
/data modify entity @e[type=minecraft:item_frame, limit=1, nbt={TileX:-129,TileY:78,TileZ:99}] Item set from block -127 76 105 Items[{Slot: 0b}]
```

- Check that you can read data from the source block:
:

```
/data get block -121 76 105 Items[0]
```

- Check that the correct target entity is selected:
:

```
/data get entity @e[type=minecraft:item_frame, limit=1, nbt={TileX:-129,TileY:78,TileZ:99}]
```

[https://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q11177898316](https://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q11177898316)
[https://www.minecraftforum.net/forums/minecraft-java-edition/redstone-discussion-and/2923845-giving-item-when-item-frame-is-used](https://www.minecraftforum.net/forums/minecraft-java-edition/redstone-discussion-and/2923845-giving-item-when-item-frame-is-used)
- `/give @s minecraft:iron_ingot{CustomModelData:1234567}`

:

```
To make the nearest item within 10 blocks unable to be picked up by players:
/data modify entity @e[type=item,distance=..10,limit=1,sort=nearest] PickupDelay set value -1
```

[https://minecraft.fandom.com/wiki/Commands/data](https://minecraft.fandom.com/wiki/Commands/data)
[Target selectors – Minecraft Wiki](https://minecraft.fandom.com/wiki/Target_selectors)

:

```
/testfor @e[type=Item_Frame] {TileX:-2,TileY:5,TileZ:0,Item:{id:"minecraft:arrow"},ItemRotation:4b}
```

[https://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q11177898316](https://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q11177898316)

set placed item frame invisible
:

```
/data modify entity @e[type=minecraft:item_frame, limit=1,sort=nearest] Invisible set value 1b
```

get invisible item frame
- `/give @p item_frame{EntityTag:{Invisible:1b}}`


:

```
/data modify entity @e[nbt={FromBucket: 0b}, limit=1] FromBucket set value 1b
```


`execute store score @s WarpX int 0 run data get entity @s Pos[0]`

`/data modify entity @e[type=minecraft:villager,sort=nearest,limit=1] VillagerData.type set value desert`


`/data modify entity @e[nbt={FromBucket: 0b}, limit=1] FromBucket set value 1b`

:

```
summon_fish:
  command: /summon_fish
  type: RUN_COMMAND
  runcmd:
    - "/summon tropical_fish"
    - "/data modify entity @e[nbt={FromBucket: 0b}, sort=nearest, limit=1] FromBucket set value 1b"
```

