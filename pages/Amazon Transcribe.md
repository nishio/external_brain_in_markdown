
やり方
- 前処理
    - Zoomから降りてくる音声ファイルはaac、これは受け付けられない
        - `$ ffmpeg -i foo.aac foo.mp3`
- 音声ファイルを[[S3 Bucket]]にアップロード
    - 同一リージョンでなければならないので注意

- Speaker Identificationをオンにする、上限人数を指定できる(6人にした)
- 書き起こしのAlternativeを表示する設定にした

![image](https://gyazo.com/39b089816a10746a0c979d1334fa2389/thumb/1000)
- 1時間の音声が40分程度で完了
    - 2019/11/28 16:07:33 / 2019/11/28 16:42:13

何を言っているのか全然わからない
> Speaker 2: 楽しめ を
>  Speaker 2: どこ
>  Speaker 1: で 食べ た 人 を 乱さ ない って いう の は
>  Speaker 1: たくさん の
>  Speaker 1:よう な 場所 を 減らす という の は やっぱり これ だけ
>  Speaker 0: じゃ ない
>  Speaker 0: サイド に 泊まれ ば 減らす って いう の は 要するに 公的 な ライバル に なっ て しまう てる 大 企業 で も 見 た こと ない です
>  Speaker 1: よ
>  Speaker 1: ね
>  Speaker 1: やっぱり 動画 情報 から です よ ね なんか 振りかける

生データはこんな感じ
:

```
 {"jobName":"Test","accountId":"736390490238","results":{"transcripts":[{"transcript":"分 として 着 られる 認知 を 目指す べき な のに そう な もの を 食べ て み たら 虹 が 一緒 だ と か あの レベル で いい です よ いや コミケ が 十分 で ない と 思い ます まあ そういう 意味 で は 日本 で は サブカル 市場 で ... けど ね 誰 だ か 分から ない けれど も この 歌 も 日本 で も やっぱり 今 まで どんな 方法 を やっ てる ん だ と 思っ て て 分類 問題 若く ない って いう よう な 情報 が ここ パリ に 違い ない これ は いう 話 でし た いや 面白い です ね 僕 も 早かっ た です ね"}],
"speaker_labels":{"speakers":6,"segments":[{"start_time":"1.16","speaker_label":"spk_2","end_time":"2.15","items":[{"start_time":"1.16","speaker_label":"spk_2","end_time":"1.47"},{"start_time":"1.47","speaker_label":"spk_2","end_time":"1.7"},{"start_time":"1.71","speaker_label":"spk_2","end_time":"1.88"},{"start_time":"1.88","speaker_label":"spk_2","end_time":"2.15"}]},{"start_time":"3.47","speaker_label":"spk_2","end_time":"5.82","items":[{"start_time":"3.47","speaker_label":"spk_2","end_time":"3.89"},{"start_time":"3.89","speaker_label":"spk_2","end_time":"3.97"},{"start_time":"3.97","speaker_label":"spk_2","end_time":"4.24"},{"start_time":"4.24","speaker_label":"spk_2","end_time":"4.42"},{"start_time":"4.42","speaker_label":"spk_2","end_time":"4.5"},{"start_time":"4.5","speaker_label":"spk_2","end_time":"4.73"},{"start_time":"4.94","speaker_label":"spk_2",
```


:

```
例えば うん 実は LENCE] 千 円 ない みたい な 感じ で そう だ! けど の 上 から 六 十 八 次元 が 寝転がる 本当 パラメーター で 変わる けど 例えば LENCE] まあ まあ 縁 の あれ で これ が どう なる か と いう と この ベクトル の 類似 度 を 計算 する こと が でき ない 敵 と か 行く いい とか という わけ ねえ 文章 の 最初 に 特別 な ん です こんな 時 に 関し て 出 て くる やつ が この LENCE] こいつ が この 文書 全体 に 対する 特徴 を 持っ て いる と 言え ば あのー 何 か あの 人 も い ない 文章 全体 から で あっ て 別 の 識別 用 調べる と 説明 し です よ そう だ ね 拍手 する と なんか ベース ライン に 比べれ ば 本来 性能 が 得 られる こと が 多い が 言う ところ の あのー ここ 計算 すごい こと な ん だ けど が 採用 さ れ まし た え ま 要する に なり まし た か と いう と その それぞれ の 文章 を ここ で 入力 と し て い ます そう する ウェブページ について 動画 でき ます よ ね 行き ます という こと は 他 の ページ も で も 何 百 六 十 八 次元 の ベクトル を 持っ て いる ので
```

これは何を話しているのか若干わかる
謎の「LENCE]」トークン
