
Wheat Seeds System is a mechanism to place custom models on minecraft worlds.
See all packages:
- [https://www.planetminecraft.com/member/nishiohirokazu/submissions/?morder=order_latest](https://www.planetminecraft.com/member/nishiohirokazu/submissions/?morder=order_latest)

![image](https://gyazo.com/c91279cc7e98aeeec292f3d8a5ba015e/thumb/1000)
- [link to this image](https://i.gyazo.com/c91279cc7e98aeeec292f3d8a5ba015e.png)
- > Each chair can be rotated 45 degrees. Each chair is actually a wheat seeds item in an invisible item frame which put on an invisible barrier block. So if you use some plugin to sit on blocks (for example GSit), you can sit on a chair.
    - [https://www.planetminecraft.com/texture-pack/colorful-chairs/](https://www.planetminecraft.com/texture-pack/colorful-chairs/)

### Commands for Resource Pack Users

To get custom item with ID=12345:
command

```
give @p wheat_seeds{CustomModelData:12345}
```

- If you use EssentialX plugin, this command returns error  `Error: Unknown item name: ...`.  EssentialX changes the syntax of `/give`,  so you need to use `/minecraft:give`. See this [Issue](https://github.com/EssentialsX/Essentials/issues/3532).
- If you use MyCommands plugin, you can use this:
mycommand

```
giveitem:
  command: /giveitem
  type: RUN_COMMAND
  runcmd:
    - "/minecraft:give @s wheat_seeds{CustomModelData: $arg1} 64"
```


To get invisible item frame:
command

```
give @p item_frame{EntityTag:{Invisible:1b}}
```


Or you can convert the nearest visible item frame into invisible one:
command

```
data modify entity @e[type=item_frame, nbt={Invisible:0b}, limit=1, sort=nearest] Invisible set value 1b
```


To fix the nearest item frame (so it doesn't break even the base block removed or new block placed on it)
command

```
data modify entity @e[type=item_frame, nbt={Fixed:0b}, limit=1, sort=nearest] Fixed set value 1b
```


To get invisible barrier block:
command

```
give @p barrier
```



### Hints for those who create models
- Model can be 6×6×6 size.
    - In the minecraft, you can make 3×3×3 model. You can set scale ×4 for displaying the model in the item frame. Model in item frame is shrinked ×0.5 by Minecraft vanilla behavior.
    - This is 3×2×1 size table:
        - [https://youtu.be/1xULTM0y7DE?t=41](https://youtu.be/1xULTM0y7DE?t=41)
    - This is 5×3×1 size table:
        - ![image](https://gyazo.com/a74f1d0d8468cdf04cf50a747a5f0233/thumb/1000)
    - The 5×3×1 size table is not a good solution. If the actual item frame go out of sight, the table disapper. Those large model is only good if player do not get near.
- Rotation
    - ![image](https://gyazo.com/87eb7a1e781f01756c4bc0bfdcf0b86b/thumb/1000)
    - The model in the minecraft has a restriction that the cuboid can rotate along only one of three axis. Because you can rotate a model in item frame, you can make a model which looks breaking the restriction.
- Overlaping two models
    - ![image](https://gyazo.com/1643fe1deac8082bb86a51867fc57767/thumb/1000)
    - [https://www.planetminecraft.com/texture-pack/umbrella-5379102/](https://www.planetminecraft.com/texture-pack/umbrella-5379102/)
- Overlaping on another block
    - For example, you can cover a chest with a custom model. The hitbox of the custom model is only in the item frame, so you can use the chest.

---

Japanese version: [[仕組みの解説]]

Memo for pack descriptions:

```
This resource pack includes X types, 16 colors Xs. Each X can be rotated 45 degrees.
This pack uses the Wheat Seeds System. Each X is actually a wheat seeds item in an invisible item frame which put on an invisible barrier block.
So if you use some plugin to sit on blocks (for example GSit), you can sit on a X.
	GSit: https://www.spigotmc.org/resources/gsit-modern-sit-seat-and-chair-lay-and-crawl-plugin-1-13-x-1-17-x.62325/
For the wheat seeds system, see this guide: https://scrapbox.io/nishio/WheatSeedsSystem
IDs: ...
```


[https://github.com/nishio/wheat_seeds_system/releases](https://github.com/nishio/wheat_seeds_system/releases)
