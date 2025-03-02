
from [[pKeicho]]
[[Add to Home screen]]したい
- [[✅アイコンを子供っぽい見た目にする]]
- ✅マニフェストのタイトルを変える
- ![image](https://gyazo.com/50638968ef44e55955367a72cc9d4965/thumb/1000)
- 高さに問題がでる
    - 適切な高さを設定で記憶するか…
    - 問題が何なのか確認
- ログ表示した後URLがコピペできない
    - Keichoを「ホーム画面に出す」して使ったらログ共有メニュー選んでもURLがコピーできないことに気づいた
    - 別タブで開くんじゃなくてURLをクリップボードに入れる設計にした方がよかったか
    - 「ホーム画面に出す」をした時にローカルストレージは共有されるのかされないのか。
    - →[[✅ログ共有を別タブで開くんじゃなくダイアログにする]]
- display: browser にすればブラウザで開く
    - [https://pwa-workshop.js.org/1-manifest/#manifest-fields](https://pwa-workshop.js.org/1-manifest/#manifest-fields)
    - [display - Web app manifests | MDN](https://developer.mozilla.org/en-US/docs/Web/Manifest/display)
    - ブラウザUIが出なかったのはstandaloneになってたからだった
    - これで上記二つの問題は回避できる
