
mime-typeに関する「データベース」であるfreedesktop.org.xmlに著作物性があるかどうか、という話。

例えばそのデータベースが下記のようなものだったら、これは単なる網羅的な事実の列挙であって、体型的な構成に創作性がないので「[[データベースの著作物]]」としての保護の対象にはならない。
:
| *.json | application/json |
| -- | -- |
| *.orf | image/x-olympus-orf |
| *.svg | image/svg+xml |
| *.pl | application/x-perl |

じゃあfreedesktop.org.xmlは実際にはどう言う記述なのか。先に僕の結論を書いておくと、データベースと解釈しても創作性が高いし、むしろ[[プログラムの著作物]]だと言って良いレベルだと西尾は考えている。

masterからは消えているので過去のリビジョン: [mimemagic : freedesktop.org.xml](https://github.com/mimemagicrb/mimemagic/blob/c0f7b6b21a192629839db87612794d08f9ff7e88/script/freedesktop.org.xml)

たとえば、ファイル名のパターンとmime-typeの対応づけだけでなく、人間が読むためのコメントや、略称とその略さない書き方、jsonはjavascritのサブクラスであるという関係、人間に対してアイコン表示するときにどのアイコンを使うか、などが書かれている。
この時点で既に「単なるmime-typeのデータを羅列したもの」を超えた創作性がある構成になっているのではないか、少なくとも著作物性が認められているタウンページ程度には…というのは一旦保留して先を読み進める。
xml

```xml
  <mime-type type="application/json">
    <comment>JSON document</comment>
    <acronym>JSON</acronym>
    <expanded-acronym>JavaScript Object Notation</expanded-acronym>
    <sub-class-of type="application/javascript"/>
    <generic-icon name="text-x-script"/>
    <glob pattern="*.json"/>
  </mime-type>
```


さらに、ものによってはコンピュータの処理対象にならないコメント文の形で、このファイルを読む人間に向けて「ORFは標準に準拠していないTIFFだ」などの解説が書かれている。
つまりこのファイルは機械的に出力されるものではなく、人間が読んだり書き換えたらする想定だということ。
xml

```xml
  <mime-type type="image/x-olympus-orf">
    <comment>Olympus ORF raw image</comment>
    <acronym>ORF</acronym>
    <expanded-acronym>Olympus Raw Format</expanded-acronym>
    <sub-class-of type="image/x-dcraw"/>
    <magic priority="50">
      <!-- an ORF file is basically a TIFF file with a non standard !-->
      <!-- header IIRO which is not nice since it is only composed  !-->
      <!-- of ASCII codes. Fortunately, the TIFF header is followed !-->
      <!-- by the offset of the first TIFF ifd which is always      !-->
      <!-- 0x00000008 (Little endian) for an ORF                    !-->
      <match value="IIRO\x08\x00\x00\x00" type="string" offset="0"/>
    </magic>
    <glob pattern="*.orf"/>
  </mime-type>
```


SVGでは、無償のツールであるInkscapeが出力するコメント文などがあるかをチェックして判断に使っている。不確かなヒントを使うためにpriorityの値で判断の確信度を表現している。
要するにこれは条件判断の方法を記述したものであり、しかもこの判断ルールはなんらかの仕様書などから機械的に作られたものではなく人間が現実のファイルを眺めて「どうすれば判断できるだろう」と考えて作り出したものだ。
xml

```xml
  <mime-type type="image/svg+xml">
    <comment>SVG image</comment>
    <acronym>SVG</acronym>
    <expanded-acronym>Scalable Vector Graphics</expanded-acronym>
    <sub-class-of type="application/xml"/>
    <magic priority="80">
      <match type="string" value="&lt;!DOCTYPE svg" offset="0:256"/>
    </magic>
    <magic priority="80">
      <match type="string" value="&lt;!-- Created with Inkscape" offset="0"/>
      <match type="string" value="&lt;svg" offset="0"/>
    </magic>
    <magic priority="45">
      <match type="string" value="&lt;svg" offset="1:256"/>
    </magic>
    <glob pattern="*.svg"/>
    <root-XML namespaceURI="http://www.w3.org/2000/svg" localName="svg"/>
  </mime-type>
```


Perlに至っては、そもそも拡張子が多様であることを、どういう時の拡張子なのかコメント付きで列挙した上で、Perlのコード中に出現しやすいパターンをヒントにして判断しようとしている。
xml

```xml
  <mime-type type="application/x-perl">
    <comment>Perl script</comment>
    <sub-class-of type="application/x-executable"/>
    <sub-class-of type="text/plain"/>
    <generic-icon name="text-x-script"/>
    <alias type="text/x-perl"/>
    <magic priority="50">
      <match type="string" value='eval \"exec /usr/local/bin/perl' offset="0"/>
      <match type="string" value="/bin/perl" offset="2:16"/>
      <match type="string" value="/bin/env perl" offset="2:16"/>
      <match type="string" value="use Test::" offset="0:256"/>
      <match type="string" value="BEGIN {" offset="0:256"/>
    </magic>
    <magic priority="40">
      <match type="string" value="use strict" offset="0:256"/>
      <match type="string" value="use warnings" offset="0:256"/>
      <match type="string" value="use diagnostics" offset="0:256"/>
      <match type="string" value="\n=pod" offset="0:256"/>
      <match type="string" value="\n=head1 NAME" offset="0:256"/>
      <match type="string" value="\n=head1 DESCRIPTION" offset="0:256"/>
    </magic>
    <glob pattern="*.pl"/>
    <glob pattern="*.PL"/><!-- CPAN-style Perl build script -->
    <glob pattern="*.pm"/><!-- module -->
    <glob pattern="*.al"/><!-- autoloader -->
    <glob pattern="*.perl"/>
    <glob pattern="*.pod"/><!-- documentation -->
    <glob pattern="*.t" weight="10"/><!-- CPAN-style Perl test script -->
  </mime-type>
```


このように、このXMLファイルはコンピュータに拡張子とファイルの内容からmime-typeを判別させるための指令の組み合わせである。
著作権法におけるプログラムの定義は「電子計算機を機能させて一の結果を得ることができるようにこれに対する指令を組み合わせたものとして表現したもの」であり、要件を満たしている。表現方法がXMLであることはプログラムであるかどうかの判断には関係ない。

----
タウンページの件と比較したTwitterでの議論のまとめ:
- タウンページは「名前と電話番号の組み合わせという創作の余地のないデータ」を集めたものであって、それを汗をかいて集めただけでは著作物にならないが、職業別分類には創作性があるからデータベースの著作物になった。
- 今回のケースは「ファイル冒頭のどのオフセットの値を確認してmime-typeを判断するかの指令」がそもそもかなり独自の工夫がある創作性のある情報だからデータベースの著作物以前にプログラムの著作物なのではと西尾は考えている
