---
title: "Sentryでエラー時にUser Feedbackのフォームを出す"
---

from [[Sentry Memo]]
[[Sentry]] User Feedback
![image](https://gyazo.com/acaeefbdd92094f9ebfebfc4fb086cb4/thumb/1000)
- [React Error Boundary for React | Sentry Documentation](https://docs.sentry.io/platforms/javascript/guides/react/components/errorboundary/)
    - [User Feedback for React | Sentry Documentation](https://docs.sentry.io/platforms/javascript/guides/react/enriching-events/user-feedback/)
    - エラーが起きた時にそれをユーザに伝えたい
        - コンソールにエラーメッセージが出てるだけだと伝わらない
    - エラー時にそれを伝えてユーザからフィードバックを集めるダイアログがプリセットされてる
        - これを出せば良いか
        - ユーザが書いてくれるとは期待してないけど、自分が使ってる時なら何をしてて起きたかここから送信できるし、それがSentryのサーバ上でスタックトレースとかとセットで読める
    - 故意にエラーを発生させるメニューを作って試す
    - `<Sentry.ErrorBoundary fallback="An error has occurred" showDialog>`
        - developだとReactのエラー画面が出て、消すと元の画面。productionだと何も出ない
    - 自前で送信前にフックして表示する
ts

```typescript
Sentry.init({...
  beforeSend(event, hint) {
    // Check if it is an exception, and if so, show the report dialog
    if (event.exception) {
      Sentry.showReportDialog({ eventId: event.event_id });
    }
    return event;
  },
});
```

        - developだとエラー画面の下にフィードバック画面が出てる
            - ID重複の警告が出てる
            - フィードバック画面がそもそも2枚出てる
            - showDialogとの重複かと思ったが、消しても変わらない
            - エラーIDやタイムスタンプの異なるエラーが2回発生している
                - 内容は同じ
                - Sentry上でのイベント回数表示も2ずつ増えてる
            - エラーバウンダリーのせいで2回出るのか？と思ったが、有無と関係ない
            - →1回だけ表示するための処理を自前でやることにした

考察
- メニューを選択した時のイベントハンドラの中で起きたエラーに関して、エラーバウンダリーどは捕捉されないのかな？
    - そういうことらしい
    - [https://ja.reactjs.org/docs/error-boundaries.html](https://ja.reactjs.org/docs/error-boundaries.html)
    - > error boundary は自身の子コンポーネントツリーで発生した JavaScript エラーをキャッチし、エラーを記録し、クラッシュしたコンポーネントツリーの代わりにフォールバック用の UI を表示する React コンポーネントです。
    - > error boundary は以下のエラーをキャッチしません：
        - >  イベントハンドラ（詳細）
        - >  非同期コード（例：setTimeout や requestAnimationFrame のコールバック）
- なぜ2回出るのか
    - Reactが一旦キャッチしてから再スローしてんのかな
