---
title: "pandoc"
---

`$ brew install pandoc`

py

```
ast = json.loads(pypandoc.convert_file("2-0-....md", "json"))
```


py

```
In [18]: ast['blocks'][0]
Out[18]: 
{'t': 'Header',
 'c': [1,
  ['information-technology-and-democracy-a-widening-gulf', [], []],
  [{'t': 'Str', 'c': 'Information'},
   {'t': 'Space'},
   {'t': 'Str', 'c': 'Technology'}, ...
```


py

```
In [19]: ast['blocks'][1]
Out[19]: 
{'t': 'BlockQuote',
 'c': [{'t': 'Para',
   'c': [{'t': 'Quoted',
     'c': [{'t': 'DoubleQuote'},
      [{'t': 'Str', 'c': 'Surveillance'},
       {'t': 'Space'},
       {'t': 'Str', 'c': 'capitalism'}, ...
```


[Pandoc - Pandoc filters](https://pandoc.org/filters.html)
![image](https://gyazo.com/e26fb1a2df3aa918e541764034223da9/thumb/1000)

