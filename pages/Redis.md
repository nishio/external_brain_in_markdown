---
title: "Redis"
---


<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
簡単な方法としては、以下の2つがおすすめです。

- Dockerを利用する:
- 公式Redisイメージで
- docker run -d --name redis -p 6379:6379 redis
- と実行するだけで、短時間でRedisサーバーが立ち上がります

- Homebrewでインストール（macOSの場合）:
- brew update && brew install redis
- redis-server
- でローカル環境で起動できます

また、クラウドサービスのマネージドRedis（例：Amazon ElastiCacheなど）を利用すると、運用負荷を大幅に軽減できます。