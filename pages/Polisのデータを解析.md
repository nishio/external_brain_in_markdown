

[[EC2でPolis]]
- [https://polis.nhiro.org/3bbdm2tsss](https://polis.nhiro.org/3bbdm2tsss)
- ![image](https://gyazo.com/41dbf7cf1ac885827d28dc9bbbae9d20/thumb/1000)
- 59 people

[[PolisのDBからデータをエクスポート]]
- [https://gist.github.com/nishio/897cdad38e9a797917f7b8e5a27c7524](https://gist.github.com/nishio/897cdad38e9a797917f7b8e5a27c7524)

py

```
import pandas as pd
df = pd.read_csv("/Users/nishio/Downloads/polis.csv")
matrix = df.pivot_table(index="pid", columns="tid", values="vote")
print(matrix)
```


![image](https://gyazo.com/e08623d52b83779b1db863dfb491d2c9/thumb/1000)
75 rows

[https://github.com/compdemocracy/analysis/blob/master/notebooks/jupyter/american-assembly-representative-groups-and-comments.ipynb](https://github.com/compdemocracy/analysis/blob/master/notebooks/jupyter/american-assembly-representative-groups-and-comments.ipynb)

py

```
matrix = matrix.dropna(thresh=3)
print(matrix.shape)
# => (59, 8)
```

論文には7が閾値って書いてあったけど実際は3のようだ

K-3
![image](https://gyazo.com/02458b971fbad2068ab060ce0575a508/thumb/1000)

[[Polis: Scaling Deliberation by Mapping High Dimensional Opinion Spaces]]

![image](https://gyazo.com/024b99a6ea894895dc345ffb441bff82/thumb/1000)

![image](https://gyazo.com/39b7589b772d69ec0f047da7daa3a5e0/thumb/1000)

![image](https://gyazo.com/26de6308bf8b358fad9a85c240c925c2/thumb/1000)

![image](https://gyazo.com/2828ca1c6ea1d4eab64c78677cd05ac0/thumb/1000)![image](https://gyazo.com/41dbf7cf1ac885827d28dc9bbbae9d20/thumb/1000)
0 12
1 36
2 11
うーん、それっぽい絵はできたけど結果が一致しないな

[[2023-06-22CodeReading]]

できた
- ![image](https://gyazo.com/8a746a484dff28c8c0971b0b0207b3cb/thumb/1000)
:

```
comment 7
Count of +1 votes in group:  0.0
Count of 0 votes in group:  2.0
Count of -1 votes in group:  12.0
 
Count of +1 votes outside group:  19.0
Count of 0 votes outside group:  19.0
Count of -1 votes outside group:  7.0
 
pvalue:  5.840739168435112e-05
```

Polisのバックエンド実装を使わずに、投票データのCSVからPolisのクラスタわけやクラスタごとの「特徴的な回答」を計算できるようになった

2023-06-22
![image](https://gyazo.com/f3fec605e6fa35612f21ad1a1c3cd461/thumb/1000)![image](https://gyazo.com/41dbf7cf1ac885827d28dc9bbbae9d20/thumb/1000)

![image](https://gyazo.com/f6e42bdef2612da442f54e526178edba/thumb/1000)
