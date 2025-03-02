
- [[Slack]]のOutgoing Webhookの返信で表示されたメッセージはまたOutgoing Webhookを発生させる
    - Mattermostではそんなことはないんだけどね。
- なのでトリガーワードなしで発言する[[ボット]]は、自分の発言にトリガーされてまた発言する
- 1秒1回に制限されているようではあるが本質的な解決にはなってない
- Outgoing Webhookでの発言はusenameがslackbotになるので、その場合に無視をすれば良い
