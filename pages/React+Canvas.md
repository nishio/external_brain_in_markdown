---
title: "React+Canvas"
---

[[React]]+[[Canvas]]
- [Using React Hooks with canvas – ITNEXT](https://itnext.io/using-react-hooks-with-canvas-f188d6e416c0)
    - 1
        - Path2D
        - useRefで生のCanvasを掴んで書き込んでいる
    - 2
        - useStateでユーザの操作ログを持つ
    - 3
        - クリック時に直接描く代わりに、useEffectで描いている
            - setXで状態が更新されるのでrenderが走り、useEffectが呼ばれる
            - 全てのクリックを描き直しているので性能問題が出るのでは？
            - > In the current implementation every render first clears the canvas and then draws all the locations. We could be smarter than that, but to keep it simple I’ll leave it to reader to further optimize this.
        - > drawing on the canvas is a side effect determined by the app state
        - Clearは履歴の削除、Undoはsliceに相当する
    - localStorage
        - 履歴を保存するだけ
    - カスタムフックで状態の永続化のためのフックを束ねる

