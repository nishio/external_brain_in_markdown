---
title: "pContinuousTranslation2023-04-27"
---

prev [[pScrapboxAutoTrans2023-04-18]]
- 2023-04-27
    - 前回の最後で1日1回の自動翻訳が安定動作していることを確認した
    - 前回は名前が変わった方が良いと感じて仮に[[pUnnamed]]というタイトルにしていたが、従来の[[pScrapboxAutoTrans]]に戻した
    - この「[[継続的翻訳]]」が達成されたところが時代の区切りだと思った
    - [[pContinuousTranslation]]

from [[継続的翻訳]]
(DeepL)[[継続的インテグレーション]]と[[継続的デリバリー]]は、自動化、頻繁な更新、迅速なフィードバック、品質保証など、共通のパターンを持っています。これらのパターンを翻訳や国際コミュニケーションの領域に適用することで、「継続的翻訳」という新しい概念を提案することができます。
- 継続的翻訳（CT）とは、CI/CDと同様に、自動化されたプロセスを用いて、翻訳や異文化コミュニケーションが常に更新、改善、改良されるシステムのことです。Continuous Translationの主な構成要素は以下の通りです：
        - 自動化：機械学習やAIを搭載した翻訳ツールを活用し、コンテンツの作成や更新時に自動的に翻訳を行い、手動による介入を最小限に抑えます。
            - done<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - 頻繁な更新： ソースコンテンツの変更を反映して翻訳が継続的に更新されるシステムを導入することで、海外のオーディエンスが常に最新の情報にアクセスできるようにします。
            - done<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - 迅速なフィードバック： フィードバックの仕組み（ユーザーからの提案、プロの翻訳者の意見など）を組み込むことで、翻訳の誤りや矛盾を素早く特定し修正することができ、長期にわたってより質の高い翻訳を実現します。
            - あー、なるほど。これはScrapboxで実現するのは難しいなぁ<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - 品質保証 エンドユーザーに提供する前に、自動的に翻訳をテストし、正確さと流暢さを検証するプロセスを確立します。
            - 「自動的に翻訳をテスト」とはLLMが読んで理解しにくいところをフィードバックするって感じかな？<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - コラボレーション： 開発者、翻訳者、その他の関係者が協力し、コンテンツ制作のワークフローに翻訳プロセスをシームレスに統合する環境を構築する。
            - これは今は開発者と翻訳者が同一だから気にしないでいいかな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 継続的な翻訳は、組織が効率的に最新、正確、高品質の翻訳コンテンツをグローバルなオーディエンスに提供することを可能にし、コミュニケーションの改善、ユーザー体験の向上、国際関係の強化につながります。
    - 「効率的に最新、正確、高品質の翻訳コンテンツをグローバルなオーディエンスに提供する」は良いミッションだね

[[pScrapboxAutoTrans2023-04-18]]のこれ
- > よくなったかどうか定量的に判断したいなぁ
- 継続的実行は可能になって、質の改善のフェーズになったと考えると、その質を計測する[[メトリクス]]がないのはおかしい(ソフトウェアエンジニア的文脈)

-----
2023-04-27
- 昨日[[Polis体験レポート:テロの原因究明をするか]]を書いて、朝起きたらちゃんと翻訳されていて、これをこのまま拡散するか、手直ししてから拡散するかを考えた
- アイコンの位置のズレとかがあることに気づいたので読んでいってどんな問題があるかとPossible solutionを書くのをやったほうがいいな

タイトル
- `Polis Experience Report: Do you want to investigate the causes of terrorism?`
- あなたはやりたいですか？みたいになってて変
    - 日本語は主語を省略しがちで、特に字数が限られたタイトルではそう
- `Polis Experience Report: Should we investigate the causes of terrorism?`

