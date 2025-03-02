
pPolis2023-06-04
- PolisのDBからデータをエクスポートした

[/yuiseki/pol.is スクレイピング](https://scrapbox.io/yuiseki/pol.is スクレイピング)
- > pol.isの自分の過去の投票データを取得して、いろいろやりたい
- > [[Cloudflare]]の強力なWAFだかbot managementだかが有効化されていて、スクレイピングの難易度が超高い

インスタンスを立てたらデータを出せるだろうかという話題になり、立てて投票を集めるところまではやったという話をした
- [[EC2でPolis]]

[Export  pol-is/polis-documentation · GitHub](https://github.com/pol-is/polis-documentation/blob/master/data/Export.md)
- > Data can be exported from the admin page for a conversation.
    - そんなメニュー見当たらない…
    - pol.isではオフにしてあるってことかな
- API `https://pol.is/api/v3/dataExport?conversation_id=4jbpxizvxf&format=csv`
    - `{}`になる
- pg_dumpしたらいいかな

:

```
$ psql
Command 'psql' not found, but can be installed with:
$ sudo apt install postgresql-client-common
$ psql
Warning: No existing cluster is suitable as a default target. Please see man pg_wrapper(1) how to specify one.
Error: You must install at least one postgresql-client-<version> package
```


:

```
$ sudo apt update
$ sudo apt install postgresql-client
$ psql
psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: No such file or directory
        Is the server running locally and accepting connections on that socket?
```


:

```
$ docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED       STATUS                   PORTS                                                                                  NAMES
12be7e86bdf7   compdem/polis-nginx-proxy:dev   "/docker-entrypoint.…"   11 days ago   Up 8 minutes             0.0.0.0:80->80/tcp, :::80->80/tcp, 0.0.0.0:443->443/tcp, :::443->443/tcp               polis-dev-nginx-proxy-1
e605f36eaf7d   compdem/polis-server:dev        "docker-entrypoint.s…"   11 days ago   Up 8 minutes             0.0.0.0:5000->5000/tcp, :::5000->5000/tcp, 0.0.0.0:9229->9229/tcp, :::9229->9229/tcp   polis-dev-server-1
25846362cfd3   compdem/polis-math:dev          "entrypoint ./bin/run"   12 days ago   Up 8 minutes             0.0.0.0:18975->18975/tcp, :::18975->18975/tcp                                          polis-dev-math-1
20b437d2786c   maildev/maildev:1.1.1           "/home/node/bin/mail…"   12 days ago   Up 8 minutes (healthy)   0.0.0.0:1025->1025/tcp, :::1025->1025/tcp, 0.0.0.0:1080->1080/tcp, :::1080->1080/tcp   polis-dev-maildev-1
f8d749409bda   compdem/polis-postgres:dev      "docker-entrypoint.s…"   12 days ago   Up 9 minutes             0.0.0.0:5432->5432/tcp, :::5432->5432/tcp                                              polis-dev-postgres-1
8dccf50c2348   compdem/polis-file-server:dev   "docker-entrypoint.s…"   12 days ago   Up 8 minutes             0.0.0.0:8080->8080/tcp, :::8080->8080/tcp                                              polis-dev-file-server-1
```



:

```
$ psql -h localhost -p 5432
Password for user ubuntu:
```


example.env

```
###### DATABASE ######
# Optional DB replica for reads:
READ_ONLY_DATABASE_URL=
POSTGRES_DB=polis-dev
POSTGRES_HOST=postgres:5432
POSTGRES_PASSWORD=oiPorg3Nrz0yqDLE
POSTGRES_PORT=5432
POSTGRES_USER=postgres
```


:

```
$ psql -h localhost -p 5432 -U postgres
Password for user postgres: 
psql (14.8 (Ubuntu 14.8-0ubuntu0.22.04.1), server 13.4)
Type "help" for help.

postgres=# 
```


![image](https://gyazo.com/44d6190cf0820fc1f7739ee89aa32e24/thumb/1000)

:

```
\c polis-dev
\dt
```

![image](https://gyazo.com/5e53dd1760fb0812b08bcbc29ef95f33/thumb/1000)

:

```
# select * from comments where zid = 3;
```

![image](https://gyazo.com/eba7fc112842308ec172d49585623f13/thumb/1000)

:

```
polis-dev=# COPY comments TO 'comments.csv' DELIMITER ',' CSV HEADER;
ERROR:  relative path not allowed for COPY to file
polis-dev=# COPY comments TO '/home/ubuntu/comments.csv' DELIMITER ',' CSV HEADER;
ERROR:  could not open file "/home/ubuntu/comments.csv" for writing: No such file or directory
HINT:  COPY TO instructs the PostgreSQL server process to write a file. You may want a client-side facility such as psql's \copy.
```

あー、そうか、Dockerの中で動いてるからか

:

```
# \COPY comments TO '/home/ubuntu/comments.csv' DELIMITER ',' CSV HEADER;
COPY 55
```


できた

:

```
polis-dev=# \COPY (SELECT * FROM comments WHERE zid = 3) TO '/home/ubuntu/comments.csv' DELIMITER ',' CSV HEADER;
COPY 8
polis-dev=# \COPY (SELECT * FROM votes WHERE zid = 3) TO '/home/ubuntu/votes.csv' DELIMITER ',' CSV HEADER;
COPY 454
```


[https://gist.github.com/nishio/897cdad38e9a797917f7b8e5a27c7524](https://gist.github.com/nishio/897cdad38e9a797917f7b8e5a27c7524)

Postgres使ったことなかったけどGPT-4があれば何も怖くないな()
[https://chat.openai.com/share/b1ded3df-9e6c-4742-95cb-10e315e76531](https://chat.openai.com/share/b1ded3df-9e6c-4742-95cb-10e315e76531)
