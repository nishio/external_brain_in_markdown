---
title: "VSCode Python Snippets"
---

- [[atcoder]]をやるにあたって頻出コードは[[vscode]]のプロジェクトスニペットにする設計でやってきたのだけど、一部の[[スニペット]]は他の一般のプロジェクトでも便利だから使いたくなってきた
    - [https://github.com/nishio/atcoder](https://github.com/nishio/atcoder)
    - mainで色々てんこ盛りのボイラープレートを作成するのだけど、他の一般のプロジェクトでは「あ、デバッグ出力したい」「doc testのテストケース作成したい」みたいな部分部分の利用
    - 同じコードベースでやろうとこねまわすより、汎用のやつだけ切り出す方がいいかな
        - 別プロジェクトにした
        - [https://github.com/nishio/vscode_python_snippets](https://github.com/nishio/vscode_python_snippets)
        - atcoderでは提出のために「一つのファイルにまとまってないといけない」って制約があるけど、一般のプロジェクトだとないのでpipにくくりだした方が良いものもあるかもな

[https://code.visualstudio.com/docs/editor/userdefinedsnippets#_variable-transforms](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_variable-transforms)
- 選択範囲に正規表現での置換を掛けることもできる
