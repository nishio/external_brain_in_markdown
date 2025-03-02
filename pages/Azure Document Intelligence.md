---
title: "Azure Document Intelligence"
---

> [hiro_gamo](https://x.com/hiro_gamo/status/1799104021703405829) 一日一善ということで…、今日はRAGのドキュメントからの情報抽出でよく使われてる地味なサービスの紹介。Azure Document Intelligence。
>
>  Azure Document Intelligence(以下ADI)はPDFのOCRやレイアウト抽出ができるAPIサービスで、LLMのRAGの文脈で発展を続けてます。
>
>  基本的な機能はPDFや画像などのファイルから
>  ・文字
>  ・表の構造と内部テキスト
>  ・図の位置情報
>  これらをJSONもしくはマークダウンで出力が可能です。
>
>  マークダウンの出力時には単純なテキスト抽出ではなく、章立てなども配慮して抽出できます。
>
>  GPTはじめLLMはマークダウン形式の読み取りは比較的強く、章立ての作りによって解釈性が変わることもあるので、RAGのドキュメントからの情報抽出においては有効な手段になります。
>
>  実はGPT-4oなどのVLMでも同様なことが出来たりしますが、プロンプティングや、出力形式の固定化の手間が無く、ファインチューニングにも対応しているため相変わらず需要が高いサービスです。
>
>  よくRAGのための情報抽出で実施するのが下記です。
>  1. ADIでレイアウト分析しマークダウン化
>  2. 図の位置情報から図だけCrop
>  3. 図をGPT-4Vに渡し、読み取れる情報を抽出
>  4. 3.で得た情報をマークダウンに戻す
>  このテキスト情報を出発点としてチャンクなどの処理に入ります。
>
>  マークダウン化されているとその後の加工(GPT4にダイナミックなチャンクをさせたり、FAQ化するなど)が楽になるので、使ってみてください。
>
>  リソースさえ建てればGUIからお試しも可能です。
>
>  [https://learn.microsoft.com/ja-jp/azure/ai-services/document-intelligence/concept-layout?view=doc-intel-4.0.0&viewFallbackFrom=form-recog-3.0.0&tabs=sample-code…](https://learn.microsoft.com/ja-jp/azure/ai-services/document-intelligence/concept-layout?view=doc-intel-4.0.0&viewFallbackFrom=form-recog-3.0.0&tabs=sample-code…)
>  ![image](https://pbs.twimg.com/media/GPerwIEbEAAmI9O?format=png&name=medium#.png) ![image](https://pbs.twimg.com/media/GPeuFiQaoAAZioi?format=jpg&name=large#.png)

