---
title: "2025年初頭のChatGPT音声会話"
---

<img src='https://scrapbox.io/api/pages/nishio/Codex/icon' alt='Codex.icon' height="19.5"/>
2025年初頭の[[ChatGPT]]には、Standard Voice（標準音声）と[[Advanced Voice]]（高度な音声）という、仕組みの異なる二つの音声会話が併存していた。
- 音声で会話できるという点は共通していたが、応答の自然さや、既存のテキスト情報を使える条件に違いがあった。

### Standard VoiceとAdvanced Voiceの違い
音声会話の比較
| 観点 | Standard Voice | Advanced Voice |
| -- | -- | -- |
| 処理の流れ | 音声を文字起こし→テキスト用モデルが回答→音声合成で読み上げ | GPT-4oが音声を直接受け取り、音声を生成 |
| 会話の感触 | 処理の段階が多く、応答に間が生じやすい | 低遅延で、途中の割り込みにも対応 |
| 声の情報 | 主に文字起こしされた内容を扱う | 話す速さや声の調子なども扱える |
| 事前のテキスト投入 | テキストから始めたチャットを音声で続けられた | 当時は、テキストを送信済みのチャットから開始できない制約があった |
処理方式の違いは[OpenAIの説明](https://help.openai.com/en/articles/20001638-retiring-advanced-and-standard-voice-in-chatgpt)に基づく。
- この説明は後年のものなので、当時の切り替え条件の根拠とは分ける。
テキストからの切り替え条件は、[2025年1月12日の利用者の実測報告](https://community.openai.com/t/feature-request-advanced-voice-mode-keeps-interrupting-me/962909/32)や[2025年2月4日のiOSでの実測報告](https://community.openai.com/t/advanced-voice-mode-inferior-to-legacy-mode/1035324/14)に残っている。

### 「事前プロンプトが使えない」の意味
Advanced Voiceでは、設定画面のCustom InstructionsとMemoryは、すでに2024年9月に追加されていた。
- [OpenAIの2024年9月24日の発表](https://x.com/OpenAI/status/1838642444365369814)
- そのため、指示や事前知識を一切使えなかったわけではない。
問題になったのは、その回に使いたい資料を通常のテキストメッセージとして渡し、それを踏まえてAdvanced Voiceで話すことだった。
- テキストを先に送るとStandard Voiceになり、Advanced Voiceを使うには新しいチャットを求められる、という挙動が報告されている。
- [2024年12月26日の報告](https://community.openai.com/t/advanced-voice-mode-inferior-to-legacy-mode/1035324/7)
- Custom Instructionsへの対応と、通常チャットに投入した資料の引き継ぎは、別の条件として考える必要がある。

### 西尾のAIタスク管理実験との関係
2025年1月、西尾は音声会話やAIエージェントとの会話ログからタスクを抽出し、文脈を含むJSONとして蓄積していた。
- 1月27日には、108件のタスクが入った`backlog.json`ができていた。
- Devinなどがそれを読み、状況に合う次の行動を提案するところは動いていた。
- [[AIタスク管理2025-01-27]]
目指していたのは、その情報を把握した相手と散歩しながら相談することだった。
- JSONを先にテキストで渡すとAdvanced Voiceを使えないという制約は、この流れを妨げる。
- 音声で話したログを後からタスク管理AIに渡す運用はできていたが、蓄積済みの情報を音声対話へ戻す部分に難しさがあった。
- [[AIタスク管理システム2025-01-08]]
[[2025振り返り]]には、テキストからJSONへの変換はできたが、Advanced Voiceに事前プロンプトを入れられず、その知識を使えなかったと記している。
1月13日には、チャットログを読ませてから「Advanced Voice」で案内を受けようとした記録もある。
- [[AIエージェント飲み会]]
- 実際にはStandard Voiceで動いていた可能性があり、この記録だけでは使用モードを確定できない。

### その後の変化と例外
2025年4月26日には、文字や画像を事前に入れた通常チャットでもAdvanced Voiceを使えるようになった、という利用報告がある。
- 同じ報告ではProjectsとCustom GPTsは未対応とされている。
- 情報の渡し方ごとに対応状況が異なっていた。
- [2025年4月26日の報告](https://community.openai.com/t/advanced-voice-mode-limited/959015/94)
macOSでは2024年12月19日から、対応アプリの内容をAdvanced Voiceで参照する「Talk with apps」も提供されていた。
- [公式macOS更新履歴](https://help.openai.com/en/articles/9703738-macos-app-release-notes)
- したがって、当時の制約は「文字情報を全く使えない」ではなく、端末・チャットの状態・情報の渡し方によって、Advanced Voiceを使える条件が限られていたと捉えるのが適切である。

### 調査上の留保
2026-11-14に当時の記録と公式情報を調査して整理した。
テキストからの切り替え制限とその解除時期は、当時の日付がある利用者報告による。
- これらはOpenAI公式の仕様保証ではない。
- 少なくとも一部の環境では2025年2月初めまで制約が残り、4月下旬までには解除されていたと絞れるが、正確な解除日や全ユーザーへの展開日は未確認。
- 西尾の各実験で使われたモード・アプリの版番号は未確認。
- 通常のテキスト貼り付け、JSONファイル添付、Projectへの資料登録は別の条件であり、今回強く裏付けられたのは「テキストを送信済みのチャット」の制約。
当時の公式FAQは現在版に置き換わっている。
- Internet Archiveで保存版の存在は確認できたが、本文取得はアクセス制限で失敗したため、その保存本文による検証はできていない。