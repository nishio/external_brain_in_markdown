
ts

```typescript
  const { id } = router.query;
  const topicId = Array.isArray(id) ? id[0]! : id!;
  useEffect(() => {
    get_topic(topicId).then(...);
  }, [topicId]);
```


<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>上記のコードで問題が起こっている箇所は useEffect が実行されるタイミングです。router.query から id を取得し、それを topicId に代入していますが、この操作はページが初めてロードされたときに実行されます。このとき router.isReady はまだ false である可能性があり、したがって router.query はまだ空である可能性があります。その結果、 topicId は undefined になります。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>なんで初回レンダリング時にルートが確定してないんだよ...
[[Next.js]]
