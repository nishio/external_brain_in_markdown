---
title: "Cypress勉強会"
---

2021-08-27
- [[Cypress]]をKozanebaのテストのために1ヶ月ほど使った段階で書いたものに、2ヶ月目に加筆した

## CypressではChromeなどの「実際のブラウザ」の中でテストコードが実行される
- 他のアプローチとしては「ブラウザのDOMをエミュレートするライブラリ」を使うものがある
    - 例えば[[Jest]] / [[jsdom]]
        - > Jest は jsdom とともに提供されており、jsdom が DOM 環境をまるでブラウザを使っているかのようにシミュレートしてくれます。 --- [DOM 操作 · Jest](https://jestjs.io/ja/docs/tutorial-jquery)
    - このアプローチだとライブラリの充実度の問題が出る
        - 例えば
            - canvas要素のgetContextが実装されてない
                - canvasを使うRegroupのほとんどの機能がテストできなかった
            - divのscrollHeightが常に0
                - Kozanebaのフォントサイズ自動調整がテストできない
        - 素朴なよくあるWebアプリならブラウザを使ってるかのようにテストできるかも知れない
            - が、ちょっと凝ったことをしようとするとすぐぶつかる
            - そして<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>の仕事は「ちょっと凝ったこと」をすることだ…
    - 実際のブラウザを使うアプローチでは、この手の問題がかなり減る
        - ゼロではない
        - 例: dragstartイベントのdataTransferがない
            - テストランナーが合成したイベントがネイティブのイベントと少し違うという現象
        - イベントを作って送りつけることでユーザの操作を模倣する
            - なので何らかの理由で「ブラウザで実際にユーザが操作した時に発生するイベント」がテストケースと異なったものになってる場合、テストで気づけない
            - 例: 最近あった「同一グループ内でドラッグしてグループの左上座標が変わった場合に座標がズレるバグ」
                - mousemoveイベントがそのグループに対して発生することがバグの再現条件だった
                - ドラッグ操作を模倣する際にこれが発生してなかった
- Cypressは、まずブラウザで特定のページを開いて、それからそのページを操作する
    - (コンポーネント単位のテスト機能もあるが、ベータ版だし、jsdomをつかうものなので今回は無視する)
    - 他人のサーバのサービスでもテスト対象にできる
        - 例えば「自分のサービスでshare操作をしたら Twitterが開いてこうなる」的なテストもできる
        - 自分のサービスに対して、ローカル環境ではなくデプロイ後の本番サーバでテストすることもできる
            - 現実的には、例えばFirebase authをエミュレータに差し替えないとテストできないなどの理由で、すんなりとはできないと思う、<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>はやってない
    - ソースコードを持ってないサービスでもテスト対象にできる
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>はアプリのコードとテストのコードを同じリポジトリに入れて、型定義などを共用してVSCodeに補完させてるけどね

## Cypressはブラウザの「中で」テストコードが実行される
- ![image](https://gyazo.com/966ce37818b54d52d17d3cbd946e70e0/thumb/1000)
- かつて良く使われていたSeleniumと比べる
    - ブラウザにHTTPサーバを組み込み、テストコードはそのサーバに対してHTTPリクエストを送って操作する仕組みだった
    - プロセスをまたぐ通信が遅そう？実際遅かった
    - HTTPリクエストが送れればなんでもいいのでテストの記述にPythonやJavaも使える
- Cypressは同一プロセス内
    - ブラウザで実行するのでJavaScriptや、JavaScriptに変換されるTypeScriptなどで書く必要がある
- 注: すごくディープな話だけどiframeが分かれていることに起因する問題はある
    - [[Cypress+Firestore=invalid data]]

## JSで記述されたテスト専用言語
- Cypressは言語内DSLで「取得コマンド」や「アサーション」を繋げてテストを記述する
    - この気持ちを持つことがとても大事だと思う、生のJavaScriptを書いてるつもりでいると間違える
    - JavaScriptを実行することで「ブロックを繋いでテストを構築」し、それが終わってからテストが実行される、というイメージ
- ![image](https://gyazo.com/1e2ed0d4667d0599a6b9f288684f752a/thumb/1000)
    - 取得やアサーションが失敗した時、デフォルト4秒の間は自動的にリトライする
    - これによってテスト対象の非同期的な振る舞いに対処しやすくなっている
- 例えば「ボタンを押すとネットワークリクエストをし、結果が返ってきたらラベルを更新」というテスト対象の振る舞いがあったとする
    - JavaScriptの仕様で前半と後半は処理の流れが切断される
        - その結果、JavaScriptから「ボタンを押す」を実行した場合、リクエストをした段階で処理がテストコードに戻ってきてしまう
        - テストコードが走り終わってから後半の「結果が返ってきたら」の部分が実行される
        - ![image](https://gyazo.com/be4e5f522965311250fca1280dd6eae1/thumb/1000)
        - なので前半部をトリガーした後のテストコードで同期的に「ラベルが更新されたか」を確認すると確実に失敗する
    - ブラウザ上のJavaScriptが協調的マルチタスクの仕組みで、かつ一部のAPIで「処理をブロックして待つことは許されない」という仕様になっているからこうなる
        - これがWebアプリのテストを書くことを難しくしている原因の一つ
    - 成功するまで一定期間リトライするテストコードを書くことが一つの解決策
        - Cypressは内部でそれをやってくれるので人間がテストコードにそれを書く必要がない
        - 別のツール、例えば[[DOM Testing Library]]では人間が明示的にライブラリが用意した[waitFor](https://testing-library.com/docs/dom-testing-library/api-async/#waitfor)を呼び出すテストコードを書く必要がある

## DOM取得のベストプラクティス
- Cypressは「テストからアクセスする要素にはデータ属性をつけ属性セレクタで取得するべき」派
    - 「idやclassで選択するな」ということ
    - データ属性とは
        - [データ属性の使用 - ウェブ開発を学ぶ | MDN](https://developer.mozilla.org/ja/docs/Learn/HTML/Howto/Use_data_attributes)
        - 例: `<div data-testid="foobar">`
        - 属性セレクタ`[data-testid="foobar"]`で選択
            - see [CSS セレクター - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Selectors)
    - なぜなら機能や描画に関係するidやclassや表示テキストやDOMの包含関係などの情報は実装の過程で変更されやすく、テストが壊れやすくなるからである
    - 特定の要素を指し示すことは機能や描画と疎結合に行われるべき
        - もし特定のidやclassや表示テキストや包含関係が本当に大事なのであれば、それは要素の取得ではなくアサーションにすればいい
    - Cypressはこれを支持している
        - >  Anti-Pattern: Using highly brittle selectors that are subject to change.
        - >  Best Practice: Use data-* attributes to provide context to your selectors and isolate them from CSS or JS changes.
        - >  ...
        - >  Don't target elements based on CSS attributes such as: id, class, tag
        - >  Don't target elements that may change their textContent
        - >  Add data-* attributes to make it easier to target elements
            - [Best Practices | Cypress Documentation](https://docs.cypress.io/guides/references/best-practices#Selecting-Elements)
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>もこれを支持してる
        - data-testidで取得するカスタムコマンドも作った
    - 一方で反対の思想の人たちもいる
        - > Based on the Guiding Principles, your test should resemble how users interact with your code (component, page, etc.) as much as possible. With this in mind, we recommend this order of priority:
        - > 1. Queries Accessible to Everyone ...`getByRole('button', {name: /submit/i})` ... `getByLabelText` ... `getByPlaceholderText` ... `getByText` ... `getByDisplayValue`
        - > 2. Semantic Queries ... `getByAltText` ... `getByTitle`
        - > 3. Test IDs ... `getByTestId`
        - >  getByTestId: The user cannot see (or hear) these, so this is only recommended for cases where you can't match by role or text or it doesn't make sense (e.g. the text is dynamic).
            - [About Queries | Testing Library](https://testing-library.com/docs/queries/about/#priority)
        - 要するに「人間の振る舞いと同じように見えてる値でDOMを選択すべきだ」的思想
- これを書いてから1ヶ月ちょい経った今の悩み
    - data-testidかidかによらない話
        - 「文字列一つで要素を選択する」という方針だと、この文字列は「グローバルスコープの変数名」に相当する
        - グローバル変数に関する問題がこちらでも起こる
        - 例:
            - T1: Add KozaneダイアログのAdd Kozaneボタンにはtestid: `add-kozane-button`をつけた
            - T2: Split Kozaneダイアログを追加した
            - T3: Split KozaneダイアログにもAdd Kozaneボタンがあるんだがどうする？
    - 要素と名前の対応を人間が覚えておくのは困難
        - まあテスト対象のソースを見て確認するけど
    - 意図せず重複する可能性がある
    - 文字列として扱ってるとtypoに気づけない
    - 🤔文字列Enumにする？？(やってない)
    - →議論
        - typoは即座に「そんなtestidの要素はない」とテストがコケるからすぐ気づける
        - 意図しない重複に関してはcy.getで取得したものが1個であるかどうかをアサーションすれば良い、意図せず複数になった時にすぐ気づける

## テストピラミッド
- UIのテストは遅く、高コスト
- ユニットテストは早く、低コスト
- だからユニットテストを多く行うべきである
- …という2012年にMartin Fowlerが書いた[記事](https://martinfowler.com/bliki/TestPyramid.html)がある
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>は無視してCypressでUIのテストを中心に書いている
    - Jestで単体テスト書いた方がいいと思うことがあったら書くつもりではある
        - create-react-appのデフォルトの設定でJestでの単体テストがファイル修正のたびにバックグラウンドで走る、特に追加のインストールなどなく使えて手軽
        - そのテストケースが0件な状態
    - ユニットテストよりUIのテストが多い状態
        - Seleniumの時代と比べてUIのテストが速く、低コストになった、ならば比率は変化して当然だろう
        - TypeScriptでanyを許さないスタイルで型を付けてるので型の整合性テストが行われてるとも言える
        - UIがテストされてるわけだからそこから呼び出されるロジックも当然テストされている
        - というわけで特に単体テストしたいものがない
        - 今主にUI部分を作ってるからテスト対象がUIぐらいしかないということかも
            - ![image](https://gyazo.com/85ee5fcf8126a1850a540a0ab530edcf/thumb/1000)
    - 「UIのテストは壊れやすい」
        - これが「機能は壊れてないのにテストだけ壊れる」なのか「機能が壊れた」なのかは区別するべき
        - UIのテストが「クリックする座標をハードコード」とか「非同期の処理をテストするために100ms待つ」などのやり方をしてた時は「テストだけ壊れる」は多かった
            - テストツールの洗練で減ってきているはず
            - Cypressの自動リトライとか、ビューポート固定とかでUIテストの再現性が高まってる
        - UIで複雑なことをしているなら後者の「機能が壊れた」も起こりやすい
            - しかし、これは起こりやすいからこそテストして早く気づくべきでは
            - Cypressだと、たとえば「このボタンをクリックする」というテストコードは自動的に「そのボタンが他の要素に覆われてない」「画面に表示されてる」などをテストする
                - 具体例: ユーザダイアログを出して、閉じた時に、直前のメニューを閉じ忘れていた
                    - 「ダイアログを閉じ、チュートリアルアイコンを押してチュートリアルを再開する」のテストがfailするので気づけた
                    - 「メニュー以外の部分をクリックするとメニューを閉じる」の実現のためのDOMがチュートリアルアイコンを覆っていることを検知した
    - 仕様が決まってないので「内部状態がこんな感じの時にこんな表示になってほしいな」から開発がスタートするせいもある
        - まずテストコードで内部状態をセットし、Cypressの画面を見て期待した表示になっているか確認する
            - ブラウザ上で動いて人間が実行後の状態を目視で観察できることが効いてる
            - ここでおかしかったらChromeの開発者ツールとかを使って調査ができる
            - 1ヶ月経って追記:
                - 「内部状態をセットする関数」をユーティリティ的に切り出してる
                - たとえば「グループがネストしている」とか
                - 具体的なテストをせずに「画面をその内部状態にする」だけのテストケースを用意してある、特定の内部状態の画面をすぐに出して人間が操作できる
        - バグレポートがあったので直そうという場合、既存の状態から少し操作して「期待した画面になってない」が確認される
            - 再現手段がここで判明した
            - この「期待した画面にならない」を再現するテストコードを足す
            - そしてバグを修正する
            - 期待した画面になったらそれをテストコードのアサーションにする
        - 比較: アプリ自体のコードに手を入れて特定の内部状態を作ることと比べて
            - その方法だと作業が終わった後に「内部状態を作るコード」をきちんと削除しないといけない
            - Cypressでやるスタイルならテストコードなのでそのまま残しておいて、別の変更をした後に走らせたりできる
        - 比較: 手で操作して確認する場合と比べて
            - ファイルを編集したらブラウザをリロードするところまで自動でやってくれる環境は多いけど、そこから手で同じ操作を繰り返すの面倒でしょ
                - 操作をミスって、リロードしてやり直したり…
                - 同じ操作を繰り返したつもりで操作ミスしてたり…
            - 特定のページを開いて特定の操作をするところまでをまずテストコードで自動化する
                - 人間がやるより高速に操作できる
                - しかも正確に再現性のある操作ができる
                - 例えばドラッグ機能のテストで、正確に10ピクセルドラッグして、それならこの値になるはずだ、というテストができる
                - 各種の数値を特徴的な値にするテクニック
                    - 影響しそうな数値にそれぞれ特徴的な値(42とか123とか)を入れる
                    - 結果を観察して「42ずれるということはこの値に関係するバグだな」みたいな判断ができる
                - 操作の各ステップでのDOMのスナップショットが見返せるので、どこでおかしくなったかわかる
                    - 色々な操作をした後で「あれ？ちょっとズレてる？」
                        - 時間を遡ってどの操作のタイミングでズレたから確認できる
                    - 具体例「4ピクセルずれるバグ」がそれで発見された
                    - 手で操作してたら見落としてしまったかも
- 2021-08-24の追記
    - こざねのdragやclickをonDragStartとかonClickとか使わずに全部onMouseDown系で実現する大手術をしたので大部分のテストが壊れた
        - まあ、それは仕方ないよな…

## 内部状態の設定API
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>は内部状態を[[ReactN]]で管理してる
- これの読み書き用の関数をJS APIとして露出して内部状態を外から設定できるようにしている
    - 追記: さらにCypressのカスタムコマンドにした
- これを使えばテストコードからアプリの内部状態を設定してテストできる
ts

```typescript
  it("show loading dialog", () => {
    cy.updateGlobal((g) => {
      g.dialog = "Loading";
    });
  });
```

    - ここをもっと説明した方がいい気がした
    - ![image](https://gyazo.com/ef5ebeddb670b083dc1a664b2923b2d2/thumb/1000)
    - そもそもReactNによってシングルトン的な内部状態管理オブジェクトが導入されている
    - Viewはそのオブジェクトにフックを掛けて(useして)内部状態が変わった時に再描画される設計になっている
    - この内部状態のget/setをテスト環境に露出している
    - setすれば画面は更新されるので「内部状態がこういう値の場合にどう表示されるか」がテストできる
    - getして「特定の操作の後の内部状態はどうなってるのか」のテストもできる
- localhostでだけ露出するようになってるのでリリース環境では触れない
    - 電子レンジのたとえ
        - 電子レンジの中身はうっかり触ると危ないので一般人の利用時にはカバーがあるべき
        - 電子レンジの開発をする人はカバーを手軽に外して内部にアクセスできるべき
- React的状態はオブジェクトの同一性で変更のチェックを行うため破壊的な更新が禁止されている
    - [[immer]]を使えば気楽に破壊的更新の書き方で非破壊的更新ができる
        - 破壊してはいけない状態のコピーがコールバックに渡されるのでそれを破壊的に書き換える、immer内部でそれを非破壊的更新に変換してくれる
    - というわけでimmerを使って更新するコードもカスタムコマンドにしてある
    - これはとても便利、テストケース内でちょこっと内部状態を書き換えて確認、ってできる

## カスタムのアサーション
- Cypressのアサーション部分は[[Chai]]なのでChaiの書き方を学ぶ必要がある
- あまりやっていない
- 画面上の位置を確認するアサーションだけ追加した
    - カスタムコマンドで「与えられた要素の画面上の位置を取得して返す」を作れば一致するかなアサーションには元々のものを使える？と当初思ったがそのアプローチはダメ
    - そのカスタムコマンドが成功するからその後のアサーションで失敗してもリトライが行われない
ts

```typescript
it("drag inside", () => {
  ready_one_group();
  cy.testid("1").should("hasPosition", [184, 199]);
  do_drag("1", "G1", 0, 0);
  cy.testid("1").should("hasPosition", [154, 144]);
});
```

- `should have`だろ、というセルフツッコミ
    - `cy.testid("1").hasPosition(154, 144)`ってしたかったのだけどやり方がわからなくて結果的にこうなった

## 小ネタ
- テストケースは`test_`で始めるようにした
    - VSCodeでCmd+Pでファイル名の一部を打って開く時にテストケースとそうでないものが区別しやすくしたかった
- Firebase AuthでGoogleなどのOAuthを使ったログインを使うならエミュレータが多分必須
    - テスト環境で通常のOAuthフローが動かないっぽい
- Cloud Firestoreを使う場合
    - エミュレータを使ってる
        - オブジェクトの中身の編集などは本番環境と同じくらい手軽
        - アクセス制御ルールの変更などは本番より手軽
            - ローカルのファイルを変更すれば自動でリロードされて即座に適用されるから
    - Cypressから使うのは…使ってるけど、使えるようになるまでイバラの道ではあった
        - experimentalForceLongPollingをtrueにする必要がある
        - useEmulatorする前にやる必要がある
            - [[Kozaneba開発日記2021-08-03#610a84dfaff09e0000e3b656]]
        - Cypressの環境で作成したオブジェクトは直接Firestoreに保存できない
            - iframeのせい
            - [[Cypress+Firestore=invalid data]]
            - アプリ側で`Object.assign`
- Google Analyticsを使う場合
    - localhostで動かないようにgtagを上書きして潰してる
    - さもないとテスト実行が毎回クッキーを捨てるため「新規ユーザー300人」などと記録される
- 僕はテストコードもTypeScriptで書いている
    - TypeScriptに既に慣れているので…
    - 最初はJSで書いてたが`position`を`posision`とtypoして「あれー、位置を変更したのに動かないな、なぜだ」とかやってたので時間の無駄
    - 補完や型チェックなしでGUIを作るのは大変
