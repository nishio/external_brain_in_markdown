---
title: "ImageHash"
---

[ImageHash · PyPI](https://pypi.org/project/ImageHash/)
[GitHub - jgraving/imagehash: A Python Perceptual Image Hashing Module](https://github.com/jgraving/imagehash)

画像類似検索
- PNGをローカルでmd5コマンドでダイジェストしたものと、それをGyazoにアップロードした時のURLは一致する
- しかし画像をScrapboxにコピーペーストした時に自動でGyazoにアップロードされたものはURLが異なる
    - サーバサイドでPNGにする際の設定が異なるなどの理由でファイルの内容が異なるのか
    - この画像をダウンロードしてmd5を見たらURLと一致していた
- 元画像、Twitterに画像を投稿してtwimgでサーブされた画像、それをローカルに保存したもの、Scrapboxにペーストされたもの、に同じ画像があっても判断しにくい
    - Pythonで[[画像類似検索]]をする
    - [[imgsim]]とImageHashがある
        - 前者はTorchを使って768次元の特徴ベクトルを作る風
        - [[clip-ViT-L-14]]の仲間かな
    - 後者は機械学習を使わない感じ
        - 後者が向いてそう
    - ペーストでアップロードされたハッシュ値の異なる画像もImageHashなら同一と判定できることがわかった
