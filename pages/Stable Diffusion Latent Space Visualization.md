
last latent
- ![image](https://gyazo.com/03001d0e0afbd7ac95f7383401bc3178/thumb/1000)
output
- ![image](https://gyazo.com/4ca15aee48ad75ab8ede624233f3ce01/thumb/1000)
input
- ![image](https://gyazo.com/ae07f5c26f239fb198ce2ff134b580e0/thumb/1000)
init_latents
- ![image](https://gyazo.com/9b9bbaec4401ba122cd371e2af49870b/thumb/1000)


py

```
        def image_grid(imgs, rows, cols):
            assert len(imgs) == rows*cols

            w, h = imgs[0].size
            grid = PIL.Image.new('L', size=(cols*w, rows*h))
            grid_w, grid_h = grid.size
            
            for i, img in enumerate(imgs):
                grid.paste(img, box=(i%cols*w, i//cols*h, i%cols*w + w, i//cols*h + h))
            return grid

        def save_latent(x, name):
            x = torch.clamp((x[0] + 1.0) / 2.0, min=0.0, max=1.0)
            x = x.cpu().numpy()
            x = x * 255.
            imgs = []
            for i, y in enumerate(x):
                from PIL import Image
                img = Image.fromarray(y.astype(np.uint8))
                imgs.append(img)
            image_grid(imgs, 2, 2).save(name)

        save_latent(init_latents, "init_latents.png")
```

