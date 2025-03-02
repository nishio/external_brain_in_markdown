---
title: "enchiへの導入"
---

割と頭が混乱しているので、まずは1ポモドーロ実行して記録を残す
書く場所は[[どこが適切かわからない]]ので[[とりあえずここに書く]]
- [[🌀どこに書こう]]

🍅
privateリポジトリを作成する
- omoikane-embed-enchi
- privateは初のケース

omniからpush
:

```
git remote add enchi https://github.com/nishio/omoikane-embed-enchi.git
git branch -M main
XXXX git push -u origin main
```

あーLFS送っちゃうのね
- rebaseして消すのかどうか
あ `git push -u origin main`は間違いじゃん
- `$ git push -u enchi main`
- そもそもoriginどこなん？

cloneして新しいcodeで開く
- `$ git clone https://github.com/nishio/omoikane-embed-enchi.git`
- `$ code omoikane-embed-enchi`

とりあえずローカルで動かす
- `.env`はリポジトリに入ってないのでomniからコピー
    - `PROJECT_NAME=enchi`する
- make_vecs_from_jsonでこうしてる
py

```
payload = {
    "title": title,
    "project": PROJECT,
    "text": "\n".join(buf),
    "is_public": is_public,
}
```

    - `is_public=True`はハードコードされてる
        - Falseにしとくか
- `.env`で`COLLECTION_NAME`を別立てにしていたことがうまく機能する？
    - `COLLECTION_NAME`は`nishio`のままにする
    - あー、これ、将来的に交通整理が必要になる予感
    - 「公開してるベクトル検索でヒットした文字列が出ないでほしい」が`is_public=False`？
    - あー、そうか[[誤った二分法]]だ
        - 「一般公開」「自分だけ見る」の二通りしか考えてなかったけど「一般公開」「限定公開」「自分だけ見る」の三通りになったからBooleanがそもそもおかしいんだ
        - [[プログラマは誤った二分法に気付きやすい]]
    - 今後`is_public=False`なものを検索対象にしてしまい、生成したものがenchiに入るようにしたら、誤って自分以外に公開してはいけない情報を`is_public=False`で入れてしまってリークする未来が見える
    - `is_public=True or for_enchi=True`が適切か
        - いや`is_public=True or project="enchi"`か
        - そもそも`project="nishio" or project="enchi"`でいいのでは？
    - この判断を未来の自分もちゃんとやるかな...


🍅
:

```
prev_title, prev_lines = bot_output[-1]
                             ~~~~~~~~~~^^^^
IndexError: list index out of range
```

- これはメインブランチが最新のノートを取得して読もうとしていて、最初の導入なので最新のノートが存在しないことによるもの
- 今回はそもそもメインブランチが必要ない気がしているのでパス

- private projectであることに起因するエラー
    - まだサポートしてなかっただけ
    - done

手動トリガーで1枚ページを作った
- いきなり自動実行にせずにどういう形の活動がいいかを模索していこう
- Github Actionsの定期実行をオフ

リファクタリングした
- えーと、これをpushしてどうするんだっけな
- omniにマージ…
    - そうか、作りかけのローカルバージョンの未コミット差分があるとややこしいのか
    - こっちのコード整理も必要

🍅
> そもそもoriginどこなん？
- origin = coreだな
- 混乱の元
- `% git remote rename origin core`
- `% git push omni main`
- `% git fetch enchi`
    - [[git fetch]]
- ![image](https://gyazo.com/e7fc85c1f4a0df1468bed850f8ca0499/thumb/1000)
- ![image](https://gyazo.com/359e241c3cb672ce5cadda058f9cff5e/thumb/1000)
- `% git push omni main`
- done!
git status

```
Your branch and 'enchi/main' have diverged,
and have 5 and 4 different commits each, respectively.
```

- それはそう、どうするの？
- `% git branch -dr enchi/main`

その他
- オモイカネのBotを「ランダムなページの末尾に感想を加筆する」にした
- unnamed-projectsのBotは「最も長いページに分割の提案をする」にした

