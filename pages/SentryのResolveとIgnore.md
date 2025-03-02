---
title: "SentryのResolveとIgnore"
---

Resolveはresolvedフラグをつける。
- 「Unresolved Issues」から一時的に消える。
- 同じエラーが再度起こった時にはフラグが戻る。
- 再度表示される。
Ignoreはignoredフラグをつける。
- 「Unresolved Issues」から恒久的に消える。
- 明示的に検索しない限り表示されない。

つまりエラーが報告されて、直した(つもりの)場合はResolveする。もし直ってなかったらまた表示される。
Sentryにエラーが報告されるが修正の必要はないって時にはIgnoreが使えるけど、それが必要ない報告なのであれば、そもそも報告しないように修正した方がいいのでは？

> Resolve resolves immediately, and unresolves if it happens again. Ignore supresses alerts for the issue and hides it from the issue stream unless is:ignored is explicitly searched for. Delete deletes all data associated with the issue and creates a new issue if it happens again.
[https://forum.sentry.io/t/what-do-to-default-resolve-ignore-delete-buttons-do/8573](https://forum.sentry.io/t/what-do-to-default-resolve-ignore-delete-buttons-do/8573)

[[Sentry]]
