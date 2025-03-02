
(4/9更新)  Zoomの4/4の修正に伴い「アプリをインストールせずにブラウザだけで参加する人」に関して、今まではURLを知っているだけで参加できたものが、Zoomアカウントでログインしなければ参加できない状態だった。4/6の修正により、アカウント不要にする設定が可能になった。

> April 6, 2020 [src](https://support.zoom.us/hc/en-us/articles/204758419-New-Updates-for-Web)
- >  New and enhanced features
    - >  Admin features
        - >  Added setting “Only authenticated users can join meetings from Web client”
        - >  By default, users will now need to sign in to their Zoom account or create a Zoom account when joining a meeting with the web client. This setting is available at the account, group, and user level and can be locked at the account or group level.

![image](https://gyazo.com/13d1a6ef8f9121173dba17c3db34878d/thumb/1000)
- このオプションをオフにすればアカウントを持たないユーザも参加可能
- もちろんログイン不要にすることはリスクを増やすが、セキュリティと利便性はトレードオフ
- 追加されたばかりの機能で翻訳が間に合っていない。今後翻訳されて見た目が変わる可能性がある



---以下 過去ログ

> Zoomの4/4の修正に伴い、「アプリをインストールせずにブラウザだけで参加する人」に関して、今まではURLを知っているだけで参加できたものが、Zoomアカウントでログインしなければ参加できないように変わりました。
>
> これ自体は、万が一好ましくない参加者が入ってしまって追い出した時に、その人が再度入室するのを防ぐ効果があります。
> でも、この仕様変更に気付いていない方が「以前と同じようにやろう」と考えていると、当日バタバタするかも知れないので、ここで念のためお知らせしておきます。
[Facebookの情報共有グループに書いた](https://www.facebook.com/groups/146940180042907/permalink/150895796314012?sfns=mo)のをこちらに転載しておく

一次ソース
[https://support.zoom.us/hc/en-us/articles/204758419-New-Updates-for-Web](https://support.zoom.us/hc/en-us/articles/204758419-New-Updates-for-Web)
> April 4, 2020
- > Changes to existing features
    - > New join flow for the web client
        - >  Users will now need to sign in to their Zoom account or create a Zoom account when joining a meeting with the web client.

---
ここから先は組織単位で契約してSSOしているケースの話

4/7現在、下記の不具合が存在する。

組織単位で契約してSSOしているアカウントが作成した会議室に、アプリをインストールしないでブラウザから参加しようとした時に、同様にログインが求められる。しかしそのログイン画面がその組織のSSO画面になる不具合があり、組織外のゲストがその方法で参加しようとしている場合、ログインできないので会議に参加できない。

こういうケースでは組織名をfoobarとして下記のような会議室URLになっている
[https://foobar.zoom.us/j/88888888888?pwd=xxxxxxxxx](https://foobar.zoom.us/j/88888888888?pwd=xxxxxxxxx)
これを下記のように書き換えるとSSOでないログインができる
[https://zoom.us/j/88888888888?pwd=xxxxxxxxx](https://zoom.us/j/88888888888?pwd=xxxxxxxxx)
条件に該当するユーザは会議室URLを共有する時に上記の書き換えを行うと良い
