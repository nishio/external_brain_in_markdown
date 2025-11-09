---
title: "スマホやPCを使えない人を優先する必要はない"
---

スマホやPCを使えない人を「優先」して「特別扱い」をする必要はない

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
1) デジタル化できる作業の割合（制度面・可能性ベース）
- 日本全体（国・自治体の手続き種類ベース）
    - 約50～55%がオンライン化可能（令和6年度の悉皆調査：75,071種類中オンライン化率51.6%）。 ([デジタル庁](https://www.digital.go.jp/assets/contents/node/basic_page/field_ref_resources/578b4dd0-db54-44da-9850-d76a6248c27f/628232ad/20250804_private-business-dx_outline_02.pdf?utm_source=chatgpt.com))
- 東京都（手続プロセス単位）
    - 78.9%がデジタル化済（2024/3末）。 ([シン・トセイ – 都政の構造改革ポータルサイト](https://shintosei.metro.tokyo.lg.jp/post_dashboard_20240530/?utm_source=chatgpt.com), [note（ノート）](https://note.com/kouzoukaikaku/n/n2189bc98755b?utm_source=chatgpt.com))
- 先進例：港区
    - 法令制約等を除く区受付手続は100%オンライン化（2,427/3,425）。 ([港区公式サイト](https://www.city.minato.tokyo.jp/houdou/kuse/koho/press/202403/20240327_press02.html?utm_source=chatgpt.com))

推定まとめ：平均的な市役所でも「作業の過半（5割前後）」は制度上オンライン化可能。先進自治体は8割前後まで現実路線。 ([デジタル庁](https://www.digital.go.jp/assets/contents/node/basic_page/field_ref_resources/578b4dd0-db54-44da-9850-d76a6248c27f/628232ad/20250804_private-business-dx_outline_02.pdf?utm_source=chatgpt.com), [シン・トセイ – 都政の構造改革ポータルサイト](https://shintosei.metro.tokyo.lg.jp/post_dashboard_20240530/?utm_source=chatgpt.com))

2) 実際のオンライン実施（利用）割合
- 国全体の悉皆調査では、オンライン可能な手続の「年間件数」ベース利用率が約8割まで上昇（令和6年度）。ただし手続ごとのばらつきが大きい。 ([デジタル庁](https://www.digital.go.jp/assets/contents/node/basic_page/field_ref_resources/578b4dd0-db54-44da-9850-d76a6248c27f/628232ad/20250804_private-business-dx_outline_02.pdf?utm_source=chatgpt.com))
- 例：世田谷区では**施設予約等は100%一方で児童手当認定0.4%、妊娠届0.6%**など低い分野もある。 ([行政情報ポータル](https://ai-government-portal.com/%E4%BD%8F%E6%B0%91%E5%90%91%E3%81%91%E3%82%AA%E3%83%B3%E3%83%A9%E3%82%A4%E3%83%B3%E7%94%B3%E8%AB%8B%E3%81%AE%E6%8B%A1%E5%85%85%E3%81%A8%E5%88%A9%E7%94%A8%E4%BF%83%E9%80%B2/))

推定まとめ：件数ベースの実利用率は分野依存で3～80%超まで広い。 “書類提出・予約・証明書交付”系は高率、相談・審査系は低率。 ([行政情報ポータル](https://ai-government-portal.com/%E4%BD%8F%E6%B0%91%E5%90%91%E3%81%91%E3%82%AA%E3%83%B3%E3%83%A9%E3%82%A4%E3%83%B3%E7%94%B3%E8%AB%8B%E3%81%AE%E6%8B%A1%E5%85%85%E3%81%A8%E5%88%A9%E7%94%A8%E4%BF%83%E9%80%B2/))

3) 「3割増の待ち時間」は妥当か？
- 窓口は利用率（ρ）が少し上がるだけで待ち時間が非線形に増大。区役所窓口の待ち行列最適化の研究でも、この感度の高さが前提に置かれている。 ([日本オペレーションズ・リサーチ学会](https://orsj.org/wp-content/corsj/or62-2/or62_2_75.pdf?utm_source=chatgpt.com))
- 簡易M/M/sモデルで、基準：利用率0.6～0.7、窓口能力が5%低下（=人手不足や離席増、採用難を想定）とすると、平均待ち時間は＋約25～40%程度に悪化（エルランC近似）。
→ つまり「3割増」は保守的に“あり得る”水準。

背景：自治体は採用難・若手離職増が顕在化。総務省の地方公共団体定員管理調査の公開や、各種調査でも人材確保難が継続。 ([e-Stat](https://www.e-stat.go.jp/stat-search/files?cycle=0&layout=dataset&month=12040604&stat_infid=000040248903&toukei=00200216&tstat=000001226021&year=20240&utm_source=chatgpt.com), [Maniken〜地域経営のためのあたらしいマニフェスト研究所〜 -](https://maniken.jp/blog/2745/?utm_source=chatgpt.com), [ジチタイワークス](https://jichitai.works/article/details/2660?utm_source=chatgpt.com))

4) 「手間が10%に減少」はどこまで現実的か？
- 証明書交付のセルフ化：コンビニ交付は直近、月に人口比2%台後半～5%（年30～60%）が窓口外で処理＝該当分は職員手間ほぼゼロ。 ([日本ライブラリー情報学会](https://www.j-lis.go.jp/file/%E3%83%9E%E3%82%A4%E3%83%8A%E3%83%B3%E3%83%90%E3%83%BC%E3%82%AB%E3%83%BC%E3%83%89%E5%88%A9%E6%B4%BB%E7%94%A8%E3%81%AE%E6%8B%A1%E5%A4%A7%E3%81%AB%E5%90%91%E3%81%91%E3%81%9F%E3%82%B3%E3%83%B3%E3%83%93%E3%83%8B%E4%BA%A4%E4%BB%98%E7%AD%89%E8%AA%AC%E6%98%8E%E4%BC%9A.pdf?utm_source=chatgpt.com))
- 転記・照合作業：RPA導入で平均▲64.8%、**データ入力は▲82.3%の時間削減。自治体事例でも▲85%**近い削減が出ている。 ([行政情報ポータル](https://ai-government-portal.com/ai%E3%83%BBrpa%E7%AD%89%E3%81%AB%E3%82%88%E3%82%8B%E6%A5%AD%E5%8B%99%E5%8A%B9%E7%8E%87%E5%8C%96/?utm_source=chatgpt.com), [富士電機](https://www.fujielectric.co.jp/about/column/detail/government_column002.html?utm_source=chatgpt.com))
- 「書かないワンストップ窓口」×マイナポータル：事前転記・補正連絡のオンライン化で審査以外の手間を大幅圧縮する設計が進行中。 ([デジタル庁](https://www.digital.go.jp/policies/administrative_procedures_online))

推定まとめ：
- 対象業務が“申請入力・証明書・予約”系なら、職員の1件当たり工数は実務で**10～30%**まで圧縮、**最適化が進むと“10%前後”**も十分射程。 ([行政情報ポータル](https://ai-government-portal.com/ai%E3%83%BBrpa%E7%AD%89%E3%81%AB%E3%82%88%E3%82%8B%E6%A5%AD%E5%8B%99%E5%8A%B9%E7%8E%87%E5%8C%96/?utm_source=chatgpt.com), [日本ライブラリー情報学会](https://www.j-lis.go.jp/file/%E3%83%9E%E3%82%A4%E3%83%8A%E3%83%B3%E3%83%90%E3%83%BC%E3%82%AB%E3%83%BC%E3%83%89%E5%88%A9%E6%B4%BB%E7%94%A8%E3%81%AE%E6%8B%A1%E5%A4%A7%E3%81%AB%E5%90%91%E3%81%91%E3%81%9F%E3%82%B3%E3%83%B3%E3%83%93%E3%83%8B%E4%BA%A4%E4%BB%98%E7%AD%89%E8%AA%AC%E6%98%8E%E4%BC%9A.pdf?utm_source=chatgpt.com), [デジタル庁](https://www.digital.go.jp/policies/administrative_procedures_online))
- 相談・審査・現地確認を伴う手続は30～70%削減が現実的レンジ。 ([デジタル庁](https://www.digital.go.jp/policies/administrative_procedures_online))
- 全体平均（窓口ポートフォリオ混在）では、**まずは“40～70%削減”（=手間は30～60%残）**が日本の現状に沿った一次目標。**先進自治体の設計では“20～30%残”**まで狙える。 ([シン・トセイ – 都政の構造改革ポータルサイト](https://shintosei.metro.tokyo.lg.jp/post_dashboard_20240530/?utm_source=chatgpt.com), [港区公式サイト](https://www.city.minato.tokyo.jp/houdou/kuse/koho/press/202403/20240327_press02.html?utm_source=chatgpt.com))

5) デジタルデバイド（“使えない人”の規模感）
- 個人のスマホ保有は8割超に到達（R6調査）。 ([カレントアウェアネス・ポータル](https://current.ndl.go.jp/car/253615?utm_source=chatgpt.com))
- ただし70～79歳のインターネット利用は約67%、80歳以上は約36%（R5）。
⇒ 高齢層には約3～6割の“オンライン未利用者”が残るため、窓口混在前提の設計が不可欠。 ([国立研究開発法人情報通信研究機構](https://www.nict.go.jp/info-barrierfree/relate/statistics/elder_net.html?utm_source=chatgpt.com))

ざっくり結論（日本の状況に即した推定）
- “3割増の待ち時間”：成立し得る（能力5%低下で+25～40%）。対策なしなら局所的に**+70～100%**もあり得る。 ([日本オペレーションズ・リサーチ学会](https://orsj.org/wp-content/corsj/or62-2/or62_2_75.pdf?utm_source=chatgpt.com))
- “手間を10%”：
    - 範囲限定（証明書・予約・単純申請）では妥当。
    - 庁内全体平均では現状**“30～60%残”が現実的な一次着地。先進設計で“20～30%残”**へ。 ([行政情報ポータル](https://ai-government-portal.com/ai%E3%83%BBrpa%E7%AD%89%E3%81%AB%E3%82%88%E3%82%8B%E6%A5%AD%E5%8B%99%E5%8A%B9%E7%8E%87%E5%8C%96/?utm_source=chatgpt.com), [日本ライブラリー情報学会](https://www.j-lis.go.jp/file/%E3%83%9E%E3%82%A4%E3%83%8A%E3%83%B3%E3%83%90%E3%83%BC%E3%82%AB%E3%83%BC%E3%83%89%E5%88%A9%E6%B4%BB%E7%94%A8%E3%81%AE%E6%8B%A1%E5%A4%A7%E3%81%AB%E5%90%91%E3%81%91%E3%81%9F%E3%82%B3%E3%83%B3%E3%83%93%E3%83%8B%E4%BA%A4%E4%BB%98%E7%AD%89%E8%AA%AC%E6%98%8E%E4%BC%9A.pdf?utm_source=chatgpt.com), [デジタル庁](https://www.digital.go.jp/policies/administrative_procedures_online), [シン・トセイ – 都政の構造改革ポータルサイト](https://shintosei.metro.tokyo.lg.jp/post_dashboard_20240530/?utm_source=chatgpt.com))
- “デジタル化できる作業の割合”：
    - 制度的可能性で5割強（全国）/8割（都）/100%（港区のような先進例）。
    - 実運用のオンライン実施率は手続依存で3～80%+。証明書・予約系が先に進む。 ([デジタル庁](https://www.digital.go.jp/assets/contents/node/basic_page/field_ref_resources/578b4dd0-db54-44da-9850-d76a6248c27f/628232ad/20250804_private-business-dx_outline_02.pdf?utm_source=chatgpt.com), [シン・トセイ – 都政の構造改革ポータルサイト](https://shintosei.metro.tokyo.lg.jp/post_dashboard_20240530/?utm_source=chatgpt.com), [港区公式サイト](https://www.city.minato.tokyo.jp/houdou/kuse/koho/press/202403/20240327_press02.html?utm_source=chatgpt.com), [行政情報ポータル](https://ai-government-portal.com/%E4%BD%8F%E6%B0%91%E5%90%91%E3%81%91%E3%82%AA%E3%83%B3%E3%83%A9%E3%82%A4%E3%83%B3%E7%94%B3%E8%AB%8B%E3%81%AE%E6%8B%A1%E5%85%85%E3%81%A8%E5%88%A9%E7%94%A8%E4%BF%83%E9%80%B2/))




## きっかけ
[[dd2030 slack]]
田中勇
スマホやPCの使えない世代にはどのように対応しますか？

kuboon
そういう方々も間接的にメリットを享受できるような仕組みを考えたいですね

田中勇
国民全員に、１０万円の商品券や選挙前の２万円をばら撒く代わりに、スマホをばら撒く


NISHIO Hirokazu
そういう人に対しては特に何もしなくてもいいんですよ。
現状のままデジタル化を進めない場合は人手不足によって市役所の待ち行列での待ち時間が3割増とかになるところを、スマホやPCを使えば申請者だけでなく行政職員も10%くらいの手間に減少する。この手間の削減によって、スマホやPCを使えない人の待ち時間も減る。

田中勇
必殺、情弱切り捨て:ウケる::ウケる::ウケる:

NISHIO Hirokazu
切り捨ててないですね、今までどおりの手続きはできるわけですから。