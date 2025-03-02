---
title: "Prettier"
---

コードをキレイな見た目にする作業はほとんど自動化できるので人間がやるべきでない

[[VSCode]]で拡張を入れる
- [Prettier - Code formatter - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

全部のファイルをフォーマットする
- `$ npx prettier --write .`

編集時に自動でフォーマットする
- Cmd+Shift+P: Configure Language Specific Settings
settings.json

```json
{
  ...
  "editor.formatOnPaste": true,
  "editor.formatOnSave": true,
  "editor.formatOnType": true,
	...   
  "[typescript]": {
	...
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
	...
```


まあ、ちょっと気に入らないときもあるのだけど、それを通すために設定ファイルを頑張っても不毛なので素直に従うことにしている。



--- old

`$ npm install --save-dev prettier`
`$ ./node_modules/.bin/prettier --write src/*.ts`
[[VSCode]]: [[prettier-vscode]] Cmd+Shift+P: Configure Language Specific Settings
settings.json

```json
{
  "editor.fontSize": 16,
	...
  "editor.formatOnPaste": true,
  "editor.formatOnSave": true,
  "editor.formatOnType": true,
  "editor.tabSize": 2,
  "editor.detectIndentation": true,
	...   
  "[typescript]": {
    "editor.insertSpaces": true,
    "editor.tabSize": 2,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
	...
```


- Cmd+Shift+P: Prettier create config file
- Prettier config
json

```json
{
  "tabWidth": 2,
  "useTabs": false,
  "overrides": [
    {
      "files": ["*.ts", "*.tsx"],
      "options": {
        "trailingComma": "all"
      }
    }
  ]
}
```

