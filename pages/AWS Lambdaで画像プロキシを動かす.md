
[[キャンバス汚染解決編]]で書いたプロキシサーバをAWS Lambdaで動かせるか検討

生の環境ではrequestsが動かないのでそれごと入れるか、使わないで書き直す必要がある
`$ pip3 install requests --target .`

Lambdaから画像のようなバイナリデータを返すのには追加で色々やる必要がある
- めんどくさいな…
- 2020/01/07 今確認したらパススルーができそうだった
    - [https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-payload-encodings-configure-with-console.html](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-payload-encodings-configure-with-console.html)

- [【新機能】Amazon API Gatewayを使ってAWS LambdaをSDKなしでHTTPS越しに操作する ｜ Developers.IO](https://dev.classmethod.jp/cloud/aws/lambda-restful-api-by-using-api-gateway/)
- [lambdaに外部モジュールを読み込ませる | ハックノート](https://hacknote.jp/archives/48083/)
- [image - How to return binary data from lambda function in AWS in Python? - Stack Overflow](https://stackoverflow.com/questions/44860486/how-to-return-binary-data-from-lambda-function-in-aws-in-python)
