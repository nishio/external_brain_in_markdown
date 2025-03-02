---
title: "Supabaseの書き込みがサイレントに失敗する"
---

ts

```typescript
await supabase.from("foo_table").insert({...})...
```


SupabaseのAPIは失敗時に[[例外]]を投げるのではなく、[[Result型]]を返す設計になっている。
なので、失敗時に例外を投げる設計のつもりで使っているとサイレントに失敗する。

例外を投げたいならこう
ts

```typescript
const {data, error} = await supabase.from("foo_table").insert({...})...
if (error) {
    throw new Error(`Failed to insert data: ${error.message}`);
}
```


<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>TypeScriptでクラウドデータベースを使用する際に例外を使うエラーハンドリングが必ずしも最適でない理由
- エラー復旧: データベース操作でエラーが発生した場合、例外を投げて処理を中断するよりも、エラー状態からの復旧や再試行を試みる方が適切な場合があります。例えば、タイムアウトや一時的な接続問題に対してリトライするロジックを実装することが考えられます。
- APIの設計: クラウドデータベースを操作するライブラリやAPIでは、エラーレスポンスを詳細に返すことで、利用者が自分の用途に合わせたエラーハンドリングを実装できるようにするのが一般的です。これにより、例外を投げる代わりにエラーコードやエラーメッセージを利用して、より柔軟にエラーを処理することが可能になります。