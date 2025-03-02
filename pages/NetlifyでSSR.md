---
title: "NetlifyでSSR"
---

[[SSR]]: [[Server Side Rendering]]
- [How to Build a Serverless, SEO-friendly React blog | Netlify](https://www.netlify.com/blog/2017/09/26/how-to-build-a-serverless-seo-friendly-react-blog/)
    - > [[Prerendering]]
    - >  Our blog is set up, but crawlers from search engines and social networks don’t always execute JavaScript so our blog has terrible SEO.
    - >  There are a number of ways to address this, including setting up server-side rendering and pre-rendering services like Prerender.io. But these options all require setting up and maintaining a Node.js server. Luckly, Netlify offers built-in prerendering which allows us to keep our code “serverless” while still making sure our blog is optimized for crawlers.
- [Prerendering | Netlify Docs](https://docs.netlify.com/site-deploys/post-processing/prerendering/)
    - > When detecting a single page app their crawler will send an _escaped_fragment_ query parameter in the request, and the origin server can then choose to return a document that represents the content a user will actually get when the single page app is running.