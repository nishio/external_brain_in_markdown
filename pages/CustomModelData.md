---
title: "CustomModelData"
---

custom_model_data
[https://minecraft.fandom.com/wiki/Model](https://minecraft.fandom.com/wiki/Model)
> Item predicates
>  Some items support additional predicates for model overrides. Below is a full list of available predicates.
- > "custom_model_data": Used on any item and is compared to the tag.CustomModelData NBT,
- "any item" doesn't include a stick: [https://minecraft.fandom.com/wiki/Item](https://minecraft.fandom.com/wiki/Item)

[https://www.planetminecraft.com/forums/communities/texturing/new-1-14-custom-item-models-tuto-578834/](https://www.planetminecraft.com/forums/communities/texturing/new-1-14-custom-item-models-tuto-578834/)

:

```
  "overrides": [
    {
      "predicate": { "custom_model_data": 1 },
      "textures": { "5": "item/blue_screen" }
    },
    {
      "predicate": { "custom_model_data": 2 },
      "textures": { "5": "item/minecraft" }
    },
    {
      "predicate": { "custom_model_data": 3 },
      "textures": { "5": "item/cybozusiki" }
    }
  ],

```

