
Q: 自作のモデルを設置した仮想空間をoculus goで見るところまでに何をする必要がありますか？当方3D知識はメタセコで止まってます。[Facebook](https://www.facebook.com/nishiohirokazu/posts/10215457336603119)

A:
1. Blenderなどでモデルを作る（あるいは3D会社に課金する）
2. Oculus Go の開発者モードをonにする（過程で、開発団体登録する）
3. [[Unity]] でAndroidアプリをビルドできるようにセットアップし、XRサポートでOculusを有効にする
4. Unity にモデルをインポートして、メインカメラを置く
5. Oculus Go を PC に繋いで、Build and Run

手順2と3の参考
[http://www.yoshidayo.com/entry/2018/05/09/103503](http://www.yoshidayo.com/entry/2018/05/09/103503)
- 2018-06-04時点でAPI Level 25はないって言われるのでTargetは27にした
- 一応ビルドはできて、何かが見えた
- 終了の仕方がわからない

- オブジェクトの置き方がわからない
    - 物が置けないと正しく見えてるのかもよくわからない
    - [[Unityでのレイアウト]] [http://www.atmarkit.co.jp/ait/articles/1410/27/news037_3.html](http://www.atmarkit.co.jp/ait/articles/1410/27/news037_3.html)
    - HierarchyからCreateを押して適当にやればできる
        - [http://www.atmarkit.co.jp/ait/articles/1411/06/news040.html](http://www.atmarkit.co.jp/ait/articles/1411/06/news040.html)
- オブジェクトのfbxファイルをどうやっておけばよいかがわからない
    - [https://docs.unity3d.com/jp/460/Manual/HOWTO-importObject.html](https://docs.unity3d.com/jp/460/Manual/HOWTO-importObject.html)
    - プロジェクトフォルダに置けばよいらしい
    - ドラッグドロップでもいい

- [[Oculus Utilities for Unity]]を入れる
    - [https://developer.oculus.com/downloads/package/oculus-utilities-for-unity-5/](https://developer.oculus.com/downloads/package/oculus-utilities-for-unity-5/)
    - ダウンロードして展開しAssetsフォルダに入れる


Q: カメラが操作に応じて動くように実装を書かなきゃいけないのかな…

A:
Unityの標準のVRサポート機能により、シーン内のカメラが（コードを何も書かなくても）勝手に首を振るようになります。
細かく設定したいときや、コントローラのモデルをシーン内に表示したい時は、AssetStore から [[Oculus Integration]] を落としてきて、[[OVRCameraRig]] や [[TrackedRemote prefab]] を使用してください。


