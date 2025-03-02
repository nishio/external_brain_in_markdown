---
title: "Firestoreに複雑なオブジェクトを入れる"
---

[[聞き出しチャットシステム]]の環境オブジェクトを[[Firestore]]に入れた

- 1: obj.__dict__をそのまま入れようとする
    - →`"Cannot convert to a Firestore Value"`
    - いくつかのフィールドがFirestoreに入れられない型
- 2: jsonに変換
    - [[defaultdict]]がdictに変わって、後の使用でKeyError
    - tupleがlistに変わる
        - これはdictのkeyに使っているのでlistに揃えることはできない
        - 変換関数を書く

複雑なオブジェクトのシリアライズは落とし穴がいっぱい
はまりだしてから書いたけど、最初から「入れたものが元どおりになるかどうかのテスト」を書くべきだったね。
