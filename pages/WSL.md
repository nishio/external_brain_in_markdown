
Windows Sybsystem for Linux


2022-08-28
- [[Stable Diffusion]]
- `\\wsl$`
- [Get started using VS Code with WSL | Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode)
- [Configuring SSH access into WSL 1 and WSL 2 - Julio Merino (jmmv.dev)](https://jmmv.dev/2022/02/wsl-ssh-access.html)
- [Developing in the Windows Subsystem for Linux with Visual Studio Code](https://code.visualstudio.com/docs/remote/wsl)


2018-05-21
自宅のゲーム用PCにWSLを入れようかなと思ったのでメモ
- [Windows 10でLinuxプログラムを利用可能にするWSL（Windows Subsystem for Linux）をインストールする（バージョン1803対応版）：Tech TIPS - ＠IT](http://www.atmarkit.co.jp/ait/articles/1608/08/news039.html)

- Ubuntuを入れた
- gitは入っていた
- 秘密鍵をコピー、設定
    - /mnt/c がWindowsのCドライブ
- gitでcloneできた
    - パーミッションの変化をチェンジセットに入れられないように
        - `git config --global core.filemode false`

- ターミナルへの貼り付けは右クリック

- tmuxがデフォルトで入ってる
- makeが入ってない

