---
title: "ai_museum誕生の記録"
---

from [[ai_museum]]
ai_museum誕生の記録

2022-09-07 (private: [/mitoujr/Stable Diffusion#6317738aaff09e00000841ba](https://scrapbox.io/mitoujr/Stable Diffusion#6317738aaff09e00000841ba))
ゲーミングPC(Windows)のWSLで動かしてるんだけど、ホストOSにDropboxを入れて生成された画像がDropboxに入るようにしました<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- プロンプトもDropboxにおいたファイルから読むようにしてある
- シードをインクリメントするタイミングで自動でリロードするので適当にプロンプトを書いて放置しておくと絵が生えてくる農業みたいなスタイル
- 生えてきたものをタイル表示にして選抜しやすくするアプリを書くかどうか迷ってる
    - 正確に言うとPythonで書くかNodeで書くかを迷ってる

2022-09-08 (private [/mitoujr/作業室2022-09-08](https://scrapbox.io/mitoujr/作業室2022-09-08))
### 1:00
- AIが生成した画像の一覧を表示したい<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - Next.jsでやることにした
        - TypeScriptでサーバサイドのコードを書くのとPythonでクライアントサイドのコードを書く(ことはできないのでJSと併用する)のでは前者の方がノウハウが今後有益そうと判断した
        - [[ai_museum]]という名前にした
    - Nodeからファイルシステムを見る方法を調べてる
        - `fs.readdirSync`
        - [File system | Node.js v18.8.0 Documentation](https://nodejs.org/api/fs.html#fsreaddirsyncpath-options)
        - ファイル一覧がとれた
    - 画像を静的サーブする方法を調べる
        - ローカル専用だからpublicの中でDropboxにシンボリックリンクするか
        - できた
    - ではAPIを叩いた結果で画像一覧を…
        - あっ、fetchは非同期だからPromiseになるのか
        - useEffectで叩いて更新するか

### 3:00
- 続き
    - 1フォルダー内の画像一覧は出るようになった
        - なぜか縦にならぶ…
        - flex-direction: columnのせいだった
        - みっちり並べるのはどうするんだったかなー
            - flex-wrapか
    - クリックして拡大縮小できるようになった
    - 次は「フォルダの中にフォルダがある」時の展開表示
        - APIにパラメータを渡すのは…
ts

```typescript
    fetch("/api/get_images", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ folder }),
    })
```

        - ってしたら`req.body.folder`に入るのか便利
            - [/nishio/Unexpected token o in JSON](https://scrapbox.io/nishio/Unexpected token o in JSON)
        - あーこれ、非同期にAPIを叩くのを繰り返さないといけないのか、どうしようかな
        - Promise.allで解決

### 23:00
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>クリックした画像がモーダルダイアログで拡大表示されるようにした
    - ここにプロンプトの情報などを表示したい
        - データの保存の仕方を何度か変えているのでどうするか…
        - fs.existsがあるな、これで判定するか
            - deprecated
            - fs.existsSync(path)がある
            - できた
    - レビューした画像を移動させる機能をつける
        - fs.rename
        - クライアントサイドでonClickに書いて動かなかった、そりゃそうだ
        - APIをつければいいのね
        - できた
- こんな感じでサブフォルダ内の画像がタイル表示されて
    - ![image](https://scrapbox.io/files/633e55151b49e40022b16ccc.png)
- クリックするとモーダルで詳しい情報が表示され、ここで「excellent!」を押すと良い画像を集めたフォルダにファイルを移動する
    - ![image](https://scrapbox.io/files/633e551c36081a00237100f0.png)
- テストユーザ(妻)が寝てしまったので続きはまた明日

### 雑談
- Today I learned<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - ローカルで動かして画像の選別を助けるツールを、ファイル処理とか慣れてるPythonで書いてUIをHTML+JSで頑張るか、TypeScriptでNext.jsをするか迷ったが、結論Next.jsは超便利だった
    - UI部分はReactのJSXで手軽に作れる
    - API部分もAPIフォルダにあるサンプルファイルをコピーして増やすだけ
        - ルーティングとか書かなくても動く
    - ファイル操作系、PythonにあるやつはだいたいNodeにもある、Syncって名前になってる
