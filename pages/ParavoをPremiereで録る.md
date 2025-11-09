---
title: "ParavoをPremiereで録る"
---

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
Premiere内で録音（ボイスオーバー）
- トラックヘッダーで R（Record）ボタンを有効化
- Shift + Space で録音開始（停止はもう一度 Space）
- タイムラインに WAV クリップが生成される

Premiere Pro に取り込むには (1) Paravo でマイク→Paravo→仮想オーディオデバイスへルーティング し、(2) Premiere Pro の Audio Hardware 設定でその仮想デバイスを「Default Input」に指定 するだけです 。

1 | Paravo のセットアップ
手順	要点
① ダウンロード&インストール	公式ランチャーから β 版を取得し、ウィザードに従う
jp.imyfone.com
② 入力デバイスを設定	マイクを選択し、事前録音/キャリブレーションを行うと変換精度が上がる
jp.imyfone.com
③ 出力デバイスを設定	「仮想オーディオケーブル」を選ぶ（後述）
④ 遅延チェック	変換速度スライダーを上げればレイテンシ低減


2 | 仮想オーディオデバイスを用意する
macOS の王道 2 ルート
BlackHole 16ch（無料）	オープンソース・ゼロレイテンシ。Apple Silicon もネイティブ対応

Paravo の Output を BlackHole／Loopback の Input に指定。

Audio MIDI Setup › “＋” > Create Aggregate Device で
仮想ケーブル＋スピーカーをまとめ、録音とモニタリングを同時に可能にする