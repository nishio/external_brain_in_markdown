
2023-01-11

[https://github.com/nishio/kozaneba](https://github.com/nishio/kozaneba)
- Gitは入れてあった

VSCodeで開く
- 入れてあった

`$ npm start`
`zsh: command not found: npm`
npmがない
- [Downloading and installing Node.js and npm | npm Docs](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
- `$ node -v`
- `zsh: command not found: node`
- なるほどNodeが入ってない
    - nvm入れる
        - [https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)
        - `$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash`
- nvmでnodeを入れる
    - `$ nvm install --lts`
- `$ node -v`
- `v18.13.0`
- Node, OK
`$ npm install -g npm`
`% npm -v`
`9.2.0`
npm, OK

`% npm start`
`sh: react-scripts: command not found`
- [[create-react-app]]で作ったんだったな

`$ npm install react-scripts@latest`
:

```
npm ERR! code ERESOLVE
npm ERR! ERESOLVE could not resolve
...
npm ERR! Conflicting peer dependency: @types/react@16.14.34
...
npm ERR! Fix the upstream dependency conflict, or retry
npm ERR! this command with --force or --legacy-peer-deps
npm ERR! to accept an incorrect (and potentially broken) dependency resolution.
...
```

(注: ここは`npm install`すべきでは？)

- [[Conflicting peer dependency]]について調べる
- [How do I read npm "conflicting peer dependency" error messages? - Stack Overflow](https://stackoverflow.com/questions/67185714/how-do-i-read-npm-conflicting-peer-dependency-error-messages)
    - >  Check out Yarn.
    - `$ npm i -g yarn`
    - `$ yarn install`
    - `success Saved lockfile.`
    - OK
    - (注: 問題なく動いたが、そもそもnpm installではダメだったのか？確認せずに進んでしまった)

`$ npm start`
![image](https://gyazo.com/1ece088f5d6d285b74482f1ffc83f00f/thumb/1000)
:

```
Compiled successfully!

You can now view movidea in the browser.
  Local:            http://localhost:3000
```

無事開発環境が動くようになった

本番環境はどこだっけ？？
Netlify
- ![image](https://gyazo.com/eb5f650e05499d8fb3e0676f002b4f67/thumb/1000)
    - ![image](https://gyazo.com/bbed211e32805f5ee5058434fda828b5/thumb/1000)
    - なんか警告出てるな

-----
![image](https://gyazo.com/d54afcbefdc0349da03520d938520011/thumb/1000)


-----
`error expect@29.3.1: The engine "node" is incompatible with this module. Expected version "^14.15.0 || ^16.10.0 || >=18.0.0". Got "12.18.0"`

> You can choose the Node.js version we use to build your site ...
- [https://docs.netlify.com/configure-builds/manage-dependencies/](https://docs.netlify.com/configure-builds/manage-dependencies/)
- `$ echo "lts/*" > .nvmrc`
