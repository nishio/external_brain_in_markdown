---
title: "2024年夏Polis祭り"
---

2024年夏、いまPolisを立てると面白いのでは？と思ったのでやっていく([[Polis2024年夏]])
- [[デジタル民主主義]]的には[[アジェンダ設定の権限を人々に開放する]]のが良いこと
- [[Talk to the City]]はOSSなので誰でもできるが、とはいえエンジニアしかできない
- もっと広い範囲の人々が「参加」できるデジタル民主主義祭り(2024年夏Polis祭り)をやりたい

方針
- 誰でも会話を開始できるようにする(特定の陣営に限定しない)
- 個人と紐づくデータを取らない(TwitterやFacebookとの連携をしない)
- すべての入力を[[オープンデータ]]とする

-----
公開済みリスト
- [選挙ポスターに対する議論](https://polis.nhiro.org/6kvuuursmy)
    - [[Polis準備:選挙ポスター]]
- [自治体DXにおける情報システム共通化](https://polis.nhiro.org/6spai5zjrr)
- [0歳からの投票権](https://polis.nhiro.org/29uzxjufe9)
- [新しい民主主義](https://polis.nhiro.org/2fsjcfkkpz)
    - [[Polis準備: 新しい民主主義]]
- [神宮外苑再開発に関する議論(ver2)](https://polis.nhiro.org/4udffmr5yy)
    - [ver1](https://polis.nhiro.org/m/9herb9baam)
- [公職選挙法違反に対する議論](https://polis.nhiro.org/4mudryyhwn)

テンプレ
- ~に関する議論の場です。みなさんは意見に対して賛成反対を投じたり、新しい意見を投稿することができます。
- 投稿・投票内容は個人が特定されない形でオープンデータにする予定です。

----- 作業ログ

2024-06-18~22 [[2024年夏Polis祭り:インスタンスの準備]]

2024-06-22
明日以降にすること
- サーバが動くまでの話を切り出す
- 変更したファイルをcommitする
- conversationをつくる、voteする、commentする、reportをみる、データを見る、を一通りやる


[[Polis準備:選挙ポスター]]
![image](https://gyazo.com/bf0a4308ba38a456005e2529d782e134/thumb/1000)
自分がconversationつくると自分が投票済みになる...
- 7人投票したら可視化も表示された


2024-06-23
![image](https://gyazo.com/0b83de49032550645aa3548e696798e6/thumb/1000)
SNSと紐付けない

Tasks
- ✅サーバが動くまでの話を切り出す
- 変更したファイルをcommitする
- ✅conversationをつくる、voteする、commentする
- reportをみる
- データを見る


js

```javascript
convasation_id = "6kvuuursmy"
report_id = "r4xnu5hwjajhsebyfbehb"
data = await fetch(`/api/v3/math/pca2?lastVoteTimestamp=0&conversation_id=${convasation_id}`).then(x=>x.json());
not_sorted_comments = await fetch(`/api/v3/comments?conversation_id=${convasation_id}&report_id=${report_id}&moderation=true&mod_gt=-1&include_voting_patterns=true`).then(x=>x.json());
comments = [];
not_sorted_comments.forEach(c=>{
    comments[c.tid] = c;
})
```



個別
js

```javascript
groupid = 0;
repness = data.repness[groupid];
result = "" 
repness.forEach((r)=>{
    c = comments[r.tid];
    overall = `Overall Group: Agree: ${c.agree_count}, Disagree: ${c.disagree_count}, Pass: ${c.pass_count}, Total: ${c.count}`;
    g = data["group-votes"][groupid].votes[r.tid]
    group = `This Group: Agree: ${g.A}, Disagree: ${g.D}, Pass: ${g.S - g.A - g.D}, Total: ${g.S}`;
    result += `${c.txt}\n${overall}\n${group}\n\n`;
})
console.log(result);
```


全部
js

```javascript
for (let groupid = 0; groupid < 5; groupid++) {
    const repness = data.repness[groupid];
    let result = "";

    repness.forEach((r) => {
        const c = comments[r.tid];
        const overall = `Overall Group: Agree: ${c.agree_count}, Disagree: ${c.disagree_count}, Pass: ${c.pass_count}, Total: ${c.count}`;
        const g = data["group-votes"][groupid].votes[r.tid];
        const group = `This Group: Agree: ${g.A}, Disagree: ${g.D}, Pass: ${g.S - g.A - g.D}, Total: ${g.S}`;
        result += `${c.txt}\n${overall}\n${group}\n\n`;
    });
    let groupChar = String.fromCharCode('A'.charCodeAt(0) + groupid);
    console.log(`Result for Group ${groupChar}:\n${result}`);
}
```



Claude 3.5 Sonnet
:

```
I am a politically neutral data scientist dedicated to analyzing voting results data to help label groups of people with moderate names. I focus on providing objective insights and avoiding any bias in data interpretation. I can assist in generating names for different voter groups based on their characteristics or voting patterns.
Output should be in Japanese.

Group A
猥褻な選挙ポスターは表現の自由の範囲内である。
Overall Group: Agree: 5, Disagree: 10, Pass: 4, Total: 19
...
```

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>ご要望に基づき、各グループの特徴を反映した中立的な名称を日本語で提案いたします：
- Group A: 「表現自由重視派」
    - このグループは、選挙ポスターにおける表現の自由を重視し、奇抜な手法も戦略として認める傾向があります。
- Group B: 「規制慎重派」
    - このグループは、選挙制度の悪用には反対しつつも、ポスターの内容規制や警察の介入には慎重な姿勢を示しています。
- Group C: 「民主主義原則派」
    - このグループは、民主主義の原則を重視しつつ、公共の場における適切性と表現の自由のバランスを求める傾向があります。
これらの名称は、各グループの投票パターンを客観的に反映しつつ、過度に偏った解釈を避けるよう配慮しています。

10件コメントきた
- Claude 3.5 Sonnetにモデレーションさせた

Unmoderated 10
選挙ポスターにかぎらず、性的な表現の掲示物は、子供だけでなく大人も含め「みたくない人」がいることを念頭に置いて議論すべきです。台湾や北欧では、性的な掲示物を見ることが少なかったように思いますが、性にあり方や自己の選択、人々の快適性に配慮しているのではないかと思います。
選挙ポスターは本来自由であるべきだが、それが法を犯す表現かどうかを事前に確認するため警察を利用することを勧める。ただし、利用はあくまで任意である。
選挙ポスターは、立候補者本人が発行すべきである。選挙ポスターを本人以外が広告手段として利用することを禁じる。
制限の内容は、立候補者の名前が必ず入ることや該当の選挙に対する自身の主張とすることとするべきだ。
そもそも、ポスターの意義が薄くなってきていると思いますので、廃止がベターだと考えます。
選挙ポスターであっても他の法制度に従うべき
そもそも選挙ポスターに求められるのは表現ではない
ポルノとヌードは異なる。今回問題視されているのは前者
禁止事項を増やすというより、そもそも選挙ポスターはもっと条件を制約した方が良い
ポスターの貼り付けが新規参入障壁になっているので最初から貼り付けたものを掲示するべきだ

~2024-06-25
[[Polis準備:選挙ポスター]]
[[Polis準備:自治体DXの情報システム共通化]]
[[Polis準備:0歳投票権]]
[[Polis準備:神宮外苑再開発]]

2024-06-25
EC2でgit cloneしたためid_rsaなどがなくてpush時に認証を求められてしまいます。GitHubはpassword認証をもうやってないと思います。id_rsaの設置は行ったけど、clone済みのrepositoryをどうしたらいいかわかりません

ChatGPT
既にクローンしたリポジトリでSSHキーを使って認証するように設定するには、リモートリポジトリのURLをHTTPSからSSHに変更する必要があります。以下の手順で行ってください。

現在のリモートリポジトリのURLを確認します：

git remote -v
リモートリポジトリのURLをSSHに変更します：

bash
コードをコピーする
git remote set-url origin git@github.com:ユーザー名/リポジトリ名.git
これで、SSHキーを使用してGitHubにアクセスできるようになります。git pushコマンドを実行すると、SSHキーを使用した認証が行われます。


`$ git remote -v`
origin  [https://github.com/nishio/polis.git](https://github.com/nishio/polis.git) (fetch)
origin  [https://github.com/nishio/polis.git](https://github.com/nishio/polis.git) (push)

`$ git remote set-url origin git@github.com:nishio/polis.git`

`$ git push`
:

```
The authenticity of host 'github.com (140.82.112.3)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
```

yes

pushできた
ここ数日の成果
[https://github.com/nishio/polis/commit/d8fee6cb9fbe938950fc54fa148fed619440301f](https://github.com/nishio/polis/commit/d8fee6cb9fbe938950fc54fa148fed619440301f)

次はローカル環境でこれを動かす


Polisのシード追加がめんどい問題
![image](https://gyazo.com/1e69883fb9834768d71f3e64924b5fc7/thumb/1000)

![image](https://gyazo.com/014e528d9e71620e16f4063e0f55dddc/thumb/1000)
![image](https://gyazo.com/46d61e54cd900b059315417ba1bdcc3d/thumb/1000)


2024-06-26
オープンデータのための口をつける話、そもそもあんまり意見が集まってないので保留

もっとPolisをどんどんやっていくといいかな

投稿してから誤植に気づいても修正できない問題
- まあ、手軽に変更ができると賛成の投票が集まってから別の意味のものに変えて民意の捏造ができるからなぁ
- とはいえデータベースを編集しちゃえば可能ではある
- 多分暗号系の人が改竄不能な投票方法を考えてそう

button = document.querySelector("#root > div > div.css-vurnku > div > div.css-ppq56n > div > div:nth-child(7) > div.css-vurnku > button")


/api/v3/comments
{txt: "a", pid: "mypid", conversation_id: "7dnp9ma5nv", is_seed: true}

js

```javascript
// 複数行のテキストを文字列として定義
const multiLineText = `最初のコメント

次のコメント

最後のコメント`;

// 改行で分割し、空白行を取り除いて配列にする
const texts = multiLineText.split('\n').filter(line => line.trim() !== '');
```


conversation_idを変えるのを忘れないようにね
js

```javascript
// APIを呼び出す非同期関数
async function postComments(texts) {
    const apiUrl = '/api/v3/comments';

    for (const text of texts) {
        const data = {
            txt: text,
            pid: 'mypid',
            conversation_id: '7dnp9ma5nv',
            is_seed: true
        };

        try {
            const response = await fetch(apiUrl, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data)
            });

            if (!response.ok) {
                throw new Error(`HTTP error! status: ${response.status}`);
            }

            const result = await response.json();
            console.log('Response:', result);
        } catch (error) {
            console.error('Error posting comment:', error);
        }
    }
}

// 関数を呼び出してAPIにテキストを送信
postComments(texts);
```


複数行のまとめ投稿、できた


2024-06-27
> [nishio](https://x.com/nishio/status/1806226862525538537) (Claude)各グループの特徴を見て、以下のような名前を提案します：
>  グループA: 「規制重視派」
>  選挙の公平性のための規制や、金銭の影響力抑制のための規制に賛成する傾向が強い。
>
>  グループB: 「自由表現派」
>  表現の自由を重視し、規制に反対する傾向がある。選挙運動の自由度を重視している。
>
>  グループC: 「中立バランス派」
>  賛成・反対が分かれる傾向があり、状況に応じて判断する柔軟な姿勢が見られる。
>
>  グループD: 「選挙秩序派」
>  選挙期間中の行動や表現に制限を設けることに賛成する傾向が強い。
>
>  グループE: 「自由市場派」
>  選挙関連の商業活動や表現の自由を重視する傾向がある。
>
>  これらの名前は、各グループの投票パターンや意見の傾向を反映しつつ、過度に政治的な表現を避けるよう心がけています。データの解釈に基づいた客観的な分類を目指しています。
>  ![image](https://pbs.twimg.com/media/GREBviObQAAXhJG?format=jpg&name=medium#.png)

> [nishio](https://x.com/nishio/status/1806227134920393120) 投票はこちら
>  [https://polis.nhiro.org/4mudryyhwn](https://polis.nhiro.org/4mudryyhwn)
>  レポートはこちら
>  [https://polis.nhiro.org/report/r8kaansrbxtwu5wfrvitm…](https://polis.nhiro.org/report/r8kaansrbxtwu5wfrvitm…)
>
>  #デジタル民主主義

> [nishio](https://x.com/nishio/status/1806231332508631105) もしかしたら画像のA〜Eと解説のA〜Eがズレてるかも(中立派は真ん中では？みたいな気持ち)
>  試行錯誤実験してる段階なのでご理解ください！


> [nishio](https://x.com/nishio/status/1806229343892582751) (Claude)各グループの投票パターンに基づいて、中立的な名称を日本語で提案いたします：
>  グループA: 「現状維持派」 このグループは再開発に対して慎重な姿勢を示し、現状を維持したい傾向があります。
>  グループB: 「行政判断尊重派」 このグループは行政の決定を尊重し、再開発を都知事選の争点にすべきでないと考えています。
>  グループC: 「市民参加推進派」 このグループは市民の意見を重視し、より多くの情報公開と協議を求めています。
>  グループD: 「慎重な再開発支持派」 このグループは再開発の必要性を認識しつつ、透明性と公共性を重視しています。
>  ![image](https://pbs.twimg.com/media/GRECvJfbUAApui7?format=jpg&name=medium#.png)

> [nishio](https://x.com/nishio/status/1806229480324657197) 投票はこちら
>  [https://polis.nhiro.org/4udffmr5yy](https://polis.nhiro.org/4udffmr5yy)
>  レポートはこちら
>  [https://polis.nhiro.org/report/r36bmkx37pa635xd6xmek…](https://polis.nhiro.org/report/r36bmkx37pa635xd6xmek…)

