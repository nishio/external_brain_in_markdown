
- ![image](https://gyazo.com/9b56949eefcc9f7f031b74a847a68d1b/thumb/1000)
py

```
x = model.cond_stage_model.encode("a painting of a black cat with yellow eyes, a color pencil sketch by Betye Saar, deviantart, folk art, creative commons attribution, chalk art, charcoal drawing")
y = torch.clamp((x + 1.0) / 2.0, min=0.0, max=1.0)
Image.fromarray((255. * y[0]).cpu().numpy().astype(np.uint8)).save("token.png")
```

- [[Black Cat 42]]
- ちなみにクエリが空の場合
    - ![image](https://gyazo.com/7b785e7dae25478475843a325f78742a/thumb/1000)
