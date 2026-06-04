---
title: "複数AIエージェントに共通のDBを読ませる"
---

[agmsg](https://x.com/fujibee/status/2059357190725783892) 2026-05-27
> (GPT)特徴はまさに：
> Claude Code, Codex, Gemini CLI などのCLIエージェントが、共有SQLite DB 経由でメッセージをやり取りする。
> READMEにも「No daemon, no network」「shared SQLite database」「Claude Code, Codex, Gemini CLI…」とあります。

[[kouchou-ai-developer-wiki]]では[[KarpathyのLLM Wiki]]をClaude CodeとCodexが読んで開発をしている
- これは「ファイルシステム上のWiki」というデータベースを各エージェントが共有している仕組み

この「データベース」の部分を、RDBMSを使ってより明確に構造化したりすることもできる
- それがagmsgの発想

僕の[[annotation-wiki]]は人間のアノテーションの情報をSQLiteに溜めるところまではやっていたが、それを各Wikiに渡すところを設計していなかった
- annotation-wiki側でexportすると各々のWikiのrawにテキスト形式で出力される仕組みになっていた、雑
- 各wikiの側のagentがSQLiteを読みにくればいいんじゃないか、という気づき(2026-06-02)

