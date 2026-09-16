---
title: "grasp"
---

![image](https://gyazo.com/5372fa212043b4d5985dfb8571b6b704/thumb/1000)


![image](https://gyazo.com/34145c985c60f2d33c3ab586bcbd4b01/thumb/1000)
- [[wiki森]]のそれぞれが[[Markdownの束]]な[[KarpathyのLLM Wiki]]であるか[[Cosense]]であるかに関係なく[[すべてを包括して掴む]]grasp
- [https://github.com/nishio/grasp](https://github.com/nishio/grasp)

[/villagepump/grasp](https://scrapbox.io/villagepump/grasp)

2026-07-30
- 数日前から[[Opus5]]と組み合わせて使っている
    - その前にはFableと組み合わせていることを<img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/nishio/Fable/icon' alt='Fable.icon' height="19.5"/>という形で表現していたが面倒になったので<img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>だけで表現している

AIは下記のようなコマンドを叩いて検索する
- > for q in '図でしか' '絵でしか' '言葉にならない' 'ベン図' '囲み' '囲む' '関係の網目' '一目で' '一望'; do echo "### $q"; grasp --project nishio search "$q" --limit 6 2>&1 | grep -E '^- ' | head -6; done
