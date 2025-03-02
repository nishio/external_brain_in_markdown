
- 実装後に一手間かけるのが嫌だなぁと思って避けていた
- `webpack --watch`がある
- チュートリアル
    - [https://webpack.js.org/guides/getting-started/](https://webpack.js.org/guides/getting-started/)
- `$ npx webpack --watch`


-----雑メモ
結局のところ、各時点で、その時点での適切なライブラリを選択してインストールしないとこける、ということだと思った
詳細に書いても次回やるときにはどうせまた動かないのでメモしない
[https://www.valentinog.com/blog/react-webpack-babel/](https://www.valentinog.com/blog/react-webpack-babel/)

- npm init -y
- npm install webpack webpack-cli --save-dev
- npx webpack --mode=development
    - まあJSXを使っているのでこける
- npm i --save-dev babel-core babel-loader babel-preset-env babel-preset-react
- npm i -S react react-dom
    - -S == --save

- > Error: Cannot find module '@babel/core'
- >  babel-loader@8 requires Babel 7.x (the package '@babel/core'). If you'd like to use Babel 6.x ('babel-core'), you should install 'babel-loader@7'.
`$ npm i --save-dev @babel/core`
- > Error: Plugin/Preset files are not allowed to export objects, only functions. In /Users/nishio/grouping/node_modules/babel-preset-react/lib/index.js
`$ npm i -S @babel/preset-react`