アイコンの位置
- ![image](https://gyazo.com/8c26d2dce272cfd3573c9463bb3ebff4/thumb/1000)
- これ「冒頭にアイコンを置く」「末尾にアイコンを置く」は構文の一種なんだな

Link
- ![image](https://gyazo.com/b0cbdfcb20198372aa4d1cb59af89e9e/thumb/1000)
- why?
- 長いリンクの途中に空白文字が入って分断されている
- `[detail https://scrapbox.io/nishio/Polis:%E3%83%86%E3%83%AD%E3%81%AE%E5%8E%9F%E5%9B%A0%E7%A9%B6%E6%98%8E%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6%E3%81%AE%E8%AD%B0%E8%AB%96#643d39f4aff09e0000dd6581]`

翻訳
- ![image](https://gyazo.com/479f8baa670a2425d72bb765f0c5f4b6/thumb/1000)
- ![image](https://gyazo.com/38fdf5e75dfbd7dabedabf70e39d320f/thumb/1000)

以上が英文を読まずにわかるミス

次に英文をDeepLして眺める
- いや？意外と問題ないな
- おかしいなと思ったところ、確認したら英和の翻訳で失敗してた

fixed
- run local_batch
- 英会話スクールから帰ってきたら結果を確認する

全然終わってないな
:

```
  9%|███████▍                                                                              | 1279/14848 [2:45:52<21:35:30,  5.73s/it]
  503 Server Error: Temporary Error for url: https://api.deepl.com/v2/translate
 14%|███████████▊                                                                          | 2037/14848 [4:19:43<77:17:07, 21.72s/it]
 ('Connection aborted.', ConnectionResetError(54, 'Connection reset by peer'))
 26%|██████████████████████▎                                                               | 3862/14848 [7:05:29<13:20:20,  4.37s/it]
```

3時間翻訳が走って、残り時間15時間の見積もりになっている(これは帰宅時に書いた)
- (最終的に7時間実行して残り13時間の表示になってる)
- 全体再翻訳はレアだから高速化してないせいなんだけども、これどうしようかな
方針
- どっちみち今のペースだと定期翻訳とぶつかるので一旦止めないといけない
- 並列化の実装をして今の翻訳を止めて差し替える


<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>下記のコードは翻訳サービスのAPIにリクエストを送ります。現在の下記のコードはAPIアクセスが直列化しているので遅いです。並列化して高速にしてください。
python

```
for page in pages:
    for line in lines:
        line["text"] = translate(line["text"])
```

<img src='https://scrapbox.io/api/pages/nishio/gpt-4/icon' alt='gpt-4.icon' height="19.5"/>あなたが要求しているように、Pythonの concurrent.futures ライブラリを使って、翻訳APIへのリクエストを並列化し、高速化することができます。以下にサンプルコードを示します。
python

```
import concurrent.futures

def translate_line(line):
    return {"text": translate(line["text"])}

# 翻訳リクエストを並列化する
with concurrent.futures.ThreadPoolExecutor() as executor:
    for page in pages:
        # 各行に対して翻訳リクエストを送信
        translated_lines = list(executor.map(translate_line, lines))
        
        # 翻訳された行を元のリストに戻す
        for i, translated_line in enumerate(translated_lines):
            lines[i].update(translated_line)
```

便利〜

:

```
cache length: 273667
 40%|████████████████████████████████████████████████████▏                                                                            | 6003/14848 [18:22<4:18:18,  1.75s/it]503 Server Error: Temporary Error for url: https://api.deepl.com/v2/translate
 50%|████████████████████████████████████████████████████████████████▊                                                                | 7461/14848 [38:26<1:00:26,  2.04it/s]503 Server Error: Temporary Error for url: https://api.deepl.com/v2/translate
 51%|██████████████████████████████████████████████████████████████████                                                               | 7606/14848 [41:43<1:25:02,  1.42it/s]503 Server Error: Temporary Error for url: https://api.deepl.com/v2/translate
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 14848/14848 [53:34<00:00,  4.62it/s]
total 29370658 no_cache 1581996 ratio 0.05386314463911568
translate: 3218.0509019168094
```

おー、1時間弱で残りが終わった。
- ![image](https://gyazo.com/3697e4b0198c4e52445b0f798f5f64a7/thumb/1000)
- 3000円くらいかな

next [[pContinuousTranslation2023-06-01]]

