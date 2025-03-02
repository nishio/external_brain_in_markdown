---
title: "OpenAI Project API Key"
---

`User API keys have been replaced by project API keys.`

[Managing your work in the API platform with Projects | OpenAI Help Center](https://help.openai.com/en/articles/9186755-managing-your-work-in-the-api-platform-with-projects)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>この文書は、OpenAIのAPIプラットフォームにおけるプロジェクトの管理方法について説明しています。要点は以下の通りです。
- プロジェクトを使うことで、組織内の作業を整理することができる。プロジェクト内でアクセス権限や利用制限の管理、使用状況の追跡などが可能。
- プロジェクトを作成できるのは組織のオーナーのみ。各組織にはデフォルトプロジェクトが用意されている。
- プロジェクトにはオーナーとメンバーというロールがあり、権限が異なる。オーナーはプロジェクト設定の変更やメンバー管理ができるが、メンバーはAPIを使った推論などに限定される。
- サービスアカウントは疑似ユーザーのようなもので、個人アカウントとは区別される。システムアクセス用に使われる。
- 組織レベルとプロジェクトレベルで利用制限を設定できる。プロジェクトの制限は組織の制限以下に設定する必要がある。
- ユーザーは複数のプロジェクトに所属できる。プロジェクトごとにAPIキーを発行して、そのプロジェクト内でのみ使用可能。
- 現在のところ、プロジェクト間でのリソース移動はサポートされていない。使わなくなったプロジェクトは、メンバーを外して名前を変更することで廃止扱いにするのが推奨される。

以上のように、OpenAIのAPIプラットフォームではプロジェクト単位で作業を管理し、きめ細かなアクセス制御や利用制限の設定ができるようになっています。
