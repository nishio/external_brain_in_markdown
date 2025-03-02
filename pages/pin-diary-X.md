---
title: "pin-diary-X"
---

[[井戸端]]で使われている日記ページ作成システムを自分のプロジェクトにも導入した。

導入メモ
- 2022-05-21現在の最新のコード
    - [/villagepump/pin-diary-6](https://scrapbox.io/villagepump/pin-diary-6)
- これはTypeScriptで書かれていることと、複数のファイルに分かれて、サードパーティのライブラリも使っていることから、事前にバンドルする必要がある
    - バンドルしたものは例えばこのようになる
        - [/takker/pin-diary-6-min](https://scrapbox.io/takker/pin-diary-6-min)
        - このスクリプトが「日記ページを追加したいプロジェクトX」から呼び出される仕組み
            - Xのユーザページでインポートして使っている
            - ([/takker/import#619379b61280f0000031837c](https://scrapbox.io/takker/import#619379b61280f0000031837c)を経由している)
- 日記ページのデザインやタイトルは関数に切り出されているから変えたければこれを変えればいい
    - [/villagepump/pin-diary-6/template](https://scrapbox.io/villagepump/pin-diary-6/template)
- 必要なファイルはすべてこのページに転記した
    - 自分向けに変更するscript.tsとtemplate.ts以外は井戸端に置いたままプロジェクトを跨いだURL importをする手もある
    - 全体像がわからないまま使うのが気持ち悪かったので全部集めただけ
- バンドルにはこれを使う
    - [/villagepump/scrapbox-bundler](https://scrapbox.io/villagepump/scrapbox-bundler)
    - `deno bundle <url> | esbuild --minify`をしているだけなので手元に開発環境があるならそれで良い
    - このビルド結果がCDNに入って明示的リフレッシュしない限り10年キャッシュされるとかではないので、今はできたスクリプトを手作業でScrapboxに貼ってる
        - ちょっとめんどくさいけど、この作業を今後たくさんやる予定はないので自動化しようという気持ちにはなってない
    - このURLにアクセスするとビルドが走る
        - [https://scrapbox-bundler.vercel.app/?url=https://scrapbox.io/api/code/nishio/pin-diary-X/script.ts&bundle&minify&run&output=newtab&reload](https://scrapbox-bundler.vercel.app/?url=https://scrapbox.io/api/code/nishio/pin-diary-X/script.ts&bundle&minify&run&output=newtab&reload)
        - 実際にやってみると一部のファイルがないとエラーが出て、pin-diary-5からいくつかの関数をインポートすることが必要だった
    - 出来上がったものをこのページの末尾にmin.jsという名前で置いた、これを自分のUserScriptから呼び出して使う
- [/villagepump/なぜかpin-diaryでunpinされない](https://scrapbox.io/villagepump/なぜかpin-diaryでunpinされない)
    - タイトルのフォーマットを変えた場合、タイトルのフォーマットを判定する正規表現も合わせて変える必要がある
- deps.tsの意味
    - [/deno-ja/deps.tsでモジュールを管理する#5fb4f9c21a00a2000055ba](https://scrapbox.io/deno-ja/deps.tsでモジュールを管理する#5fb4f9c21a00a2000055ba)
- 2022-05-30
    - 未踏ジュニアのScrapboxに作業室テンプレートでページを作成するようにした
    - その後「ピン留めしないようにしたい」という本体部分に手を加えるニーズが出てきたのでこのページではなく[/mitoujr-script/times-dev](https://scrapbox.io/mitoujr-script/times-dev)に移した

script.ts

```typescript
import { launch } from "./mod.ts";
import {
  makeDiary, filter,
} from "./template.ts";

launch(
  "nishio",
  {
    makeDiary,
    filter,
  },
);
```


template.ts

```typescript
import {
  getDay,
  getWeek,
  addDays,
  subDays,
  subYears,
  getYear,
  lightFormat,
  getDayOfYear,
  getDaysInYear,
} from "./template_deps.ts";

const titleFormat = "日記yyyy-MM-dd";
const titleRegExp = /^日記\d{4}-\d{2}-\d{2}$/;

export function makeDiary(date: Date): {
  title: string;
  header: string[];
  footer: string[];
} {
  return {
    title: toTitle(date),
    header: [],
    footer: [
      `[${lightFormat(subDays(date, 1), titleFormat)}]←${lightFormat(
        date,
        titleFormat
      )}→[${lightFormat(addDays(date, 1), titleFormat)}]`,
      `100日前 [${lightFormat(subDays(date, 100), titleFormat)}]`,
      `1年前 [${lightFormat(subYears(date, 1), titleFormat)}]`,
    ],
  };
}

function youbiLine(date: Date): string {
  const day = getDay(date);
  return [..."日月火水木金土"]
    .map((char, i) => (i === day ? `[[${char}]]` : char))
    .join("");
}

export function filter(title: string, today: Date): boolean {
  if (!titleRegExp.test(title)) return true;
  return toTitle(today) === title;
}

function toTitle(date: Date): string {
  return lightFormat(date, titleFormat);
}
```


template_deps.ts

```typescript
// 一年の経過率を計算するのに必要
 export { default as getDaysInYear } from "https://deno.land/x/date_fns@v2.22.1/getDaysInYear/index.ts";
 export { default as getDayOfYear } from "https://deno.land/x/date_fns@v2.22.1/getDayOfYear/index.ts";
 // 日付計算に使う
 export { default as addDays } from "https://deno.land/x/date_fns@v2.22.1/addDays/index.ts";
 export { default as subDays } from "https://deno.land/x/date_fns@v2.22.1/subDays/index.ts";
 export { default as getWeek } from "https://deno.land/x/date_fns@v2.22.1/getWeek/index.ts";
 export { default as subYears } from "https://deno.land/x/date_fns@v2.22.1/subYears/index.ts";
 export { default as getDay } from "https://deno.land/x/date_fns@v2.22.1/getDay/index.ts";
 export { default as getYear } from "https://deno.land/x/date_fns@v2.22.1/getYear/index.ts";
 // 文字列変換に使う
 export { default as lightFormat } from "https://deno.land/x/date_fns@v2.22.1/lightFormat/index.ts";
```


mod.ts

```typescript
/// <reference no-default-lib="true"/>
/// <reference lib="esnext"/>
/// <reference lib="dom"/>
import {
  pin,
  unpin,
  patch,
  useStatusBar,
  sleep,
  makeSocket,
  disconnect,
  format,
} from "./deps.ts";
import { listPinnedPages } from "./list.ts";
import type { Scrapbox, Socket } from "./deps.ts";
declare const scrapbox: Scrapbox;

export interface DiaryInit {
  makeDiary: (date: Date) => {
    title: string;
    header: string[];
    footer: string[];
  },
  filter: (title: string, today: Date) => boolean;
}

// initialize
export function launch(
  project: string,
  init: DiaryInit & { interval?: number },
) {
  const interval = init.interval ?? 24 * 3600 * 1000;
  
  const handleChange = () =>
    scrapbox.Project.name === project ?
      startObserve(project, interval, init) :
      endObserve();
  handleChange();
  scrapbox.addListener("project:changed", handleChange);
}

let updateTimer: number | undefined;
async function startObserve(
  project: string,
  interval: number,
  init: DiaryInit,
) {
  endObserve();
  await pinDiary(project, new Date(), init);
  updateTimer = setInterval(
    () => pinDiary(project, new Date(), init),
    interval,
  );
}
function endObserve() {
  clearInterval(updateTimer);
}

export async function pinDiary(
  project: string,
  date: Date,
  { makeDiary, filter, }: DiaryInit,
): Promise<void> {
  const { render, dispose } = useStatusBar();
  let socket: Socket | undefined;
  try {
    // 今日以外の日付ページを外す
    render(
      { type: "spinner" },
      { type: "text", text: `unpin other diary pages...`},
    );
    socket = await makeSocket();
    for await (const { title } of listPinnedPages(project)) {
      if (filter(title, date)) continue;
      await unpin(project, title, { socket });
    }
    
    // 今日の日付ページをピン留めする
    const { title, header, footer } = makeDiary(date);
    render(
      { type: "spinner" },
      { type: "text", text: `pin "/${project}/${title}"...`},
    );
    await pin(project, title, { socket, create: true });
    
    // 今日の日付ページにtemplateを挿入する
    render(
      { type: "spinner" },
      { type: "text", text: `format "/${project}/${title}"...`},
    );
    await patch(project, title, (lines) => [
      lines[0].text,
      ...format(
        lines.slice(1).map(line => line.text),
        header,
        footer,
      ),
    ], { socket });
    
    render(
      { type: "check-circle" },
      { type: "text", text: `Pinned "/${project}/${title}".`},
    );
  } catch(e: unknown) {
    render(
      { type: "exclamation-triangle" },
      { type: "text", text: e instanceof Error ?
        `${e.name} ${e.message}` :
        `Unknown error! (see developper console)`,
      },
    );
    console.error(e);
  } finally {
    if (socket) await disconnect(socket);
    await sleep(1000);
    dispose();
  }
}

```


list.ts

```typescript
import { listPages, PageSummary } from "./deps.ts";

/** 全てのピン留めされたページを取得する */
export async function* listPinnedPages(project: string, skip = 0): AsyncGenerator<PageSummary> {
  const { count, pages } = await ensureList(project, skip);
  for (const page of pages) {
    if (page.pin === 0) continue;
    yield page;
  }
  // pinしたページこれ以上ないときは終了
  if ((pages.at(-1)?.pin ?? 0) === 0) return;
  yield* listPinnedPages(project, skip + 1000);
}

async function ensureList(project: string, skip: number) {
  const result = await listPages(project, {
    limit: 1000,
    skip,
  });
  // login errorなどは全部例外として扱う
  if (!result.ok) {
    const error = new Error();
    error.name = result.value.name;
    error.message = result.value.message;
    throw error;
  }
  
  return result.value;
}

```


deps.ts

```typescript
export { patchTemplate as format } from "./format.ts";
export {
  pin,
  unpin,
  patch,
  useStatusBar,
  makeSocket,
  disconnect,
  listPages,
} from "https://raw.githubusercontent.com/takker99/scrapbox-userscript-std/0.10.3/mod.ts";
export type {
  Socket,
} from "https://raw.githubusercontent.com/takker99/scrapbox-userscript-std/0.10.3/mod.ts";
export {
  sleep,
} from "https://raw.githubusercontent.com/takker99/scrapbox-userscript-std/0.10.3/sleep.ts";
export type {
  Scrapbox,
  PageSummary,
} from "https://raw.githubusercontent.com/scrapbox-jp/types/0.0.8/mod.ts";

```


[https://scrapbox.io/api/code/villagepump/pin-diary-5/format.ts](https://scrapbox.io/api/code/villagepump/pin-diary-5/format.ts)
format.ts

```typescript
import { patchLines, findSplitIndex } from "./util.ts";

// linesにタイトルを入れないように
export function patchTemplate(lines: string[], headers: string[], footers: string[]): string[] {
  // headerとfooterに相当する行を補う
  const bodies = patchLines(
    patchLines(lines, headers).reverse(),
    [...footers].reverse(),
  ).reverse();
  
  // headerとfooterの間に余裕をもたせる
  const headerStart = findSplitIndex(bodies, headers);
  const footerStart = bodies.length - 1 - findSplitIndex(
    [...bodies].reverse(),
    [...footers].reverse(),
  );
  return [
    ...bodies.slice(0, headerStart + 1),
    "",
    ...bodies.slice(headerStart + 1, footerStart).join("\n").trim().split("\n"),
    "",
    ...bodies.slice(footerStart),
  ];
}
```


[https://scrapbox.io/api/code/villagepump/pin-diary-5/util.ts](https://scrapbox.io/api/code/villagepump/pin-diary-5/util.ts)
util.ts

```typescript
export function patchLines(lines: string[], appends: string[]) {
  let index = 0;
  const result = [] as string[];
  for (let i = 0; i < appends.length; i++) {
    const pos = lines.findIndex((line, j) => j >= index && line.trim() === appends[i].trim());
    if (pos < 0) {
      result.push(appends[i]);
      continue;
    }
    result.push(...lines.slice(index, pos + 1));
    index = pos + 1;
  }
  result.push(...lines.slice(index));
  return result;
}

export function findSplitIndex(lines: string[], query: string[]) {
  let index = -1;
  for (const text of query) {
    const pos = lines.findIndex((line, j) => j > index && line.trim() === text.trim());
    if (pos < 0) return -1;
    index = pos;
  }
  return index;
}
```


min.js

```javascript
function X(e,t){let r=0,n=[];for(let o=0;o<t.length;o++){let s=e.findIndex((a,i)=>i>=r&&a.trim()===t[o].trim());if(s<0){n.push(t[o]);continue}n.push(...e.slice(r,s+1)),r=s+1}return n.push(...e.slice(r)),n}function G(e,t){let r=-1;for(let n of t){let o=e.findIndex((s,a)=>a>r&&s.trim()===n.trim());if(o<0)return-1;r=o}return r}function V(e,t,r){let n=X(X(e,t).reverse(),[...r].reverse()).reverse(),o=G(n,t),s=n.length-1-G([...n].reverse(),[...r].reverse());return[...n.slice(0,o+1),"",...n.slice(o+1,s).join(`
`).trim().split(`
`),"",...n.slice(s)]}async function J(e){let t="https://scrapbox.io/api/users/me",r=await fetch(t,e?.sid?{headers:{Cookie:I(e.sid)}}:void 0);if(!r.ok)throw L("UnexpectedError",`Unexpected error has occuerd when fetching "${t}"`);return await r.json()}var I=e=>`connect.sid=${e}`;function Ye(e){return e!=null}function qe(e){return Ye(e)?(e.name===void 0||typeof e.name=="string")&&typeof e.message=="string":!1}function S(e){try{let t=typeof e=="string"?JSON.parse(e):e;return qe(t)?t:!1}catch(t){if(t instanceof SyntaxError)return!1;throw t}}function L(e,t){let r=new Error;return r.name=e,r.message=t,r}var U=e=>e.replaceAll(" ","_").toLowerCase();var Z=e=>[...e].map((t,r)=>t===" "?"_":!Be.includes(t)||r===e.length-1&&Ke.includes(t)?encodeURIComponent(t):t).join(""),Be='@$&+=:;",',Ke=':;",';async function le(e,t,r){let n=`https://scrapbox.io/api/pages/${e}/${Z(t)}?followRename=${r?.followRename??!0}`,o=await fetch(n,r?.sid?{headers:{Cookie:I(r.sid)}}:void 0);if(!o.ok){let a=S(await o.text());if(!a)throw L("UnexpectedError",`Unexpected error has occuerd when fetching "${n}"`);return{ok:!1,value:a}}let s=await o.json();return{ok:!0,value:s}}async function ee(e,t){let{sort:r,limit:n,skip:o}=t??{},s=new URLSearchParams;r!==void 0&&s.append("sort",r),n!==void 0&&s.append("limit",`${n}`),o!==void 0&&s.append("skip",`${o}`);let a=`https://scrapbox.io/api/pages/${e}?${s.toString()}`,i=await fetch(a,t?.sid?{headers:{Cookie:I(t.sid)}}:void 0);if(!i.ok){let d=S(await i.text());if(!d)throw L("UnexpectedError",`Unexpected error has occuerd when fetching "${a}"`);return{ok:!1,value:d}}let c=await i.json();return{ok:!0,value:c}}async function me(e,t){let r=`https://scrapbox.io/api/projects/${e}`,n=await fetch(r,t?.sid?{headers:{Cookie:I(t.sid)}}:void 0);if(!n.ok){let s=S(await n.json());if(!s)throw L("UnexpectedError",`Unexpected error has occuerd when fetching "${r}"`);return{ok:!1,value:s}}let o=await n.json();return{ok:!0,value:o}}var fe=(e,t)=>{if(!(e instanceof HTMLDivElement))throw new TypeError(`"${t}" must be HTMLDivElememt but actual is "${e}"`)};var ge=()=>Qe(document.getElementsByClassName("status-bar")?.[0],"div.status-bar"),Qe=(e,t)=>{if(!!e)return fe(e,t),e};var F=e=>new Promise(t=>setTimeout(()=>t(),e));function te(){let e=ge();if(!e)throw new Error("div.status-bar can't be found");let t=document.createElement("div");return e.append(t),{render:(...r)=>{t.textContent="";let n=ye(...r);n&&t.append(n)},dispose:()=>t.remove()}}function ye(...e){let t=e.flatMap(n=>{switch(n.type){case"spinner":return[Ze()];case"check-circle":return[et()];case"exclamation-triangle":return[tt()];case"text":return[q(n.text)];case"group":{let o=ye(...n.items);return o?[o]:[]}}});if(t.length===0)return;if(t.length===1)return t[0];let r=document.createElement("span");return r.classList.add("item-group"),r.append(...t),r}function q(e){let t=document.createElement("span");return t.classList.add("item"),t.append(e),t}function Ze(){let e=document.createElement("i");return e.classList.add("fa","fa-spinner"),q(e)}function et(){let e=document.createElement("i");return e.classList.add("kamon","kamon-check-circle"),q(e)}function tt(){let e=document.createElement("i");return e.classList.add("fas","fa-exclamation-triangle"),q(e)}var rt="4.2.0";async function D(){let t=(await nt())("https://scrapbox.io",{reconnectionDelay:5e3,transports:["websocket"]});return await new Promise((r,n)=>{let o=s=>n(s);t.once("connect",()=>{t.off("disconnect",o),r()}),t.once("disconnect",o)}),t}function nt(){let e=`https://cdnjs.cloudflare.com/ajax/libs/socket.io/${rt}/socket.io.min.js`;if(document.querySelector(`script[src="${e}"]`))return Promise.resolve(window.io);let t=document.createElement("script");return t.src=e,new Promise((r,n)=>{t.onload=()=>r(window.io),t.onerror=o=>n(o),document.head.append(t)})}function N(e,t=9e4){function r(o,s){let a;return new Promise((i,c)=>{let d=u=>{clearTimeout(a),c(new Error(u))};e.emit(o,s,u=>{clearTimeout(a),e.off("disconnect",d),u.error&&c(new Error(JSON.stringify(u.error))),"data"in u?i(u?.data):i(void 0)}),a=setTimeout(()=>{e.off("disconnect",d),c(new Error(`Timeout: exceeded ${t}ms`))},t),e.once("disconnect",d)})}async function*n(...o){let s,a=()=>new Promise(c=>s=c),i=c=>{s?.(c)};for(let c of o)e.on(c,i);try{for(;;)yield await a()}finally{for(let c of o)e.off(c,i)}}return{request:r,response:n}}function re(){return D()}async function P(e){if(e.connected)return;let t=new Promise(r=>e.once("connect",()=>r()));e.connect(),await t}async function v(e){if(e.disconnected)return;let t=new Promise(r=>{let n=o=>{o==="io client disconnect"&&(r(),e.off("disconnect",n))};e.on("disconnect",n)});e.disconnect(),await t}var B;async function _(){if(B!==void 0)return B;let e=await J();if(e.isGuest)throw new Error("this script can only be executed by Logged in users");return B=e.id,B}var be=new Map;async function A(e){let t=be.get(e);if(t!==void 0)return t;let r=await me(e);if(!r.ok){let{name:o,message:s}=r.value;throw new Error(`${o} ${s}`)}let{id:n}=r.value;return be.set(e,n),n}function we(e){return e.padStart(8,"0")}function ke(e){let t=Math.floor(new Date().getTime()/1e3).toString(16),r=Math.floor(16777214*Math.random()).toString(16);return`${we(t).slice(-8)}${e.slice(-6)}0000${we(r)}`}function Ee(e,t){let r=e.length>t.length,n=r?t:e,o=r?e:t,s=n.length+1,a=n.length+o.length+3,i=new Array(a);i.fill(-1);let c=[];function d(l,w,O){let E=Math.max(w,O),Y=E-l;for(;Y<n.length&&E<o.length&&n[Y]===o[E];)++Y,++E;return i[l+s]=c.length,c.push([{x:Y,y:E},i[l+(w>O?-1:1)+s]]),E}let u=new Array(a);u.fill(-1);let y=-1,f=o.length-n.length;do{++y;for(let l=-y;l<=f-1;++l)u[l+s]=d(l,u[l-1+s]+1,u[l+1+s]);for(let l=f+y;l>=f+1;--l)u[l+s]=d(l,u[l-1+s]+1,u[l+1+s]);u[f+s]=d(f,u[f-1+s]+1,u[f+1+s])}while(u[f+s]!==o.length);let k=[],b=i[f+s];for(;b!==-1;)k.push(c[b][0]),b=c[b][1];return{from:e,to:t,editDistance:f+y*2,buildSES:function*(){let l=0,w=0;for(let{x:O,y:E}of ot(k))for(;l<O||w<E;)E-O>w-l?(yield{value:o[w],type:r?"deleted":"added"},++w):E-O<w-l?(yield{value:n[l],type:r?"added":"deleted"},++l):(yield{value:n[l],type:"common"},++l,++w)}}}function*De(e){let t=[],r=[];function*n(){if(t.length>r.length){for(let o=0;o<r.length;o++)yield ve(t[o],r[o]);for(let o=r.length;o<t.length;o++)yield t[o]}else{for(let o=0;o<t.length;o++)yield ve(t[o],r[o]);for(let o=t.length;o<r.length;o++)yield r[o]}t=[],r=[]}for(let o of e)switch(o.type){case"added":t.push(o);break;case"deleted":r.push(o);break;case"common":yield*n(),yield o;break}yield*n()}function ve(e,t){return{value:e.value,oldValue:t.value,type:"replaced"}}function*ot(e){for(let t=e.length-1;t>=0;t--)yield e[t]}function*Te(e,t,{userId:r}){let{buildSES:n}=Ee(e.map(({text:a})=>a),t),o=0,s=e[0].id;for(let a of De(n())){switch(a.type){case"added":yield{_insert:s,lines:{id:ke(r),text:a.value}};continue;case"deleted":yield{_delete:s,lines:-1};break;case"replaced":yield{_update:s,lines:{text:a.value}};break}o++,s=e[o]?.id??"_end"}}var st=e=>({type:"title",text:e.rows[0].text}),it=e=>{let{rows:[t,...r]}=e,{indent:n=0,text:o=""}=t??{},s=o.replace(/^\s*code:/,"");return{indent:n,type:"codeBlock",fileName:s,content:r.map(a=>a.text.substring(n+1)).join(`
`)}},x=(e,{parseOnNested:t,parseOnQuoted:r,patterns:n})=>(o,s,a)=>{var i,c,d,u,y,f;if(!t&&s.nested)return(i=a?.())!==null&&i!==void 0?i:[];if(!r&&s.quoted)return(c=a?.())!==null&&c!==void 0?c:[];for(let k of n){let b=k.exec(o);if(b===null)continue;let l=o.substring(0,b.index),w=o.substring(b.index+((u=(d=b[0])===null||d===void 0?void 0:d.length)!==null&&u!==void 0?u:0)),O=e((y=b[0])!==null&&y!==void 0?y:"",s);return[...H(l,s),...O,...H(w,s)]}return(f=a?.())!==null&&f!==void 0?f:[]},h=e=>[{type:"plain",raw:e,text:e}],at=x(h,{parseOnNested:!0,parseOnQuoted:!0,patterns:[/^()(.*)()$/]}),ct=/^>.*$/,ut=(e,t)=>t.context==="table"?h(e,t):[{type:"quote",raw:e,nodes:H(e.substring(1),{...t,quoted:!0})}],dt=x(ut,{parseOnNested:!1,parseOnQuoted:!1,patterns:[ct]}),pt=/^\? .+$/,lt=(e,t)=>t.context==="table"?h(e,t):[{type:"helpfeel",raw:e,text:e.substring(2)}],mt=x(lt,{parseOnNested:!1,parseOnQuoted:!1,patterns:[pt]}),ft=/\[\[https?:\/\/[^\s\]]+\.(?:png|jpe?g|gif|svg)\]\]/i,gt=/\[\[https?:\/\/(?:[0-9a-z-]+\.)?gyazo\.com\/[0-9a-f]{32}\]\]/,xt=(e,t)=>{if(t.context==="table")return h(e,t);let r=e.substring(2,e.length-2),n=/^https?:\/\/([0-9a-z-]\.)?gyazo\.com\/[0-9a-f]{32}$/.test(r);return[{type:"strongImage",raw:e,src:n?`${r}/thumb/1000`:r}]},ht=x(xt,{parseOnNested:!1,parseOnQuoted:!0,patterns:[ft,gt]}),yt=/\[[^[\]]*\.icon(?:\*[1-9]\d*)?\]/;function Ie(e){return(t,r)=>{if(e==="strongIcon"&&r.context==="table")return h(t,r);let n=e==="icon"?t.substring(1,t.length-1):t.substring(2,t.length-2),o=n.lastIndexOf(".icon"),s=n.substring(0,o),a=s.startsWith("/")?"root":"relative",i=n.substring(o+5,n.length),c=i.startsWith("*")?parseInt(i.substring(1),10):1;return new Array(c).fill({}).map(()=>({path:s,pathType:a,type:e,raw:t}))}}var bt=Ie("icon"),wt=x(bt,{parseOnNested:!1,parseOnQuoted:!0,patterns:[yt]}),kt=/\[\[[^[\]]*\.icon(?:\*\d+)?\]\]/,Et=Ie("strongIcon"),Dt=x(Et,{parseOnNested:!1,parseOnQuoted:!0,patterns:[kt]}),vt=/\[\[(?:[^[]|\[[^[]).*?\]*\]\]/,Tt=(e,t)=>t.context==="table"?h(e,t):[{type:"strong",raw:e,nodes:H(e.substring(2,e.length-2),{...t,nested:!0})}],It=x(Tt,{parseOnNested:!1,parseOnQuoted:!0,patterns:[vt]}),Lt=/\[\$ .+? \]/,Mt=/\[\$ [^\]]+\]/,Ct=(e,t)=>t.context==="table"?h(e,t):[{type:"formula",raw:e,formula:e.substring(3,e.length-(e.endsWith(" ]")?2:1))}],Ot=x(Ct,{parseOnNested:!1,parseOnQuoted:!0,patterns:[Lt,Mt]}),Nt=/\[[!"#%&'()*+,\-./{|}<>_~]+ (?:\[[^[\]]+\]|[^\]])+\]/,St=(e,t)=>{if(t.context==="table")return h(e,t);let r=e.indexOf(" "),n=e.substring(1,r),o=e.substring(r+1,e.length-1),s=new Set(n);if(s.has("*")){let a=n.split("*").length-1;s.delete("*"),s.add(`*-${Math.min(a,10)}`)}return[{type:"decoration",raw:e,rawDecos:n,decos:Array.from(s),nodes:H(o,{...t,nested:!0})}]},Pt=x(St,{parseOnNested:!1,parseOnQuoted:!0,patterns:[Nt]}),At=/`.*?`/,Ht=(e,t)=>t.context==="table"?h(e,t):[{type:"code",raw:e,text:e.substring(1,e.length-1)}],Rt=x(Ht,{parseOnNested:!1,parseOnQuoted:!0,patterns:[At]}),_t=/^[$%] .+$/,jt=(e,t)=>{var r;if(t.context==="table")return h(e,t);let n=(r=e[0])!==null&&r!==void 0?r:"",o=e.substring(2);return[{type:"commandLine",raw:e,symbol:n,text:o}]},$t=x(jt,{parseOnNested:!1,parseOnQuoted:!1,patterns:[_t]}),Ut=/\[\s+\]/,Ft=(e,t)=>t.context==="table"?h(e,t):[{type:"blank",raw:e,text:e.substring(1,e.length-1)}],Wt=x(Ft,{parseOnNested:!1,parseOnQuoted:!0,patterns:[Ut]}),Yt=/\[https?:\/\/[^\s\]]+\.(?:png|jpe?g|gif|svg)(?:\?[^\]\s]+)?(?:\s+https?:\/\/[^\s\]]+)?\]/i,qt=/\[https?:\/\/[^\s\]]+\s+https?:\/\/[^\s\]]+\.(?:png|jpe?g|gif|svg)(?:\?[^\]\s]+)?\]/i,Bt=/\[https?:\/\/(?:[0-9a-z-]+\.)?gyazo\.com\/[0-9a-f]{32}(?:\/raw)?(?:\s+https?:\/\/[^\s\]]+)?\]/,Kt=/\[https?:\/\/[^\s\]]+\s+https?:\/\/(?:[0-9a-z-]+\.)?gyazo\.com\/[0-9a-f]{32}(?:\/raw)?\]/,zt=e=>/^https?:\/\/[^\s\]]+\.(png|jpe?g|gif|svg)(\?[^\]\s]+)?$/i.test(e)||Qt(e),Qt=e=>/^https?:\/\/([0-9a-z-]\.)?gyazo\.com\/[0-9a-f]{32}(\/raw)?$/.test(e),Xt=(e,t)=>{if(t.context==="table")return h(e,t);let r=e.search(/\s/),n=r!==-1?e.substring(1,r):e.substring(1,e.length-1),o=r!==-1?e.substring(r,e.length-1).trimLeft():"",[s,a]=zt(o)?[o,n]:[n,o];return[{type:"image",raw:e,src:/^https?:\/\/([0-9a-z-]\.)?gyazo\.com\/[0-9a-f]{32}$/.test(s)?`${s}/thumb/1000`:s,link:a}]},Gt=x(Xt,{parseOnNested:!0,parseOnQuoted:!0,patterns:[Yt,qt,Bt,Kt]}),Vt=/\[https?:\/\/[^\s\]]+\s+[^\]]*[^\s]\]/,Jt=/\[[^[\]]*[^\s]\s+https?:\/\/[^\s\]]+\]/,Zt=/\[https?:\/\/[^\s\]]+\]/,er=/https?:\/\/[^\s]+/,tr=(e,t)=>{if(t.context==="table")return h(e,t);let r=e.startsWith("[")&&e.endsWith("]")?e.substring(1,e.length-1):e,n=/^https?:\/\/[^\s\]]/.test(r),o=(n?/^https?:\/\/[^\s\]]+/:/https?:\/\/[^\s\]]+$/).exec(r);if(o?.[0]===void 0)return[];let s=n?r.substring(o[0].length):r.substring(0,o.index-1);return[{type:"link",raw:e,pathType:"absolute",href:o[0],content:s.trim()}]},rr=x(tr,{parseOnNested:!0,parseOnQuoted:!0,patterns:[Vt,Jt,Zt,er]}),Le=/\[([^\]]*[^\s])\s+([NS]\d+(?:\.\d+)?,[EW]\d+(?:\.\d+)?(?:,Z\d+)?)\]/,Me=/\[([NS]\d+(?:\.\d+)?,[EW]\d+(?:\.\d+)?(?:,Z\d+)?)(?:\s+([^\]]*[^\s]))?\]/,nr=e=>{let[t="",r="",n=""]=e.split(","),o=parseFloat(t.replace(/^N/,"").replace(/^S/,"-")),s=parseFloat(r.replace(/^E/,"").replace(/^W/,"-")),a=/^Z\d+$/.test(n)?parseInt(n.replace(/^Z/,""),10):14;return{latitude:o,longitude:s,zoom:a}},or=(e,t)=>{var r;if(t.context==="table")return h(e,t);let n=(r=e.match(Le))!==null&&r!==void 0?r:e.match(Me);if(n===null)return[];let o=e.startsWith("[N")||e.startsWith("[S"),[,s="",a=""]=o?n:[n[0],n[2],n[1]],{latitude:i,longitude:c,zoom:d}=nr(s),u=a!==""?`https://www.google.com/maps/place/${encodeURIComponent(a)}/@${i},${c},${d}z`:`https://www.google.com/maps/@${i},${c},${d}z`;return[{type:"googleMap",raw:e,latitude:i,longitude:c,zoom:d,place:a,url:u}]},sr=x(or,{parseOnNested:!1,parseOnQuoted:!0,patterns:[Le,Me]}),ir=/\[\/?[^[\]]+\]/,ar=e=>{let t=e.substring(1,e.length-1);return[{type:"link",raw:e,pathType:t.startsWith("/")?"root":"relative",href:t,content:""}]},cr=x(ar,{parseOnNested:!0,parseOnQuoted:!0,patterns:[ir]}),ur=/(?:^|\s)#\S+/,dr=(e,t)=>{if(t.context==="table")return h(e,t);if(e.startsWith("#"))return[{type:"hashTag",raw:e,href:e.substring(1)}];let r=e.substring(0,1),n=e.substring(1);return[...h(r,t),{type:"hashTag",raw:n,href:n.substring(1)}]},pr=x(dr,{parseOnNested:!0,parseOnQuoted:!0,patterns:[ur]}),lr=(e,t,r)=>{var n;return e===""?[]:(n=r?.())!==null&&n!==void 0?n:[]},mr=(...e)=>(t,r)=>e.reduceRight((n,o)=>()=>o(t,r,n),()=>at(t,r))(),H=mr(lr,dt,mt,Rt,$t,Ot,Wt,Pt,ht,Dt,It,Gt,rr,wt,sr,cr,pr),fr=e=>{let{rows:[t,...r]}=e,{indent:n=0,text:o=""}=t??{},s=o.replace(/^\s*table:/,"");return{indent:n,type:"table",fileName:s,cells:r.map(a=>a.text.substring(n+1)).map(a=>a.split("	").map(i=>H(i,{nested:!1,quoted:!1,context:"table"})))}},gr=e=>{let{indent:t,text:r}=e.rows[0];return{indent:t,type:"line",nodes:H(r.substring(t),{nested:!1,quoted:!1,context:"line"})}},Ce=e=>{switch(e.type){case"title":return st(e);case"codeBlock":return it(e);case"table":return fr(e);case"line":return gr(e)}},Oe=e=>e.split(`
`).map(t=>{var r,n,o;return{indent:(o=(n=(r=/^\s+/.exec(t))===null||r===void 0?void 0:r[0])===null||n===void 0?void 0:n.length)!==null&&o!==void 0?o:0,text:t}}),xr=(e,t)=>{var r,n;return(e.type==="codeBlock"||e.type==="table")&&t.indent>((n=(r=e.rows[0])===null||r===void 0?void 0:r.indent)!==null&&n!==void 0?n:0)},Ne=(e,t)=>{let r=e[e.length-1];return r!==void 0&&xr(r,t)?(r.rows.push(t),e):(e.push({type:/^\s*code:/.test(t.text)?"codeBlock":/^\s*table:/.test(t.text)?"table":"line",rows:[t]}),e)},Se=(e,t)=>{var r;if(!((r=t.hasTitle)!==null&&r!==void 0)||r){let[n,...o]=e;return n===void 0?[]:[{type:"title",rows:[n]},...o.reduce(Ne,[])]}return e.reduce(Ne,[])};function Pe(e,t,{userId:r,head:n}){let o=t.flatMap(u=>u.split(`
`)),s=[...Te(e,o,{userId:r})];(e[0].text!==o[0]||!n.persistent)&&s.push({title:o[0]});let a=e.slice(1,6).map(u=>u.text),i=o.slice(1,6);a.join("")!==i.join("")&&s.push({descriptions:i});let[c,d]=hr(o.join(`
`));return(n.links.length!==c.length||!n.links.every(u=>c.includes(u)))&&s.push({links:c}),n.image!==d&&s.push({image:d}),s}function hr(e){let t=Oe(e),r=Se(t,{hasTitle:!0}).flatMap(i=>{switch(i.type){case"codeBlock":case"title":return[];case"line":case"table":return[Ce(i)]}}),n=new Map,o=[],s=null,a=i=>{switch(i.type){case"hashTag":if(n.has(U(i.href)))return;n.set(U(i.href),!1),o.push(i.href);return;case"link":if(i.pathType!=="relative"||n.get(U(i.href)))return;n.set(U(i.href),!0),o.push(i.href);return;case"image":case"strongImage":{s??=i.src.endsWith("/thumb/1000")?i.src.replace(/\/thumb\/1000$/,"/raw"):i.src;return}case"strong":case"quote":case"decoration":{for(let c of i.nodes)a(c);return}default:return}};for(let i of yr(r))a(i);return[o,s]}function*yr(e){for(let t of e)switch(t.type){case"codeBlock":case"title":continue;case"line":for(let r of t.nodes)yield r;continue;case"table":{for(let r of t.cells)for(let n of r)for(let o of n)yield o;continue}}}async function M(e,t){let r=await le(e,t);if(!r.ok)throw new Error(`You have no privilege of editing "/${e}/${t}".`);let{commitId:n,persistent:o,image:s,links:a,lines:i,id:c,pin:d}=r.value;return{commitId:n,pageId:c,persistent:o,image:s,links:a,pin:d,lines:i}}async function K(e,t,r){return t.length===0?{commitId:r.parentId}:await e("socket.io-request",{method:"commit",data:{kind:"page",...r,changes:t,cursor:null,freeze:!0}})}async function R(e,t,{project:r,title:n,retry:o=3,parentId:s,...a}){try{s=(await K(e,t,{parentId:s,...a})).commitId}catch{console.log("Faild to push a commit. Retry after pulling new commits");for(let c=0;c<o;c++){let{commitId:d}=await M(r,n);s=d;try{s=(await K(e,t,{parentId:s,...a})).commitId,console.log("Success in retrying");break}catch{continue}}throw Error("Faild to retry pushing.")}return s}async function ne(e,t,r,n){let[o,s,a]=await Promise.all([M(e,t),A(e),_()]),i=o,c=n?.socket,d=c??await D();await P(d);try{let{request:u}=N(d);for(let y=0;y<3;y++)try{let f=r(i.lines,i),k=f instanceof Promise?await f:f;if(!k)return;k.length===0&&await R(u,[{deleted:!0}],{projectId:s,pageId:i.pageId,parentId:i.commitId,userId:a,project:e,title:t});let b=Pe(i.lines,k,{userId:a,head:i});await K(u,b,{parentId:i.commitId,projectId:s,pageId:i.pageId,userId:a});break}catch{if(y===2)throw Error("Faild to retry pushing.");console.log("Faild to push a commit. Retry after pulling new commits");try{i=await M(e,t)}catch(k){throw k}}}finally{c||await v(d)}}async function oe(e,t,r){let[n,o,s]=await Promise.all([M(e,t),A(e),_()]);if(n.pin>0||!n.persistent&&!(r?.create??!1))return;let a={parentId:n.commitId,projectId:o,pageId:n.pageId,userId:s,project:e,title:t},i=r?.socket,c=i??await D();await P(c);let{request:d}=N(c);if(!n.persistent){let u=await R(d,[{title:t}],a);a.parentId=u}try{await R(d,[{pin:br()}],a)}finally{i||await v(c)}}async function se(e,t,r){let[n,o,s]=await Promise.all([M(e,t),A(e),_()]);if(n.pin==0||!n.persistent)return;let a={parentId:n.commitId,projectId:o,pageId:n.pageId,userId:s,project:e,title:t},i=r?.socket,c=i??await D();await P(c);let{request:d}=N(c);try{await R(d,[{pin:0}],a)}finally{i||await v(c)}}var br=()=>Number.MAX_SAFE_INTEGER-Math.floor(Date.now()/1e3);async function*ie(e,t=0){let{count:r,pages:n}=await wr(e,t);for(let o of n)o.pin!==0&&(yield o);(n.at(-1)?.pin??0)!==0&&(yield*ie(e,t+1e3))}async function wr(e,t){let r=await ee(e,{limit:1e3,skip:t});if(!r.ok){let n=new Error;throw n.name=r.value.name,n.message=r.value.message,n}return r.value}function Ae(e,t){let r=t.interval??24*3600*1e3,n=()=>scrapbox.Project.name===e?kr(e,r,t):Re();n(),scrapbox.addListener("project:changed",n)}var He;async function kr(e,t,r){Re(),await _e(e,new Date,r),He=setInterval(()=>_e(e,new Date,r),t)}function Re(){clearInterval(He)}async function _e(e,t,{makeDiary:r,filter:n}){let{render:o,dispose:s}=te(),a;try{o({type:"spinner"},{type:"text",text:"unpin other diary pages..."}),a=await re();for await(let{title:u}of ie(e))n(u,t)||await se(e,u,{socket:a});let{title:i,header:c,footer:d}=r(t);o({type:"spinner"},{type:"text",text:`pin "/${e}/${i}"...`}),await oe(e,i,{socket:a,create:!0}),o({type:"spinner"},{type:"text",text:`format "/${e}/${i}"...`}),await ne(e,i,u=>[u[0].text,...V(u.slice(1).map(y=>y.text),c,d)],{socket:a}),o({type:"check-circle"},{type:"text",text:`Pinned "/${e}/${i}".`})}catch(i){o({type:"exclamation-triangle"},{type:"text",text:i instanceof Error?`${i.name} ${i.message}`:"Unknown error! (see developper console)"}),console.error(i)}finally{a&&await v(a),await F(1e3),s()}}function p(e,t){if(t.length<e)throw new TypeError(e+" argument"+(e>1?"s":"")+" required, but only "+t.length+" present")}function m(e){p(1,arguments);let t=Object.prototype.toString.call(e);return e instanceof Date||typeof e=="object"&&t==="[object Date]"?new Date(e.getTime()):typeof e=="number"||t==="[object Number]"?new Date(e):((typeof e=="string"||t==="[object String]")&&typeof console!="undefined"&&(console.warn("Starting with v2.0.0-beta.1 date-fns doesn't accept strings as date arguments. Please use `parseISO` to parse strings. See: https://git.io/fjule"),console.warn(new Error().stack)),new Date(NaN))}function z(e){let t=new Date(Date.UTC(e.getFullYear(),e.getMonth(),e.getDate(),e.getHours(),e.getMinutes(),e.getSeconds(),e.getMilliseconds()));return t.setUTCFullYear(e.getFullYear()),e.getTime()-t.getTime()}function g(e){if(e===null||e===!0||e===!1)return NaN;let t=Number(e);return isNaN(t)?t:t<0?Math.ceil(t):Math.floor(t)}function j(e,t){p(2,arguments);let r=m(e),n=g(t);return isNaN(n)?new Date(NaN):(n&&r.setDate(r.getDate()+n),r)}function W(e,t){p(2,arguments);let r=g(t);return j(e,-r)}function ae(e,t){p(2,arguments);let r=m(e),n=g(t);if(isNaN(n))return new Date(NaN);if(!n)return r;let o=r.getDate(),s=new Date(r.getTime());s.setMonth(r.getMonth()+n+1,0);let a=s.getDate();return o>=a?s:(r.setFullYear(s.getFullYear(),s.getMonth(),o),r)}function ce(e,t){p(2,arguments);let r=g(t);return ae(e,r*12)}function Q(e,t){p(2,arguments);let r=g(t);return ce(e,-r)}function T(e,t){for(var r=e<0?"-":"",n=Math.abs(e).toString();n.length<t;)n="0"+n;return r+n}var Er={y(e,t){let r=e.getUTCFullYear(),n=r>0?r:1-r;return T(t==="yy"?n%100:n,t.length)},M(e,t){let r=e.getUTCMonth();return t==="M"?String(r+1):T(r+1,2)},d(e,t){return T(e.getUTCDate(),t.length)},a(e,t){let r=e.getUTCHours()/12>=1?"pm":"am";switch(t){case"a":case"aa":return r.toUpperCase();case"aaa":return r;case"aaaaa":return r[0];case"aaaa":default:return r==="am"?"a.m.":"p.m."}},h(e,t){return T(e.getUTCHours()%12||12,t.length)},H(e,t){return T(e.getUTCHours(),t.length)},m(e,t){return T(e.getUTCMinutes(),t.length)},s(e,t){return T(e.getUTCSeconds(),t.length)},S(e,t){let r=t.length,n=e.getUTCMilliseconds(),o=Math.floor(n*Math.pow(10,r-3));return T(o,t.length)}},$e=Er;function ue(e){p(1,arguments);var t=m(e);return!isNaN(t)}function de(e,t){p(2,arguments);let r=m(e).getTime(),n=g(t);return new Date(r+n)}function pe(e,t){p(2,arguments);let r=g(t);return de(e,-r)}var Dr=/(\w)\1*|''|'(''|[^'])+('|$)|./g,vr=/^'([^]*?)'?$/,Tr=/''/g,Ir=/[a-zA-Z]/;function C(e,t){p(2,arguments);let r=m(e);if(!ue(r))throw new RangeError("Invalid time value");let n=z(r),o=pe(r,n),s=t.match(Dr);return s?s.map(i=>{if(i==="''")return"'";let c=i[0];if(c==="'")return Lr(i);let d=$e[c];if(d)return d(o,i);if(c.match(Ir))throw new RangeError("Format string contains an unescaped latin alphabet character `"+c+"`");return i}).join(""):""}function Lr(e){let t=e.match(vr);return t?t[1].replace(Tr,"'"):e}var $="日記yyyy-MM-dd",Cr=/^日記\d{4}-\d{2}-\d{2}$/;function Ue(e){return{title:We(e),header:[],footer:[`[${C(W(e,1),$)}]←${C(e,$)}→[${C(j(e,1),$)}]`,`100日前 [${C(W(e,100),$)}]`,`1年前 [${C(Q(e,1),$)}]`]}}function Fe(e,t){return Cr.test(e)?We(t)===e:!0}function We(e){return C(e,$)}Ae("nishio",{makeDiary:Ue,filter:Fe});
```

