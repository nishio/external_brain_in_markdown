
[話題のOpenAIの新たな画像分類モデルCLIPを論文から徹底解説！ | DeepSquare](https://deepsquare.jp/2021/01/clip-openai/)


> This is the Image & Text model CLIP, which maps text and images to a shared vector space. For applications of the models
[https://huggingface.co/sentence-transformers/clip-ViT-L-14](https://huggingface.co/sentence-transformers/clip-ViT-L-14)
[[clip-ViT-L-14]]

49408
BOS=49406
EOS=49407
python

```
>>> clip.tokenize("a painting of a cat")
tensor([[49406,   320,  3086,   539,   320,  2368, 49407,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0]], dtype=torch.int32)
```


subwords
python

```
>>> clip.tokenize("bozuman")
tensor([[49406,   647,  4091,   786, 49407,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0,     0,     0,     0,
             0,     0,     0,     0,     0,     0,     0]], dtype=torch.int32)
```

