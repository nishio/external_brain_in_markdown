
![image](https://gyazo.com/77ea598963604fa2b5e57c07581de594/thumb/1000)

Cache clear
- [https://cards-dev.twitter.com/validator](https://cards-dev.twitter.com/validator)

:

```
 const description = props.json.descriptions
   .map((line) => line.replace(/\[.*?\]/g, ""))
   .join(" ");

 return (
   <>
     <Head>
       <title>{title} - NISHIO Hirokazu</title>
       <meta name="twitter:card" content="summary_large_image" />
       <meta name="twitter:site" content="nishio" />
       <meta name="twitter:title" content={title} />
       <meta name="twitter:description" content={description} />
       <meta name="twitter:image" content={props.json.image} />
     </Head>
```

