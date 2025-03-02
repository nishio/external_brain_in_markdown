---
title: "Unityプロジェクトの作り方"
---

- 初回のみ [Android開発環境の設定](https://docs.unity3d.com/Manual/android-sdksetup.html)
- 初回のみ [Organizationを作成](https://dashboard.oculus.com/)
- 3Dのプロジェクトを作成
- 初回のみ [[外部ツール]] の設定
- [[Build Settings]]の[[Platform]]をAndroidに
    - ![image](https://gyazo.com/8e9d7d6ec503d50e7954f59415439edb/thumb/1000)

- [[Edit]] > [[Project Settings]] > [[Player]] > [[XR Settings]]
    - Supported = True
    - SDK = Oculus
    - 他は知らない
    - ![image](https://gyazo.com/db0d75642a085b2a48d9e9dad184b1ef/thumb/1000)
    - これを忘れると＝[[両眼視にならない]]

- Other Settings
    - Package Name
    - Minimum API Level=7.1
    - ![image](https://gyazo.com/e9099415897ef7ce54489b4de304770f/thumb/1000)

- 個人的に
    - (0, 0, 100)あたりに何か今までと違うものを置く
        - 後からスクリーンショットなどを見返したときにどのプロジェクトかわかるので
        - ![image](https://gyazo.com/f43d85e9c0cc0ccdbef6bc27f30a7298/thumb/1000)
        - あと[[マザーモノリス]]も。
- この時点でBuild & Runして上記のような期待通りのシーンが見えることを確認する

- プロジェクトの場所
    - 見当たらないなぁと思ったらなぜかこんなところにあった
        - `C:\Users\Public\Documents\Unity Projects`

- [[Oculus Utilities for Unity]]を入れる
    - [https://developer.oculus.com/downloads/package/oculus-utilities-for-unity-5/](https://developer.oculus.com/downloads/package/oculus-utilities-for-unity-5/)
    - ダウンロードして展開しAssetsフォルダに入れる
    - もしくはAssets StoreからOculus Integrationで検索してそれを入れる
    - Oculus > VR > Prefabs
        - [[OVRPlayerController]]を入れると、物理演算の入った[[Collider]]が作られてカメラがそれの子になるので、地面がないと落ちていく
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>はそういうマップを動き回る系のゲームを作りたいわけではないので、[[OVRCameraRig]]を直接追加する
        - LeftHandAnchor, RightHandAnchorに[[TrackedRemote]]を入れる
    - ここまでやると頭の向きでカメラが動き、リモコンの向きや回転も反映されるようになるはず

-----
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>の経験談メモ
- 1つ目
    - 地面を普通のCubeにしてた
    - [[レーザーポインターでものを選ぶ]]
    - 拡大したらなぜかカメラの向きによって地面が動くようになった
- 2つ目
    - 地面を[[Terrain]]で作ったら、Oculusに書き込む用のビルドをしたときにやたら時間がかかるようになった
    - 削除したが一度作るとダメ？？
    - [[地面は不要]]
    - [[スライドの自動移動]]
    - 自分のアバターとしてUnityちゃんを使ってみようとした
        - [[Unityちゃんの一人称視点]]
- 3つ目←いまここ
