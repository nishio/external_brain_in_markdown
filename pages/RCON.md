---
title: "RCON"
---

> RCON is a protocol that allows server administrators to remotely execute Minecraft commands.
[https://wiki.vg/RCON](https://wiki.vg/RCON)

Python
[https://github.com/barneygale/MCRcon](https://github.com/barneygale/MCRcon)
- これはどうも挙動がおかしい

mcrconはちゃんと動く

[Iapetus-11/aio-mc-rcon: An asynchronous RCON client/wrapper for Minecraft Java Edition](https://github.com/Iapetus-11/aio-mc-rcon)
- `$ pip install aio-mc-rcon`
python

```
from aiomcrcon import Client
import asyncio

async def main():
    command = "hd setLine test 1 Hello World via RCON"

    client = Client(HOST, PORT, PASSWORD)
    await client.connect()

    response = await client.send_cmd(command)
    print(response)

    await client.close()


if __name__ == "__main__":
    asyncio.run(main())
```

![image](https://gyazo.com/3f8b05fedbd5995d286f344fcdff6a06/thumb/1000)
