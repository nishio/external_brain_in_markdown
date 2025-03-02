
![image](https://gyazo.com/d82a2610de7f71191303b86b6bc97399/thumb/1000)
Minecraft: Pi editionはTCPでパケットを送って任意座標にブロック配置ができる
- クライアント側はPythonライブラリ[[mcpi]]がある
- Bukkit系サーバにこのプロトコルを追加するプラグインが[[RaspberryJuice]]

[[mcpi]]: Python library for communicating with Minecraft: Pi edition and RaspberryJuice.
[https://github.com/martinohanlon/mcpi](https://github.com/martinohanlon/mcpi)
API REFERENCE [https://www.stuffaboutcode.com/p/minecraft-api-reference.html](https://www.stuffaboutcode.com/p/minecraft-api-reference.html)

[[RaspberryJuice]]: A Bukkit plugin which implements the Minecraft Pi Socket API.
[https://github.com/zhuowei/RaspberryJuice](https://github.com/zhuowei/RaspberryJuice)
- [https://www.spigotmc.org/resources/raspberryjuice.22724/](https://www.spigotmc.org/resources/raspberryjuice.22724/)

python

```
from mcpi import minecraft
m = minecraft.Minecraft.create(SERVER_IP_ADDRESS, 4711)
m.setBlock([X, Y, Z, ID])
```


デフォルトの設定ではスポーンポイントからの相対座標なので期待したところにブロックが作られなくて混乱した。
初回起動時に作られる設定ファイルを変更して再起動することが必要だった

python

```
from mcpi import block
m.setBlock(0, 80, 0, block.STONE.id)
```

![image](https://gyazo.com/6dc5f0c700922eb6af0eca2e6bb0e433/thumb/1000)

python

```
m.setBlocks(0, 80, 0, 15, 80, 15, block.STONE.id)
```

![image](https://gyazo.com/7d0577698a7571c3a3d0db82e482d355/thumb/1000)

python

```
m.setBlocks(0, 80, 0, 512, 80, 512, block.STONE.id)
```

![image](https://gyazo.com/9c9e7e6ae2220d4dea255f2ecec3d2f3/thumb/1000)

python

```
for x in range(30):
	for z in range(30):
		m.setBlock(x, 81, z, block.WOOL.id, x * z % 16)
```

![image](https://gyazo.com/d82a2610de7f71191303b86b6bc97399/thumb/1000)
