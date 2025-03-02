---
title: "TTTC:error"
---

:

```
> next build

▲ Next.js 14.2.4

Linting and checking validity of types ...
Creating an optimized production build ...
✓ Compiled successfully
Collecting page data ...
Generating static pages (0/3) ...
✓ Generating static pages (3/3)
Errors:

Error occurred prerendering page "/". Read more: https://nextjs.org/docs/messages/prerender-error

SyntaxError: Unexpected token 'N', ..."rgument": NaN,
     "... is not valid JSON
    at JSON.parse (<anonymous>)
    at s (/Users/nishio/election2024_broadlistening/scatter/next-app/.next/server/pages/index.js:1:19050)
    at /Users/nishio/election2024_broadlistening/scatter/next-app/node_modules/next/dist/compiled/next-server/pages.runtime.prod.js:25:4024
    at /Users/nishio/election2024_broadlistening/scatter/next-app/node_modules/next/dist/server/lib/trace/tracer.js:140:36
    at NoopContextManager.with (/Users/nishio/election2024_broadlistening/scatter/next-app/node_modules/next/dist/compiled/@opentelemetry/api/index.js:1:7062)
    at ContextAPI.with (/Users/nishio/election2024_broadlistening/scatter/next-app/node_modules/next/dist/compiled/@opentelemetry/api/index.js:1:518)
    at NoopTracer.startActiveSpan (/Users/nishio/election2024_broadlistening/scatter/next-app/node_modules/next/dist/compiled/@opentelemetry/api/index.js:1:18093)
    at ProxyTracer.startActiveSpan (/Users/nishio/election2024_broadlistening/scatter/next-app/node_modules/next/dist/compiled/@opentelemetry/api/index.js:1:18854)
    at /Users/nishio/election2024_broadlistening/scatter/next-app/node_modules/next/dist/server/lib/trace/tracer.js:122:103
    at NoopContextManager.with (/Users/nishio/election2024_broadlistening/scatter/next-app/node_modules/next/dist/compiled/@opentelemetry/api/index.js:1:7062)

> Export encountered errors on following paths:
        /

Pipeline completed.
```

