---
title: "TTTC: float found"
---

argument抽出の段階でNaNが混じってlabellingやvisualizationで死ぬという面倒なバグ


:

```
Running step: labelling
  0%|                                                                                    | 0/8 [00:00<?, ?it/s]
Traceback (most recent call last):
  File "/Users/nishio/election2024_broadlistening/scatter/pipeline/main.py", line 39, in <module>
    main()
  File "/Users/nishio/election2024_broadlistening/scatter/pipeline/main.py", line 35, in main
    termination(config, error=e)
  File "/Users/nishio/election2024_broadlistening/scatter/pipeline/utils.py", line 295, in termination
    raise error
  File "/Users/nishio/election2024_broadlistening/scatter/pipeline/main.py", line 27, in main
    run_step('labelling', labelling, config)
  File "/Users/nishio/election2024_broadlistening/scatter/pipeline/utils.py", line 255, in run_step
    func(config)
  File "/Users/nishio/election2024_broadlistening/scatter/pipeline/steps/labelling.py", line 44, in labelling
    label = generate_label(question, args_sample,
  File "/Users/nishio/election2024_broadlistening/scatter/pipeline/steps/labelling.py", line 55, in generate_label
    outside = '\n * ' + '\n * '.join(args_sample_outside)
TypeError: sequence item 6: expected str instance, float found
```


:

```
['教員の負担を減らしてほしい。' '予算の多い東京から教員の負担軽減を進めてほしい。'
 '都独自の教員確保・処遇改善により公教育の質の抜本的改善をしてほしい。'
 '資産を持たない人でも24時間いつでも腰を落ち着けて物事を考えることができる環境が必要だと思う。' nan
```


NaNが入ってる


py

```
def generate_label(question, args_sample, args_sample_outside, prompt, model):
    llm = ChatOpenAI(model_name=model, temperature=0.0)
    # remove NaNs from args_sample
    args_sample_outside = [arg for arg in args_sample_outside if isinstance(arg, str)]
    args_sample = [arg for arg in args_sample if isinstance(arg, str)]
```


この修正を入れてもvisualizationで死ぬ


argsにnanが入っている
![image](https://gyazo.com/f5fb29471b5a877807cdd8a71a554b24/thumb/1000)

![image](https://gyazo.com/c806a3ffd527d7ca2ab517f597c49338/thumb/1000)

手動で削った
- 出力するスクリプトがfilterすべきだ
