
![image](https://gyazo.com/e1b043d657fea88b8fb75f94f810873d/thumb/1000)

- インターネット接続のない状況でnet::ERR_INTERNET_DISCONNECTEDが出る(これはわかる)
- オフラインでも使えるようにしたいのでエラーで死なないでほしい
- どうやってエラー処理するんだ？？
    - firebase.initializeAppもfirebase.firestoreもPromiseではない
    - firebase.initializeAppとfirebase.firestoreをtryで囲ってもダメ
- Reactの側でエラー処理すべき
    - [Error Boundaries – React](https://reactjs.org/docs/error-boundaries.html)
    - > componentDidCatch and getDerivedStateFromError: There are no Hook equivalents for these methods yet, but they will be added soon.
        - [Hooks FAQ – React](https://reactjs.org/docs/hooks-faq.html)
        - FCでできない
    - class ErrorBoundaryを作って解決した
    - 今はcomponentDidCatchで単にconsole.logしている
        - 将来的には[[Sentry]]とかにつなぐとよい

[[pKakidashi]]
