---
title: "settings"
---

[/customize/Auto Dark Themes](https://scrapbox.io/customize/Auto Dark Themes)
style.css

```
@import url('./var.css') (prefers-color-scheme: dark);

:root {
	color-scheme: light dark;

	/* light */
	--body-bg: #88cc88;
	--card-bg: #eeffee;
	--card-title-bg: #eeffee;
}

body {
	background-color: var(--body-bg);
}
 
.grid li.two-two.page-list-item a .title {
	background-color: var(--card-title-bg);
}

.grid li.page-list-item a .content {
	background-color: var(--card-bg);
}
```



var.css

```
:root {
	--body-bg: #202228;
	--card-bg: #373b44;
	--card-title-bg: #2b2e38;
}
/* default-dark */
/* eksklusive hacker1 */
html[data-project-theme=default],
html[data-project-theme=default-minimal],
html[data-project-theme=blue],
html[data-project-theme=purple],
html[data-project-theme=green],
html[data-project-theme=orange],
html[data-project-theme=red],
html[data-project-theme=spring],
html[data-project-theme=summer],
html[data-project-theme=autumn],
html[data-project-theme=winter],
html[data-project-theme=tropical],
html[data-project-theme=kyoto],
html[data-project-theme=paris],
html[data-project-theme=mred] {
	--body-bg: #202228;
	--brand-icon-y-first-stop-opacity: 0.3;
	--brand-icon-y-last-stop-opacity: 0.6;
	--brand-icon-x-first-stop-opacity: 0.2;
	--brand-icon-x-last-stop-opacity: 0.3;
	--navbar-bg: rgba(55, 59, 68, 0.5);
	--navbar-title-color: #fff;
	--navbar-icon-color: #fff;
	--navbar-icon-active-color: #338c46;
	--navbar-icon-hovered-color: #338c46;
	--search-form-bg: rgba(255, 255, 255, 0.13);
	--search-form-icon-color: #fff;
	--search-form-icon-focus-color: #4a4a4a;
	--2hop-search-bg: rgba(255, 255, 255, 0.15);
	--card-title-color: #f0f0f0;
	--card-title-bg: #2b2e38;
	--card-bg: #373b44;
	--card-hover-bg: rgba(0, 0, 0, 0.1);
	--card-active-bg: rgba(229, 229, 229, 0.1);
	--card-backside: #545860;
	--card-description-color: #c4c4c4;
	--card-description-link-color: #80c9fe;
	--card-description-code-color: #ccc;
	--card-box-shadow-color: #000;
	--card-box-shadow: 0 2px 0 var(--card-box-shadow-color);
	--card-box-hover-shadow: 0 2px 0 rgba(0, 0, 0, 0.23);
	--card-title-bg-pinned: #2b2e38;
	--relation-label-bg: #2b2e38;
	--relation-label-text: #dddede;
	--relation-label-links-bg: #80c9fe;
	--relation-label-links-text: #202228;
	--relation-label-empty-bg: #fb7476;
	--relation-label-empty-text: #fff;
	--tool-color: #535863;
	--tool-light-color: #353b48;
	--tool-badge-bg: #2b2e38;
	--tool-bg: #2b2e38;
	--tool-text-color: #dddede;
	--new-button-vertical-color: #fff;
	--new-button-horizontal-color: #fff;
	--new-button-bg: hsl(227 51% 56% / 1);
	--new-button-hover-bg: hsl(227 51% 50% / 1);
	--new-button-active-bg: hsl(227 51% 45% / 1);
}
/* inkluzive hacker1 */
html[data-project-theme=default],
html[data-project-theme=default-minimal],
html[data-project-theme=blue],
html[data-project-theme=purple],
html[data-project-theme=green],
html[data-project-theme=orange],
html[data-project-theme=red],
html[data-project-theme=hacker1],
html[data-project-theme=spring],
html[data-project-theme=summer],
html[data-project-theme=autumn],
html[data-project-theme=winter],
html[data-project-theme=tropical],
html[data-project-theme=kyoto],
html[data-project-theme=paris],
html[data-project-theme=mred] {
	--telomere-border: #545863;
	--page-text-color: rgba(255, 255, 255, 0.87);
	--page-link-color: #80c9fe;
	--page-link-hover-color: #6a9ec6;
	--page-link-color-cursor-line: #a985e4;
	--page-bg: #373b44;
	--empty-page-link-color: #fb7476;
	--empty-page-link-hover-color: #b47576;
	--line-title-color: rgba(255, 255, 255, 0.87);
	--line-permalink-color: rgba(234, 218, 74, 0.35);
	--code-color: #ccc;
	--code-bg: rgba(0, 0, 0, 0.18);
	--quote-bg-color: rgba(0, 0, 0, 0.2);
	--page-image-loading-border-color: #555;
	--cursor-color: #fff;
	
	--hashtag-color: lime;
	--hashtag-hover-color: olive;
	--empty-hashtag-color: magenta;
	--empty-hashtag-hover-color: deeppink;
	
	& code.highlight {
		color: #ccc
	}
	& code.highlight .hljs {
		display: block;
		overflow-x: auto;
		padding: .5em;
		background: #fdf6e3;
		color: #657b83
	}
	& code.highlight .hljs-comment,
	& code.highlight .hljs-quote {
		color: #93a1a1
	}
	& code.highlight .hljs-keyword,
	& code.highlight .hljs-selector-tag,
	& code.highlight .hljs-addition {
		color: #859900
	}
	& code.highlight .hljs-number,
	& code.highlight .hljs-string,
	& code.highlight .hljs-meta .hljs-meta-string,
	& code.highlight .hljs-literal,
	& code.highlight .hljs-doctag,
	& code.highlight .hljs-regexp {
		color: #2aa198
	}
	& code.highlight .hljs-title,
	& code.highlight .hljs-section,
	& code.highlight .hljs-name,
	& code.highlight .hljs-selector-id,
	& code.highlight .hljs-selector-class {
		color: #268bd2
	}
	& code.highlight .hljs-attribute,
	& code.highlight .hljs-attr,
	& code.highlight .hljs-variable,
	& code.highlight .hljs-template-variable,
	& code.highlight .hljs-class .hljs-title,
	& code.highlight .hljs-type {
		color: #b58900
	}
	& code.highlight .hljs-symbol,
	& code.highlight .hljs-bullet,
	& code.highlight .hljs-subst,
	& code.highlight .hljs-meta,
	& code.highlight .hljs-meta .hljs-keyword,
	& code.highlight .hljs-selector-attr,
	& code.highlight .hljs-selector-pseudo,
	& code.highlight .hljs-link {
		color: #cb4b16
	}
	& code.highlight .hljs-built_in,
	& code.highlight .hljs-deletion {
		color: #dc322f
	}
	& code.highlight .hljs-strong {
		font-weight: bold
	}
}

/* paper-dark-dark */
html[data-project-theme=paper-light],
html[data-project-theme=newyork],
html[data-project-theme=lgreen] {
	--body-bg: #192f3d;
	--2hop-search-bg: rgba(255, 255, 255, 0.15);
	--card-title-bg: #294252;
	--card-title-color: rgba(255, 255, 255, 0.9);
	--card-bg: #395666;
	--card-hover-bg: rgba(0, 0, 0, 0.1);
	--card-active-bg: rgba(193, 203, 213, 0.1);
	--card-backside: #5c96b6;
	--card-description-color: rgba(255, 255, 255, 0.9);
	--card-description-link-color: #6bb8ed;
	--card-description-code-color: #ccc;
	--card-box-shadow-color: rgba(0, 0, 0, 0.2);
	--card-box-shadow: 0 2px 0 var(--card-box-shadow-color);
	--card-box-hover-shadow: 0 2px 0 var(--card-box-shadow-color);
	--card-title-bg-pinned: #294252;
	--relation-label-bg: #294252;
	--relation-label-text: #fff;
	--relation-label-links-bg: #5c96b6;
	--relation-label-links-text: #fff;
	--relation-label-empty-bg: #fb7476;
	--relation-label-empty-text: #fff;
	--tool-color: #578eac;
	--tool-light-color: #294252;
	--tool-badge-bg: #294252;
	--tool-bg: #294252;
	--tool-text-color: rgba(255, 255, 255, 0.87);
}
html[data-project-theme=paper-light],
html[data-project-theme=paper-dark],
html[data-project-theme=hacker2],
html[data-project-theme=newyork],
html[data-project-theme=lgreen] {
	--brand-icon-y-first-stop-opacity: 0.75;
	--brand-icon-x-first-stop-opacity: 0.4;
	--navbar-bg: hsl(203deg 38% 22% / 80%);
	--navbar-title-color: #fff;
	--navbar-icon-color: #5c96b6;
	--navbar-icon-active-color: #5c96b6;
	--navbar-icon-hovered-color: #8bc7e8;
	--search-form-bg: #395666;
	--search-form-icon-color: #fff;
	--search-form-icon-focus-color: #444;
	--new-button-vertical-color: #fff;
	--new-button-horizontal-color: #fff;
	--new-button-bg: #192f3d;
	--new-button-hover-bg: #466a7d;
	--new-button-active-bg: #395666;
	--telomere-border: #4a6e83;
	--telomere-unread: #86a8bb;
	--telomere-updated: #6bb8ed;
	--page-text-color: rgba(255, 255, 255, 0.95);
	--page-link-color: #68b3e5;
	--page-link-hover-color: #5c96b6;
	--page-link-color-cursor-line: #ae8de4;
	--page-bg: #395666;
	--empty-page-link-color: #fb7476;
	--empty-page-link-hover-color: #cf554d;
	--line-title-color: rgba(255, 255, 255, 0.95);
	--line-permalink-color: rgba(234, 218, 74, 0.35);
	--code-color: #ccc;
	--code-bg: rgba(0, 0, 0, 0.18);
	--page-image-loading-border-color: #888;
	--quote-bg-color: rgba(0, 0, 0, 0.2);
	--cursor-color: #fff;
	
	--hashtag-color: lime;
	--hashtag-hover-color: olive;
	--empty-hashtag-color: magenta;
	--empty-hashtag-hover-color: deeppink;
	
	& code.highlight {
		color: #ccc
	}
	& code.highlight .hljs {
		display: block;
		overflow-x: auto;
		padding: .5em;
		background: #fdf6e3;
		color: #657b83
	}
	& code.highlight .hljs-comment,
	& code.highlight .hljs-quote {
		color: #93a1a1
	}
	& code.highlight .hljs-keyword,
	& code.highlight .hljs-selector-tag,
	& code.highlight .hljs-addition {
		color: #859900
	}
	& code.highlight .hljs-number,
	& code.highlight .hljs-string,
	& code.highlight .hljs-meta .hljs-meta-string,
	& code.highlight .hljs-literal,
	& code.highlight .hljs-doctag,
	& code.highlight .hljs-regexp {
		color: #2aa198
	}
	& code.highlight .hljs-title,
	& code.highlight .hljs-section,
	& code.highlight .hljs-name,
	& code.highlight .hljs-selector-id,
	& code.highlight .hljs-selector-class {
		color: #268bd2
	}
	& code.highlight .hljs-attribute,
	& code.highlight .hljs-attr,
	& code.highlight .hljs-variable,
	& code.highlight .hljs-template-variable,
	& code.highlight .hljs-class .hljs-title,
	& code.highlight .hljs-type {
		color: #b58900
	}
	& code.highlight .hljs-symbol,
	& code.highlight .hljs-bullet,
	& code.highlight .hljs-subst,
	& code.highlight .hljs-meta,
	& code.highlight .hljs-meta .hljs-keyword,
	& code.highlight .hljs-selector-attr,
	& code.highlight .hljs-selector-pseudo,
	& code.highlight .hljs-link {
		color: #cb4b16
	}
	& code.highlight .hljs-built_in,
	& code.highlight .hljs-deletion {
		color: #dc322f
	}
	& code.highlight .hljs-strong {
		font-weight: bold
	}
}
```


imports
style.css_disabled

```
@import "https://scrapbox.io/api/code/nishio/%E3%82%A4%E3%83%B3%E3%83%87%E3%83%B3%E3%83%88%E8%A1%A8%E7%A4%BA/style.css";
```


2022-02-28
[[nishio]]と[[favicon]]をTopPageから消す
style.css

```
li.page-list-item.grid-style-item[data-page-title="favicon"],
li.page-list-item.grid-style-item[data-page-title="nishio"]
 {
  display: none;
}
```


2026-02-14 [/villagepump/曇りガラス記法](https://scrapbox.io/villagepump/曇りガラス記法)
style.css

```
.line:not(.cursor-line) .deco-\~:not(:hover) { filter: blur(5px); }
```


2022-02-26
[/blu3mo-public/関連ページ一覧を横に移動させる](https://scrapbox.io/blu3mo-public/関連ページ一覧を横に移動させる)
style.css_disabled

```
.col-page {
	max-width: 1200px;
}
 @media (min-width: 768px) {
 	.related-page-list {
 		flex-basis: 140px !important;
 	}
 }
 @media (min-width: 1240px) {
 	.related-page-list {
 		flex-basis: 285px !important;
 	}
		.related-page-list .relation-label {
  		width: 285px !important;
  	}
 }
 @media (min-width: 768px) {
   .page-wrapper {
     display: flex;
     justify-content: space-around;
   }
   .drag-and-drop-enter {
     order: 1;
     margin-right: 20px;
     flex-basis: 100% !important;
     min-width: 0;
   }
   .related-page-list {
     order: 2;
     flex-shrink: 0;
     margin-top: 0px;
     background-color: var(--related-page-list-bg);
   }
    .related-page-sort-menu {
    	display: none;
    }
   	.related-page-list .grid li {
   		margin-bottom: 5px !important;	
   		margin-right: 5px !important;	
   		width: 140px;
   	}
   	.related-page-list .grid .splitter {
   		height: 15px !important; 
   	}
   	.related-page-list .relation-label {
   		height: auto !important;
   	}
   	
   	.related-page-list .relation-label .arrow {
   		display: none !important;
   	}
   	
   	.related-page-list .relation-label a {
   		/* 関連リンク ラベル */
   		padding: 4px !important;
   		/* border-bottom: 2px solid var(--relation-label-bg); */
   	}
   	.related-page-list .relation-label .title{
    	font-size: 12px;
    }
   	.related-page-list .relation-label .icon-lg{
   		display: none !important;
   	}
   	.related-page-list .page-list-item {
    		/* カードサイズ変更 */
    		height: 50px !important;
    	}
    	.related-page-list .content {
    		/* カードサイズ変更 */
    		height: 100% !important;
     }
    	.related-page-list .page-list-item .header {
    		border-top-width: 5px !important;
    		padding-top: 3px !important;
    		padding-bottom: 3px !important;
    		z-index: 1;
    		/* background-color: var(--translucent-card-bg)*/
    	}
    	.related-page-list .page-list-item .header .title {
    		font-size: 12px !important;
    		filter: drop-shadow(0px 0px 6px var(--card-bg, #fff)) drop-shadow(0px 0px 8px var(--card-bg, #fff)) drop-shadow(0px 0px 10px var(--card-bg, #fff)) drop-shadow(0px 0px 14px var(--card-bg, #fff))
    	}
    	.related-page-list .page-list-item .description {
     	padding-top: 0px !important;
     	padding-bottom: 0px !important;
      	line-height: 1.4 !important;
      	z-index: 1;
     }
    	.related-page-list .page-list-item .description .line {
      	font-size: 11px !important;
     }	
     .related-page-list .page-list-item .description .line .inline-icon {
     	font-size: 9px !important;
     }
     .related-page-list .page-list-item .icon {
         position: absolute;
      	width: 100%;
         height: 100%;
         z-index: 0;
         opacity: 1;
         padding: 5px !important;
      }
      
      .related-page-list .page-list-item .icon img {
      	width: 100% !important;
      	height: 150% !important;
        	width: auto !important;
        	margin-right: 0 !important;
      	object-fit: contain;
      }
       .related-page-list .ellipsis {
       	height: 30px !important;
       }
       
       .related-page-list .ellipsis a {
        	padding: 2px !important;
        }
       
       .related-page-list .ellipsis .circle {
       	width: 30px !important;
       	height: 30px !important;
       }
   }
```


2022-02-08
[[インデント表示]]

2022-01-24
[/villagepump/settings#5f818b421280f00000bedd4a](https://scrapbox.io/villagepump/settings#5f818b421280f00000bedd4a)
style.css

```
 /* マトリクス記法 */
 .line:not(.cursor-line) .deco-\| { display: inline-flex }
 .line .deco-\| img.image { object-fit: contain; margin: 0 }
```


2022-01-19
[/takker/takker99/ScrapBubble](https://scrapbox.io/takker/takker99/ScrapBubble)
[[ScrapBubble-min]] [[ScrapBubble]]
style.css_disable

```
div.page {
  overflow-x: visible;
  overflow-y: visible;
}
```


2021-09-08
- ネタバレページをStreamから消す
- [/villagepump/settings#613811fa1280f0000049c5b2](https://scrapbox.io/villagepump/settings#613811fa1280f0000049c5b2)
style.css

```
li.page-list-item.grid-style-item a[href*="%E3%83%8D%E3%82%BF%E3%83%90%E3%83%AC%E6%B3%A8%E6%84%8F"] .description,
.stream .page[data-title*="ネタバレ注意"] {
  display: none;
}
```



2021-01-29
style.css

```
.level-1 img { width: 16.7% }
.level-2 img { max-width: 300px !important; max-height: none !important; width: 100% }
.level-3 img { width: 50%; max-height: none !important}
.level-4 img { width: 66.7% }
.level-5 img { width: 83.3% }
.level-6 img { width: 100%  }
```

[/scrapboxlab/画像のサイズを変えるUserCSS](https://scrapbox.io/scrapboxlab/画像のサイズを変えるUserCSS)


2018-02-04
塩澤先生のプロジェクトから文字数カウンタをコピー
## 文字数カウンタ
style.css_disabled

```
#__charCounter__ { z-index: 300; position: sticky; bottom: 0; text-align: right }
#__charCounter__ span { cursor: pointer; font: 88%/1 monospace; transition: all .2s ease-out }
#__charCounterPopup__ {
  z-index: 300; position: absolute; 
  border-radius: .25em; border: 1px solid #ddd; box-shadow: 0 0 8px 1px rgba(8,8,8,.1);
  padding: .8em; background-color: azure; color: #5F9EA0; font: 13.5px/1.4 monospace;
  transition: opacity .3s ease-out }
```



2018-01-04

- deco-#を強調表示
- 例
style.css_disabled

```
.deco-\# {
  border-radius: .2em; padding: 0 .4em; margin: .4em 0; background-color: rgba(128,128,128,0.1); 
  font-size:200%; line-height:120%}
.deco-\#::before { 
  color: #a0a0a0; content: '#'; }
```



塩澤先生のプロジェクトから良さそうなものをコピー

## 3. 文中に引用を挿入
[/villagepump/インライン引用記法](https://scrapbox.io/villagepump/インライン引用記法)
        - ねこだいすき`[" ねこだいすき]`
        - 例）文章の途中ですがここだけ引用です。
style.css

```
 .deco-\" {
   	border-radius: .2em;
   	padding: 0 .4em;
   	background-color: rgba(128,128,128,0.1); 
   	font-size: 95%;
   	font-style: italic;
 }
 .line:not(.cursor-line) .deco-\"::before { 
   	color: #a0a0a0;
   	font-size: 85%; 
   	/* font-family: 'FontAwesome'; */
   	font-family: 'Font Awesome 5 Free';
   	font-weight: 900;
   	content: '\f10d';
     position: relative;
     top: -0.5em;
     left: -0.2em;
 }
```



- オリジナル
:

```
.deco-\"::before { 
   color: #a0a0a0; font-size:85%; font-family: 'FontAwesome'; content: '\f10d'; vertical-align: super }
```


2017-06-12
画像がない時にはタイトルをたくさん表示する
style.css

```
.grid li.page-list-item a .header .title { overflow: visible }
.grid li.page-list-item a .header { overflow: visible }
.line-img { display: none }
```


画像の立て幅があふれる場合は縦に縮める
style.css 

```
.grid li.page-list-item a .icon img {
	max-width: 100%;
 	max-height: 100%;
  	width: auto; !important
}
```


色を緑にする
style.css-disabled 

```
body {
	background-color: #88cc88;
}
.grid li.two-two.page-list-item a .title {
	background-color: #eeffee; !important
}
.grid li.page-list-item a .content{
	background-color: #eeffee;
}
```


