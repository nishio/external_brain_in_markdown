
Google Colabでビデオメモリをたくさん使うような処理をしていて、1回目は上手く行ったけど、2回目はメモリが足りなくてエラーになった
これは「必要のないインスタンスがビデオメモリをつかんだまま生きていること」が原因。
- 1回目の実行の時にはXをやる時にまだYが作られていなかった、2回目の実行の時には1回目で作られたYが残ったままXを実行する、ということ。
- Colabの環境が過去に作られたグローバル変数を掴み続けるのでGCされないわけだ。

そこで明示的に解放する
py

```
from numba import cuda
device = cuda.get_current_device() 
device.reset()
```

[google colaboratory - Can i clear up gpu vram in colab - Stack Overflow](https://stackoverflow.com/questions/71371756/can-i-clear-up-gpu-vram-in-colab)

これでいいのかは未検証
