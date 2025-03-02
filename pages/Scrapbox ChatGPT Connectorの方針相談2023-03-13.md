---
title: "Scrapbox ChatGPT Connectorの方針相談2023-03-13"
---


相談
- [[Scrapbox ChatGPT Connector]]の方針について相談したい。
    - 機能を増やすのではなく理解を容易にするための最小限のコードにするつもりでリリースしたが、本当に最小限ならもっと削れる。
    - 一方で使ってみた人の色々な意見を見てて自分でもいろいろ新しい機能を試したくなっている。
    - この新しい機能のコードも手軽に共有できるのが好ましい。

要約
- Scrapbox ChatGPT Connectorは、最小限のコードで理解しやすいようにしたが、使う人たちの意見を見て新しい機能も試してみたくなった。
- 新しい機能のコードも手軽に共有できるようにしたいと考えている。
- UserScript経由で、Scrapbox上での選択範囲テキストを取得して書き換えることができる。
- Scrapbox ChatGPT ConnectorのAPIを持ったサーバを立ち上げ、それをUserScriptから叩く。
- ベクトルインデックスの更新や複数人に質問するなど、ユーザのニーズに応じて機能拡充したい。
- mainブランチと別にdevelopブランチを作成し、そこに新しい機能のコードを追加する。
- Pythonで新しい機能を実装する。



<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたはこの会話で何がどうなるとよいのでしょう？(GPT)
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>Scrapbox ChatGPT Connectorの方針について相談したい。機能を増やすのではなく理解を容易にするための最小限のコードにするつもりでリリースしたが、本当に最小限ならもっと削れる。一方で使ってみた人の色々な意見を見てて自分でもいろいろ新しい機能を試したくなっている。この新しい機能のコードも手軽に共有できるのが好ましい。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「Scrapbox ChatGPT Connector」とは、ScrapboxとGPT-3を接続し、Scrapbox上でGPT-3の応答を取得する機能を提供するプログラムです。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>違います。Scrapbox上での応答取得もやりたいことの一つではある。UserScript経由で、Scrapbox上での選択範囲テキストを取得して書き換えることができるのでそれを使うと面白い。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>それはどのようにして選択範囲のテキストを取得していますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>知らない
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>選択範囲のテキストを取得する方法について、どのような方法を使用していますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>UserScriptの呼び出しがよしなにやってくれる
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Scrapbox上の選択範囲のテキストを取得して書き換えるための具体的な「UserScript」について、どのようなものを使用しているのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>まだ実装はしてないんだけど、Scrapbox ChatGPT ConnectorのAPIを持ったサーバを立ち上げて、それをUserScriptから叩く
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その「UserScript」について、Scrapbox ChatGPT ConnectorのAPIを叩く以外にどのような機能が必要ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>特に必要ない、シンプル
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その「UserScript」は、Scrapbox ChatGPT ConnectorのAPIを持ったサーバーに対してリクエストを送信するプログラムですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>はい
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「Scrapbox ChatGPT Connector」について詳しく教えてください。具体的には、どのような機能がありますか？また、それらの機能はどのような使い方をするのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>いまは、ベクトルインデックスを作ることと、それを使ってChatGPTに質問を送ることの2つの機能だけ
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「ChatGPT」とは、オープンAIが開発した自然言語処理モデルで、大規模なコーパスから学習した知識を元に文章生成や文章の補完を行うことができます。 「Scrapbox ChatGPT Connector」は、ScrapboxとChatGPTを接続し、Scrapbox上で ChatGPTの応答を取得する機能を提供するプログラムです。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>質問して
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>この「UserScript」について、どのように情報を収集しているのですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>👎UserScript
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「ChatGPT」には、Scrapbox ChatGPT Connectorに限らず、様々な応用がありますが、現在の「Scrapbox ChatGPT Connector」には、ベクトルインデックスを作成し、それを使用してChatGPTに質問を送る2つの機能があります。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>ユーザのニーズの中で、僕も欲しいなと思うもの: ベクトルインデックスを更新したい、複数人に質問したい、会話のラリーを続けたい
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「ベクトルインデックス」は、Scrapbox ChatGPT Connectorで使用するための、文章をベクトル化する変換モデルのことです。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>質問して
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「ベクトルインデックス」を更新することができるようにするために、どのような方法が考えられますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>方法は思い浮かんでるのだけど言葉で説明するより書いた方が楽
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「ベクトルインデックス」を更新するための方法について、具体的にどのようなことを考えていますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>更新するのではなく、古いインデックスを再利用して新しいのを作る方がいい
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>了解しました。具体的にどのような手順で新しいインデックスを作るのか、詳細をお伺いできますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>いいえ。コードで書く方がいい。mainブランチと別にdevelopブランチを作ってそこに入れるかな…
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「コード」というのは、どのようなコードを指していますか？詳しく教えてください。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>Pythonのコードです。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>このPythonのコードについて、新しい機能を追加するためにどのような変更が必要になるのか、具体的なアイデアはありますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>ある。埒が開かないからここに関してはさっさと実装するか…
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「埒が開かない」という表現について、どのような意味で使用しているのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>要約して
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>- Scrapbox ChatGPT Connectorは、最小限のコードで理解しやすいようにしたが、使う人たちの意見を見て新しい機能も試してみたくなった。
- 新しい機能のコードも手軽に共有できるようにしたいと考えている。
- UserScript経由で、Scrapbox上での選択範囲テキストを取得して書き換えることができる。
- Scrapbox ChatGPT ConnectorのAPIを持ったサーバを立ち上げ、それをUserScriptから叩く。
- ベクトルインデックスの更新や複数人に質問するなど、ユーザのニーズに応じて機能拡充したい。
- mainブランチと別にdevelopブランチを作成し、そこに新しい機能のコードを追加する。
- Pythonで新しい機能を実装する。


[https://keicho.netlify.app/#talk=e59nfBQZlBc4LAFFCyqX](https://keicho.netlify.app/#talk=e59nfBQZlBc4LAFFCyqX)
#KeichobotLog
