---
title: "Unityちゃんの一人称視点"
---

- カメラのオフセットが(0, 1.4, 0.05)だと下を見たときに自然に自分の胸元が見える
    - ![image](https://gyazo.com/cf067db791e294d5772cc76529728de9/thumb/1000)
    - Unityマークのアクセサリをつけていることに初めて気づいた
    - この位置が、横を向いたときに見える腕との位置関係では割としっくりくる
    - ![image](https://gyazo.com/dd1704ce84b8198e6e08864baf4c8ba8/thumb/1000)
    - しかしすごく下を向くと体にめり込んで体内が見える
        - 実際にはすでに体の中にめり込んでいて、頭はカメラに近すぎる物が描画されてないことで裏面が見えない
        - そもそも裏面ポリゴンを描画しないオプションはないのか？
    - 横を向くと髪の毛が視界に入る
    - とりあえず干渉しそうなものをDisableしてみた
        - ![image](https://gyazo.com/ace60de05f561095393a4df519fe8740/thumb/1000)


- 本当はカメラの向きの移動に合わせて顔のボーンが回転するべき
- (0, 1.4, 0.15)だと下を向いてもめり込まないが、足先が見える感じでちょっと違和感

