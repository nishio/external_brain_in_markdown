---
title: "Minecraft Fence Model"
---

assets/minecraft/blockstates/warped_fence.json

```json
{
  "multipart": [
    {
      "apply": {
        "model": "minecraft:block/warped_fence_post"
      }
    },
    {
      "when": {
        "north": "true"
      },
      "apply": {
        "model": "minecraft:block/warped_fence_side",
        "uvlock": true
      }
    },
    {
      "when": {
        "east": "true"
      },
      "apply": {
        "model": "minecraft:block/warped_fence_side",
        "y": 90,
        "uvlock": true
      }
    },
    {
      "when": {
        "south": "true"
      },
      "apply": {
        "model": "minecraft:block/warped_fence_side",
        "y": 180,
        "uvlock": true
      }
    },
    {
      "when": {
        "west": "true"
      },
      "apply": {
        "model": "minecraft:block/warped_fence_side",
        "y": 270,
        "uvlock": true
      }
    }
  ]
}
```

