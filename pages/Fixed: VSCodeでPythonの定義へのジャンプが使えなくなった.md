
気が付いたらPythonで定義へのジャンプができなくなっていて不便で困った。

一旦Python関連の拡張をアンインストールしてVSCodeを再起動し、Pythonにオススメの拡張があるよ、というダイアログが出るのでそれを入れたら直った。

![image](https://gyazo.com/54f26be954edf2014e144e89a3141f9f/thumb/1000)

![image](https://gyazo.com/1146cab90998b04c45a547499fd6b73d/thumb/1000)

原因を確定させるための実験をしてまた壊れたら嫌なのでやらないが、関連する情報をメモしておく
- Pylanceを入れてみたことが怪しい
- ![image](https://gyazo.com/ed9698d6fdccc8b9f3309d38d157ca7b/thumb/1000)
- 詳細はもうわからないが、入れた直後に問題が起きていれば流石に気づいたのでは…
- その後しばらくの間に何度かVSCodeをアップデートしたり再起動したりした
- 僕は開発しているものによってTypeScriptを書いてる時期とPythonを書いてる時期があるので、TypeScriptの時期にしたアップデートでPythonの挙動が変わった場合はすぐに気づかなさそう。
