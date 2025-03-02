
[The Annotated Transformer](http://nlp.seas.harvard.edu/2018/04/03/attention.html) is nice guide of transformer. This page shares illustrations which I drew to understand the guide.

![image](https://gyazo.com/92b700712c863eea774458b1c5423202/thumb/1000)
![image](https://gyazo.com/d381a8a6896d075220189b19c755bb84/thumb/1000)


Before we see `EncoderLayer`, let see `SublayerConnection` which work as high-order component



![image](https://gyazo.com/f92f6f0e695011f95120df62561881ae/thumb/1000)

![image](https://gyazo.com/d88734256a59e1e8ea796d313fb07964/thumb/1000)

![image](https://gyazo.com/b3e9683e0a92b38e3ccfd1162eb4c1d8/thumb/1000)

The first `attn` works as self-attention and the second one as source-target attention.

![image](https://gyazo.com/dbf25a50913cffec321cf434a38684b6/thumb/1000)

![image](https://gyazo.com/10e07bf89e9849cbd5713eceb9961eaa/thumb/1000)

![image](https://gyazo.com/4af1dae56e55fb3dcd80bbf7758591ae/thumb/1000)


Except for attentions, the flow is simple:
![image](https://gyazo.com/74201458dbf6de2677e8fa378c535b6b/thumb/1000)

![image](https://gyazo.com/e92a208e2434a40d173bc0fba5f422c3/thumb/1000)
![image](https://gyazo.com/6e05086234806c65457c7a0a71369cfc/thumb/1000)
![image](https://gyazo.com/2f743d1d7e03aa424dc3e311ed5c012c/thumb/1000)

![image](https://gyazo.com/86a4d53b7e602325ae2e6f53c5d6db81/thumb/1000)

