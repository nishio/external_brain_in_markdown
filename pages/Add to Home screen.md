
[[ホーム画面に追加]]、[[A2HS]]と略すこともある
- [Add to Home screen - Progressive web apps (PWAs) | MDN](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Add_to_home_screen)
- > To have a manifest file with the correct fields filled in, linked from the HTML head.
- start_urlが人によって異なる場合、manifest fileを作り分ける必要がある
    - lambdaを使うのが良さそう
    - →[[Netlify]]を使っている場合、[[Netlify Functions]]でサクッとできる
        - [Function定義](https://github.com/nishio/kakidashi/blob/master/functions/makeManifest.js)
        - [[react-helmet]]で[差し込む](https://github.com/nishio/kakidashi/blob/20d7020d6c7f077b66ee976a3f9969b986f02e88/src/App.tsx#L117-L119)

#PWA
