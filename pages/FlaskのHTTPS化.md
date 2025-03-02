
answered Dec 5 '20 by Mark Dominusの回答
python

```
import ssl
context = ssl.SSLContext()
context.load_cert_chain('fullchain.pem', 'privkey.pem')
...
app.run(…, ssl_context=context)
```

'fullchain.pem', 'privkey.pem'は [[LetsEncrypt Certbot]] が作る

[rest - can you add HTTPS functionality to a python flask web server? - Stack Overflow](https://stackoverflow.com/questions/29458548/can-you-add-https-functionality-to-a-python-flask-web-server)
[[Flask]] [[HTTPS]]

`$ flask run --cert fullchain.pem --key privkey.pem`
[python - Run Flask dev server over HTTPS using CLI - Stack Overflow](https://stackoverflow.com/questions/48467835/run-flask-dev-server-over-https-using-cli)
