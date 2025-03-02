
[[Sentry Memo]]


[[クラッシュ レポート]]
[Application Monitoring and Error Tracking Software | Sentry](https://sentry.io/welcome/)

Getting Started - Docs
[https://docs.sentry.io/error-reporting/quickstart/?platform=browsernpm](https://docs.sentry.io/error-reporting/quickstart/?platform=browsernpm)

ts

```typescript
Sentry.init({
  dsn:
    "https://....ingest.sentry.io/...",
});
Sentry.captureMessage("Something went wrong"); 
```


js

```javascript
Sentry.configureScope(function(scope) {
  scope.setExtra("character_name", "Mighty Fighter");
});
```


> Be aware of maximum payload size - There are times, when you may want to send the whole application state as extra data. This is not recommended as application state can be very large and easily exceed the 200kB maximum that Sentry has on individual event payloads. When this happens, you’ll get an HTTP Error 413 Payload Too Large message as the server response or (when keepalive: true is set as fetch parameter), the request will stay in the pending state forever (eg. in Chrome).

![image](https://gyazo.com/f3d11ea932fa3d84bca24195fd619bd9/thumb/1000)
マウスダウンの処理にエンバグしたことで、マウスムーブでどっさりエラーが送られてる。短時間にたくさん送らないようにできるかな…

[Breadcrumbs - Docs](https://docs.sentry.io/enriching-error-data/breadcrumbs/?platform=browsernpm)
