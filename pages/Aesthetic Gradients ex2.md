
- 否定的な実験
    - 短い、元々対象物をうまく表現できないプロンプトではAGがうまくいかないことを検証する

Qualia san
![image](https://gyazo.com/2dd25d87bb340bd4d6f494a205a2e51f/thumb/1000)
これを下記のクオリアさん画像で学習する
![image](https://gyazo.com/1cf3f125daf801ab5f646b3a33b021cf/thumb/1000)
パラメータ
![image](https://gyazo.com/f6c08f906f3db835174689d93884e240/thumb/1000)
![image](https://gyazo.com/d2f4d2601e3d129529a9e71485cf0590/thumb/1000)

step: 20
![image](https://gyazo.com/f341e6192d84754f303d65002c926b4c/thumb/1000)

lerning rate: 0.001
![image](https://gyazo.com/b061860082a3095a4c379ebdf03f2846/thumb/1000)

lerning rate: 0.0005
![image](https://gyazo.com/21c7722f2cb3e0a6ea8c4e7e41f61465/thumb/1000)

一瞬人型にはなったが全然見当違いな方向に走っていってしまった

長い記述的プロンプトを使う
![image](https://gyazo.com/097139e36239cc76a0683595a227461c/thumb/1000)

prompt: laughing girl, shining blue eyes, shining blue long hair, blue cat ears
with AG / without AG
![image](https://gyazo.com/3c691fe52b53363376fb45faaffc10f0/thumb/1000)![image](https://gyazo.com/468356116472a8d5e5fc5fc918dd4f77/thumb/1000)
![image](https://gyazo.com/ab763f9d5eb5ee33dd342aa7c5e23f20/thumb/1000)![image](https://gyazo.com/48b1daf3911cb0287ce5bf5d2aca271c/thumb/1000)
![image](https://gyazo.com/3d39b66bfa8671ab17b29bfa06c3bcae/thumb/1000)![image](https://gyazo.com/edc4d95d112128d44b41e42aeba37f49/thumb/1000)
これは…効いてる気もするし気のせいな気もする

異なるデータセットで試す
0.001 / 5
None, qualia-san, other comic1, other comit2
![image](https://gyazo.com/c3dc2498e6be30bc593e4c3d9868caec/thumb/1000)
step 5
![image](https://gyazo.com/aed2b7ff796e15ca45066f5f7bb400c7/thumb/1000)![image](https://gyazo.com/ceb8a21e180b5db7be428ea24c7ed78f/thumb/1000)![image](https://gyazo.com/b2f18c720b1ace24c1aa3b586eea9236/thumb/1000)
step 20
![image](https://gyazo.com/b7cfd9a374fa35730ad920fbde87d145/thumb/1000)![image](https://gyazo.com/d883fceb14b3bdd09b37ea0408a90c47/thumb/1000)![image](https://gyazo.com/ec9cf7e5947e02db5b4bf5fa8e7c2e2b/thumb/1000)
step 50
![image](https://gyazo.com/ee623d1cc1fca9a5b7982faaef66d827/thumb/1000)![image](https://gyazo.com/96430d185ee2bd8e530accfae381ce83/thumb/1000)![image](https://gyazo.com/3dfddcfb8ac40883e8a6e5efdaead5a0/thumb/1000)
0.0002 / 50
![image](https://gyazo.com/7090bc9c37629339e2598bda4d8a5750/thumb/1000)
0.0005
![image](https://gyazo.com/112ef71a5d447aab541a55a6effbf55e/thumb/1000)
0.001
![image](https://gyazo.com/dcab7f880ec73279270f4ea13f90a1f6/thumb/1000)
0.002
![image](https://gyazo.com/35e51309cb5cf75d83fd4bb4f4ab650f/thumb/1000)
0.005
![image](https://gyazo.com/ec55376974b5a34ff019141f5d189e96/thumb/1000)
0.01
![image](https://gyazo.com/1223d4a715de95a160e1a03f4b608253/thumb/1000)


[[Aesthetic Gradients]]
