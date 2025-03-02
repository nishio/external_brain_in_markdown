
[[Heroku]]
- Install [[Heroku CLI]]
    - [https://devcenter.heroku.com/articles/heroku-cli#install-the-heroku-cli](https://devcenter.heroku.com/articles/heroku-cli#install-the-heroku-cli)
- Run your app locally
    - [https://devcenter.heroku.com/articles/heroku-local](https://devcenter.heroku.com/articles/heroku-local)
- gunicornがない
    - そもそもvenvあるのになんでそんなことになるの？
    - pip install -r requirements.txt
    - numpy, scikit-learn, scipy, mecab-python3などがコケる
    - なんでだ？
- そもそもこれデプロイ通るの？
    - あ、通った
    - Herokuの中ではPython3.8だな
- ローカルが3.9なので何か食い違ってるのだな
    - [[mecab on heroku]]もあやしそう

- `$ brew install python@3.8`
    - mecab-python3がコケる
        - そもそもmecabとswigが足りないbrewで入れる
- `$ brew install llvm`
- 動いた！

会話ログ
- [[Keichobot+GPTテスト2023-03-06]]
- [[LLMと回帰テストとA/Bテスト]]

ネクストアクション
- 要約コマンド欲しい
- オリジナルの出力を活用するプロンプトに変える

[[Keichobot開発日記2023-03-07]]

[[Keichobot開発日記]]
[[Keichobot]]
