
js

```javascript
function doGet(e){
	return ContentService.createTextOutput("hello world!");
}
```

![image](https://gyazo.com/c4096e11e30e87152dfeb5842dcd1053/thumb/1000)
Test web app for your latest code.では期待した出力が出るのにデプロイすると出ないと悩んだ
- →Project versionをNewにしていないとキャッシュされる

[[Google Apps Script]]
