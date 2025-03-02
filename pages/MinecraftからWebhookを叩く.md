
[https://github.com/Akenland/SimpleWebhooks](https://github.com/Akenland/SimpleWebhooks)
config.yaml

```yaml
webhooks:
  other:
    test:
      url: https://mattermost.example.org/hooks/XXXXXXXX
      json:
        text: "hello!"
```

コマンド
- `webhooks execute test`
結果
- SlackクローンのMattermostで受け取れた。Slackでも動くだろう。
- ![image](https://gyazo.com/cd5205e3479adb70b38b7db760ff9917/thumb/1000)


Incoming Webhookを持ってるサービスがだいたい全部マイクラ起点でトリガーできるようになる。
