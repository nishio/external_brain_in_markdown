---
title: "Nattoku in Vector space"
---

![image](https://gyazo.com/e5b07f1678a2b691aa89e3f8aa4baf74/thumb/1000)

> [nishio](https://twitter.com/nishio/status/1743099798537007291) #gleninjapan
>  In the lightning talk, I didn't delve into mathematical discussions due to limited time. For a more detailed explanation, I created diagrams by embedding the meanings of words into vector spaces using LLM.
>  ![image](https://pbs.twimg.com/media/GDC8BeGaEAAehIG?format=jpg&name=medium#.png)
- Lightning talk: [[Words as Public Goods]]

> [nishio](https://twitter.com/nishio/status/1743100780683706370) This is a two-dimensional visualization of the meanings of each word embedded in a high-dimensional space using OpenAI's text embedding API. In simple terms, it demonstrates how AI recognizes the similarity in meanings of words like this.
- [[Embedding API]]

> [nishio](https://twitter.com/nishio/status/1743102121317462148) Plotting two languages on a single chart is not a straightforward task. In this chart, the first principal component axis of PCA is treated as the axis representing the differences between languages and has been removed.

> [nishio](https://twitter.com/nishio/status/1743105040074895556/photo/1) Here is annotated version. The plotted words are a combination of those I have considered and those that GPT-4 has suggested as being similar. So it shows GPT4 can not find English words similar to Japanese Nattoku. Understanding and agreement is major explanation in dictionaries
>  ![image](https://pbs.twimg.com/media/GDDAKtyakAAbT68?format=jpg&name=medium#.png)

> [nishio](https://twitter.com/nishio/status/1743106756828680351) One word can bridge multiple concepts. In this example, the Japanese word "納得" (nattoku) serves as a bridge connecting concepts like "understanding", "agreement", and "satisfaction". Similarly, in Mandarin, "數位" (shùwèi) connects concepts like "digital" and "plural".

> [nishio](https://twitter.com/nishio/status/1743118818745131409) In the mapping from a high-dimensional space(H) to a low-dimensional space(L), objects that are close in H will generally remain close in L. However, there is no guarantee that objects far apart in H will also be far apart in L.
> [nishio](https://twitter.com/nishio/status/1743118975335358926) You can think of it like imagining the shadow of a three-dimensional object. Therefore, the absence of proximity in a low-dimensional space can be useful for understanding a high-dimensional space.




Making

![image](https://gyazo.com/f3290610ea13f77d41522219f97f553f/thumb/1000)
- Simple PCA generated this
    - it shows thr difference of languages

![image](https://gyazo.com/5e13f13280ccb8fc656d85026fd95008/thumb/1000)![image](https://gyazo.com/4505b5a3297c33f476a6969beabc02a7/thumb/1000)
- Visualization on each languages
- Those are good for observing each language only, but those should not be overlapped, by the nature of PCA.
- In the observation I found some candidate words are far from other words. Those outlier are ommitted from the visualization. We have only two~three dimensions to express information.
    - ![image](https://gyazo.com/f0a155a556427ce3e97fb147094a576a/thumb/1000)

>  In this chart, the first principal component axis of PCA is treated as the axis representing the differences between languages and has been removed.
- Finnaly got this
    - ![image](https://gyazo.com/f546d4ec99b272609d99dc4558dbd215/thumb/1000)
