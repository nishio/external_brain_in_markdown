
- ハッカソンなど限られた時間でPoCを作る際に使えそうなものをメモ

- [ngrok - secure introspectable tunnels to localhost](https://ngrok.com/)
    - [noelportugal/google-home-notifier: Send notifications to Google Home](https://github.com/noelportugal/google-home-notifier) の中で使われていた
    - サーバをローカルで立てて、そのまま外からアクセス可能にする
    - 単なるWebサービスだったら「適当な外のサーバにデプロイしたらいいじゃん」ってなるところだけど、例えばローカルのネットワークにつながっているIoT機器のことを考えると有用
    - [[ngrok]]

- Google Home Notifier
    - [noelportugal/google-home-notifier: Send notifications to Google Home](https://github.com/noelportugal/google-home-notifier)
    - Google Home Miniを日本語でしゃべらせることができた
    - トラップ
        - apt-getでnode.jsをインストールすると古いのでnpm installで失敗する
            - [公式インストール方法](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions)
        - dns_sd.hがない
            - > sudo apt-get install libavahi-compat-libdnssd-dev
        - npm install -gしてない時はローカルフォルダ`node_modules`にインストールされている
        - google-home-notifier自身はインストールされない。ファイル単体を相対参照でrequireしてる
            - > var googlehome = require('./google-home-notifier');
        - ipを指定するメソッドにはlang引数がないので、第2引数で言語を渡しても無視されて英語モードのまま
            - google-home-notifier側をいじって引数を取るようにした

- [IFTTT Webhooks service](https://ifttt.com/maker_webhooks)
    - かつてMaker Channelと呼ばれてたもの [Introducing the Maker Channel](https://ifttt.com/blog/2015/06/introducing-the-maker-channel)
        - > The Maker Channel has been renamed — it's now the Webhooks service!

- [Firebase](https://firebase.google.com/)
    - > Firebase is Google's mobile platform that helps you quickly develop high-quality apps and grow your business.
