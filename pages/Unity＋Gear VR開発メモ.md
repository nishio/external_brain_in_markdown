
[Unity＋Gear VR開発メモ - フレームシンセシス](https://framesynthesis.jp/tech/unity/gearvr/)
#Unity #GearVR

[[アンチエイリアシング]]について
- [[vrdaveb]]氏のおすすめ
    - [[Player Settings]]で[[Rendering Path]]をForwardにする
        - [[Graphic Settings]]かも？
        - デフォルトで既にForward
    - Quality SettingsのAnti AliasingでMulti Sampling（[[MSAA]]）をかける
- MSAAはImage Effectsのアンチエイリアス（[[FXAA]]）よりも軽量
- ポリゴンのエッジがずっと綺麗
- Gear VRでは2x MSAAはほぼノーコスト
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>8xまでやったけどきれいに思えなかった
    - [[FXAA]]したので[[MSAA]]はdisableにしたが、2xまでノーコストとの話なので2xにしてみた
