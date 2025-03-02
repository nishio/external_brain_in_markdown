
[[Google Colaboratory]]で[[LLM]]を動かしていて下記のエラーが出た。

`model = AutoModelForCausalLM.from_pretrained(MODEL_NAME, device_map='auto')`
> ValueError: The current `device_map` had weights offloaded to the disk. Please provide an `offload_folder` for them. Alternatively, make sure you have `safetensors` installed if the model you are using offers the weights in this format.

「Please provide an offload_folder」(offload_folderを指定してください)と書いてあるが「さっきは問題なく動いたのに試行錯誤してるうちに動かなくなったなぁ」の場合はその処置は適切ではない、という罠がある。

これは「GPUもメモリも足りないからディスクを使って遅いけど無理やり動かすね！」という状態。
- > The current `device_map` had weights offloaded to the disk.
- なのにオフロード先が指定されていないので「ファイルはどこに置いたらいい？」と聞かれている
    - autoのdevice_mapによってユーザの意図に反した状態になっている
- 一度offload_folderの指定なしに動いてる場合、だいたいGPUメモリは足りていてoffloadの必要はないはず
    - なので「色々いじってる間に過去にロードしたモデルが消えずに残ってメモリを圧迫している状態」になっているのが問題の根本原因
- その場合の手軽な処置は「ランタイムを再起動」になる。

このエラーが発生する前にサイレントにメモリへのオフロードが起きている
- `Counter(model.hf_device_map.values())`が本来`Counter({0: 28, 'cpu': 15})`なのに`Counter({'cpu': 41, 0: 2})`になってたりする。これは気づきにくい。
- 僕も昨日までは気付いてなくて、`hf_device_map`を教えてもらって色々観察してようやく理解した
- このケースだとGPUにゴミが残ったまま、モデルのロードのタイミングでギリギリまでGPUに詰め込んでるので、その後の処理で入力のトークンが多かったりしたときに`model.generate`で`OutOfMemoryError: CUDA out of memory.`になったりする
    - これも良くハマる人がいる
    - 途中まで動いて死ぬのでかなり時間の無駄
    - 今回参加していた[[松尾研LLMサマースクールのコンペ]]ではテストデータの100番以降に大きな入力があるので、そこまで走って死ぬ人を見かけた
- 運よく最後まで動いたとしても時間は無駄にかかる


PythonにはGCがあるのになぜこれが起きるか
- `model = AutoModelForCausalLM.from_pretrained(MODEL_NAME, device_map='auto')`のケースでは
    - まず右辺のオブジェクトが生成される
    - その後で新しいオブジェクトが名前に代入される
    - その古いオブジェクトへの参照が無効になるタイミングでGCが走る
- なので右辺のオブジェクト生成時に「リソースの状況を見てオートでリソース配分を決める」という設定は、GCで古いものが解放される前に現状のメモリ消費量を見てディスクへのオフロードを決めてしまう
- なおPythonの側でGCしてもCUDAの側でキャッシュが残ったりすることもあるようで、諸々めんどくさいのでランタイムを再起動するのが一番手軽

[[松尾研サマースクール2023大規模言語モデル]]

今これを試してる
py

```
model = None
tokenizer = None
torch.cuda.empty_cache()
tokenizer = AutoTokenizer.from_pretrained(MODEL_NAME, use_fast=False)
model = AutoModelForCausalLM.from_pretrained(MODEL_NAME, device_map='auto')
```

