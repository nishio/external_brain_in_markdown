
GPT-4での移植がどの程度現実的なのか試す
- 関連 GPT-4に書かせました[/villagepump/Twitter to Scrapbox GPT](https://scrapbox.io/villagepump/Twitter to Scrapbox GPT)
- 結果
    - 一発で移植したコードが出てきた
    - わかりやすいバグとわかりにくいバグが入ってた
    - わかりにくいバグはGPTにエラーメッセージを見せても見当違いなことをいったので、何が起きているのかを観察して理解する必要があった
    - 原因がわかってからの修正方法はGPT4が即答した
    - リファクタリングを命じたらちゃんとリファクタリングしたけど、わかりにくいバグが入った
    - 自分で移植するのとどっちが速いのかはGPT4が書いたコードのデバッグ能力に依存しそう
    - 今回のケースではTypeScriptは自分で読めるけど、読んで確認することはゼロだった。読めない言語からでも移植できるのが強みか？

下記のTypeScriptのコードをPythonにする
[https://github.com/meganii/sandbox-github-actions-scheduler/blob/main/index.ts](https://github.com/meganii/sandbox-github-actions-scheduler/blob/main/index.ts)

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Convert following TypeScript to Python: ...


-----
<img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>Here's the TypeScript code converted to Python:
[https://github.com/nishio/gpt4_translation_example/commit/ff49c64881de59214536fdb5a6588454864b6b10](https://github.com/nishio/gpt4_translation_example/commit/ff49c64881de59214536fdb5a6588454864b6b10)

This Python script uses asyncio and aiohttp for handling asynchronous tasks and HTTP requests, respectively. You might need to install the aiohttp library using the following command:

`$ pip install aiohttp`

---
と言われたけどまあvenvを作りますね
`$ python3 -mvenv venv`
`$ . venv/bin/activate`
`$ pip install aiohttp`

----
実行してみる
:

```
  File "/Users/nishio/etude-github-actions/main.py", line 58
    print(f"[page {j}@scrapbox-external-backup] start fetching "/{project}/{titles[j].title}"")
          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
SyntaxError: invalid syntax. Perhaps you forgot a comma?
```


fix1
[https://github.com/nishio/gpt4_translation_example/commit/6d89f04c19d27d89ab3fac410e6d7c654f616ab4](https://github.com/nishio/gpt4_translation_example/commit/6d89f04c19d27d89ab3fac410e6d7c654f616ab4)

-----
:

```
aiohttp.client_exceptions.ContentTypeError: 0, message='Attempt to decode JSON with unexpected mimetype
```

おや、エラーだ。
とりあえず適当にエラーメッセージを入れてみよう

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
:

```
File "/Users/nishio/etude-github-actions/main.py", line 87, in <module>
    asyncio.run(main())

aiohttp.client_exceptions.ContentTypeError: 0, message='Attempt to decode JSON with unexpected mimetype
```


<img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>
The error you encountered is caused by the aiohttp library expecting the response content type to be application/json. However, the API response may have a different content type. To fix this issue, you can update the fetch function to ignore the content type when attempting to decode the JSON response.

Replace the existing fetch function with the following:

python

```
async def fetch(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.json(content_type=None)
```


This modification will allow the fetch function to decode the JSON response without considering the content type.

感想
- 直らないね
- ![image](https://gyazo.com/3dc6fe724108e0bfa1010465fc2910c5/thumb/1000)
- うーん、この修正が妥当かどうか疑わしいな

-----
文字コードの問題？(追記: 誤った推測)
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
For `return await response.json()`, specify it is UTF-8
<img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>
The response.json() method uses the charset specified in the HTTP response's Content-Type header to decode the response text. If the server sends a response with the correct Content-Type header that includes the charset, the response should be decoded correctly. However, if you want to ensure that the response is always decoded as UTF-8, you can modify the fetch function to read the response bytes and decode them using UTF-8 explicitly.

Replace the existing fetch function with the following:

:

```
async def fetch(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            response_bytes = await response.read()
            response_text = response_bytes.decode('utf-8')
            return json.loads(response_text)
```

This modification will explicitly decode the response using UTF-8 before parsing it as JSON.

感想
- 解決しないけどとりあえずresponse_bytesをprintしたらb'The requested page was not found'だった
- 結果がこれである場合にスキップするようにしたら進み出した
- どのような時にこうなるのか確認するために問題になるURLを出力
- →ページタイトルにピリオドやスラッシュが入っている！

なるほど、こういうことね。TypeScriptとPythonでデフォルトの挙動が異なることに起因する移植ミスだ
python

```
>>> from urllib.parse import quote
>>> quote("aaa.bbb/fff")
'aaa.bbb/fff'
```


<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>How to quote period and slash in URI segment?
<img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>
To percent-encode special characters like period (.) and slash (/) in a URI segment, you can use Python's urllib.parse.quote() function and provide a custom string of safe characters. By default, the quote() function considers period (.) and slash (/) as safe characters, so they won't be percent-encoded. To override this behavior, you can pass an empty string as the safe parameter:

python

```
from urllib.parse import quote

uri_segment = "example.com/path"
encoded_segment = quote(uri_segment, safe='')

print(encoded_segment)
```


Output:

:

```
example%2Ecom%2Fpath
```


In this example, both the period (.) and slash (/) are percent-encoded. You can customize the safe parameter to include any characters that you want to keep unencoded.

fix 2
[https://github.com/nishio/gpt4_translation_example/commit/993f07457a7ffd52b4dc10b7517a75cce05f5126](https://github.com/nishio/gpt4_translation_example/commit/993f07457a7ffd52b4dc10b7517a75cce05f5126)
動いた！
----
リファクタリングさせる
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Refactor following codes. Make long string templates constants. Use namedtuple for the data class.
<img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>
I've refactored the code to use namedtuple for the data class and moved long string templates into constants:
...
I've replaced the TitlePage class with a namedtuple for better simplicity and performance. Additionally, the URL_TEMPLATE and LIMIT_PARAM constants have been introduced to improve code readability.
[https://github.com/nishio/gpt4_translation_example/commit/8f54713b4637ba39f896ef7981627aafed3f60b2](https://github.com/nishio/gpt4_translation_example/commit/8f54713b4637ba39f896ef7981627aafed3f60b2)

-----
リファクタリングでバグを仕込んであったw
[https://github.com/nishio/gpt4_translation_example/commit/53eeb191a428a47fb95e19a7b4cfb9b658caee90](https://github.com/nishio/gpt4_translation_example/commit/53eeb191a428a47fb95e19a7b4cfb9b658caee90)
