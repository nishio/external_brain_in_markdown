
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
        - ねこだいすき`[" ねこだいすき]`
        - 例）文章の途中ですがここだけ引用です。
style.css

```
.deco-\" {
  border-radius: .2em; padding: 0 .4em; background-color: rgba(128,128,128,0.1); 
  font-size:95%; font-style: italic }
.deco-\"::before { 
  color: #a0a0a0; content: '>'; }
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
style.css 

```
body {
	background-color: #88cc88;
}
#.grid li.page-list-item a .header{
#	background-color: #eeffee;
#}
.grid li.two-two.page-list-item a .title {
	background-color: #eeffee; !important
}
.grid li.page-list-item a .content{
	background-color: #eeffee;
}
```


