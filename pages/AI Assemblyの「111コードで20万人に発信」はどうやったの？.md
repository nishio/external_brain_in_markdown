---
title: "AI Assemblyの「111コードで20万人に発信」はどうやったの？"
---

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
「[[AI Assembly]]（市民熟議アセンブリ）」で 111 から20万人にSMSを送れた理由は、ざっくり言うと “政府が番号を知っていた”のではなく、通信事業者が持っている加入者番号に対して、[[111プラットフォーム]]経由で（事業者側で）ランダム送信した からです。
ポイントを分解するとこうです：

1) 送信先の番号は「通信会社が持っている」
- 携帯番号は契約情報として 通信会社（Chunghwaなどのキャリア）が保有しています。政府が全国民の番号名簿を持っている必要はありません。

2) 111は「政府の送信元ID（短碼）」で、送信は111プラットフォーム経由
- MODAの説明では、111は政府機関だけが使える短い送信元番号で、政府機関は111プラットフォームを使って送ります（不正利用防止のための統制もある）。([moda.gov.tw](https://moda.gov.tw/en/press/press-releases/8607))

3) 「20万人にランダム送信」＝（キャリア側で）ランダムな番号を抽出して送った
- MODAの“Alignment Assemblies”のページに、**「200,000 government 111 text messages were randomly sent out」**と明記されています。([moda.gov.tw](https://moda.gov.tw/en/major-policies/alignment-assemblies/2024-deliberative-assembly/1521))
- Audrey Tangの講演・インタビュー文字起こしでも「random numbers」に送った旨が繰り返し出てきます。([iHeart](https://www.iheart.com/podcast/269-firing-line-with-margaret-107826697/episode/can-technology-save-democracy-taiwans-cyber-299949024/))
- ここでの「random numbers」は、現実的には キャリアが自社の加入者番号プールから乱択して送るのが自然です（政府が番号リストを作って乱択、だと個人情報の塊になります）。

4) 政府側（111プラットフォーム）は、受信者番号を保持しない設計だと説明されている
- MODAの別のプレスリリースでは、送信後に111プラットフォームは受信者情報を保持しないと書かれています。([moda.gov.tw](https://moda.gov.tw/en/press/press-releases/16458))
    - （= 送信のオペレーションはできても、「政府が番号DBを恒常的に持つ」形を避ける設計思想が示されています）

5) その後の「参加者選抜」は、返信（応募）してきた人から層化抽出
20万人に打って、返ってきた有効回答（例：1760）から、性別・年齢・居住地などで 母集団比に合わせる層化（stratified） をした、とあります。([moda.gov.tw](https://moda.gov.tw/en/major-policies/alignment-assemblies/2024-deliberative-assembly/1521))
Audreyの説明でも「volunteer → stratified random sampling」という流れが語られています。([SayIt](https://sayit.archive.tw/speaker/audrey-tang-2?page=25))
