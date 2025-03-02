
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Githubでファイルが大きすぎるからGitLFS使いたい時ってどうするんだっけ
<img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>
- Git LFSを使うには、以下の手順を実行してください。
    - Git LFSをインストール: 公式サイト( [https://git-lfs.github.com/](https://git-lfs.github.com/) )からダウンロードしてインストールしてください。
    - ターミナルで、git lfs installと入力して実行してください。
    - 大きなファイルの拡張子を指定: git lfs track "*.拡張子"（例: git lfs track "*.psd"）と入力して実行してください。
    - .gitattributesファイルが生成されるので、これをコミットに含めてください。
    - 通常通りgit add、git commit、git pushを実行してください。
- これで、大きなファイルがGit LFSを使って管理されるようになります。