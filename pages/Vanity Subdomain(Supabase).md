---
title: "Vanity Subdomain(Supabase)"
---


Q: [[Google Auth]]と[[Supabase]]の連携でGoogleでのログインフォームに iykeevfgoyncgpprgfhi.supabase.co などと表示されて見栄えが悪い

[Custom Domains | Supabase Docs](https://supabase.com/docs/guides/platform/custom-domains)
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
- ポイントはGoogleの同意画面に出るドメイン＝OAuthのリダイレクトURIのドメインということです。デフォルトのままだと xxxxx.supabase.co が表示されますが、SupabaseのCustom Domainを使えば自前ドメインにできます。
    - auth.omorate.jp を作って、ここをSupabase Authのエンドポイントにします（有料アドオン/Pro以上）。これでGoogleの画面も「omorate.jp で続行」の表示になります。
- Vanity Subdomain（実験的）：omorate.supabase.co のように任意の文字列へ変更（CLIのみ）。完全自社ドメインよりは劣りますが、ランダム文字列よりは見栄えが良くなります。
[https://chatgpt.com/share/690da1b2-968c-8011-b230-48843155c358](https://chatgpt.com/share/690da1b2-968c-8011-b230-48843155c358)
