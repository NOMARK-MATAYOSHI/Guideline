# cssメンテナンスガイド

## 概要

CSSは非常に簡素な言語であり学習コストも他言語に比べると極めて低い。<br>
しかしながら、所謂「オレオレセレクタ」や無為なネストなど言語仕様がゆるい分、特に大規模なプロジェクトだと複数人かかわると、途端に崩壊＆黒歴史＆メンテナンス地獄にかかってしまう。<br>
本稿では「一貫性」「誰が読んでも理解できる」「簡潔に単純」「重複を避ける」の基本概念とした、一般的なCSS定義ルールとルールの必要性を説明する。


---


## 1.class名は意味が分かる単語＆省略
### Bad
~~~
.navigation {
  margin: 0 0 1rem 2rem;
}
.atr {
  color: #93c;
}
~~~
### Good
~~~
.navi {
  margin: 0 0 1rem 2rem;
}
.author {
  color: #93c;
}
~~~

### Why?
> ファイルサイズの節約。<br>
> class名が長い = ファイルサイズが大きくなる = UX損なわれる。<br>
> ただし意味がわからない省略であれば逆に省略しないほうがいい。<br>
> 単語の省略はコーディングガイドラインを参照。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 2.プロパティは可能な限りショートハンドで定義
### Bad
~~~
.list-box {
  border-top-style: none;
  font-family: serif;
  font-size: 100%;
  line-height: 1.6;
  padding-bottom: 2em;
  padding-left: 1em;
  padding-right: 1em;
  padding-top: 0;
}
~~~
### Good
~~~
.list-box {
  border-top: 0;
  font: 100%/1.6 serif;
  padding: 0 1rem 2rem;
}
~~~

### Why?
> ファイルサイズの節約。<br>
> 記述時間の削減
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 3.小数点の値の接頭の0を省く
### Bad
~~~
.list-box {
  font-size: 0.8rem;
}
~~~
### Good
~~~
.list-box {
  font-size: .8rem;
}
~~~

### Why?
> ファイルサイズの節約。<br>
> 記述時間の削減。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 4.16進数の色定義はできるかぎり三桁で記述
### Bad
~~~
.list-box {
  color: #eebbcc;
}
~~~
### Good
~~~
.list-box {
  color: #ebc;
}
~~~

### Why?
> ファイルサイズの節約。<br>
> 記述時間の削減。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 5.IDセレクタは使わない
### Bad
~~~
#info-title {
  font-size: 3rem;
}
~~~
### Good
~~~
.info-title {
  font-size: 3rem;
}
~~~

### Why?
> 様々な考え方があるのでコーダーによって議論がある内容です。<br><br>
> 理由1 : ID名は再利用できない<br>
> 同一ID名は1ページのHTML内に1つだけしか使えません。いわば「固有名詞」になります。<br>
> IDは「identity」の略で要素を特定するためのものですので、再利用の観点から非効率になります。<br><br>
> 理由2 : スタイル適用の優先順位を意識する必要がある<br>
> CSSのセレクタは優先順位があります。<br>
> 一般的なCSSの定義では、スタイルは上から順に定義されて以前のルールを上書きしていく、順番とは別に個別に定義したい場合は、加重セレクタを使って重み付ける、が一般的です。<br>
> IDセレクタはclassセレクタよりも優先されるため、上記定義を考えると子孫セレクタ名が増えたり、記述箇所を変更したりなど、メンテナンスまで考えると手間が増える恐れと可読性が落ちます。<br>
> <br>
> 理由3 : 汎用的な使用ができない<br>
> 理由1と同じですが、共通するデザインについては名前を抽象化して使うことがスマートです。<br>
> ID名は理由1で述べたように固有名詞なので「特定」であり、抽象的なものでないです。よってclassを使用するべきです。<br><br>
> ID要素を使う場合、ページ内リンクやJSのフックに使うなどに限定する使用方法を推奨します。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 6.class名には要素型セレクタ（タイプセレクタ）を記述しない
### Bad
~~~
li.member-list {
  color: #06c;
}
~~~
### Good
~~~
.member-list {
  color: #06c;
}
~~~

### Why?
> 可読性の向上。<br>
> 詳細度の高くなり且つ別の要素で再利用できない。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 7.数値ゼロには単位をつけない
### Bad
~~~
.example {
  margin: 0rem;
}
~~~
### Good
~~~
.example {
  margin: 0;
}
~~~

### Why?
> JSとCSS、それぞれの修正が極力相手に影響しないよう疎結合を保つため。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 8.インデントや改行、コメントをつける、ブロックの開始位置を統一
### Bad
~~~
.header{margin:0rem;}
.member__box,.friend__box{color:#fec;background-color:#006;}
.nav
{
color:#ff0;
}
~~~
### Good
~~~
// .header
.header {
  margin: 0rem;
}

// 共通CSS
.member__box,
.friend__box {
  color: #fec;
  background-color: #006;
}

// .nav
.nav {
  color: #ff0;
}
~~~

### Why?
> 可読性向上のため。<br>
> メンテナンス性向上のため。<br>
> ※上記はSass(Scss)やLESSなどのCSSプリプロセッサの使用を前提にしてます。<br>
> 会社や個人の文化によって異なりますが、混在するとわかりずらいものになるので統一した内容で記載するように共通化のためのコミュニケーションが必要です。<br>
> 例えば以下のように進めると良いです。<br>
> 1. ブロック単位でインデントをつける<br>
> 2. プロパティの終端には「;」をつける<br>
> 3. プロパティの値の間「:」の後には、半角スペースをつける<br>
> 4. 別々のセレクタやプロパティは複数行で記載<br>
> 5. 別々のCSSルールは1行空ける
> 6. セレクタ記述後の波括弧の間に半角スペース
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 9.ユニバーサルセレクタの使用は極力さける
### Bad
~~~
* {
  font-size: .8rem;
}
~~~
### Good
~~~
html,body {
  font-size: .8rem;
}
~~~

### Why?
> 可読性向上のため。<br>
> 影響範囲が広いため使用の際は極力注意する。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 10.セレクタ名にスタイルに関する名前をつけない
### Bad
~~~
.blue--text {
  color: #00f;
}
~~~
### Good
~~~
.highlighted--text {
  color: #00f;
}
~~~

### Why?
> メンテナンスや再利用の観点から、スタイルに関する名前をつけると後々変更する際に意味とスタイルが異なる場合があります。<br>
> 最悪以下ようになる恐れもあります。<br>
> .blue--text {<br>
> 　color: red;<br>
> }<br>
> このようなもので乱雑になるので、「目的」になるような名前をつけたほうが適切です。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 11.ネストを深くしない、セレクタをHTML構造から切り離す
### Bad
~~~
.content #intro .icon { … }
.header > nav > li > button { … }
~~~
### Good
~~~
.intro__icon { … }
.header__button { … }
~~~

### Why?
> CSSには詳細度というものがありセレクタを詳細に記載すればするほど、特異性が向上するので上書きの難しさや可読性が悪くなります。<br>
> !importantやIDセレクタを使って打開しようとしてしまう恐れもあるので、なるべくネストは浅くするように考慮しましょう。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 12.セレクタの順番はHTML構造順に合わせて記載
### Bad
~~~
.footer { … }
.header { … }
~~~
### Good
~~~
.header { … }
.footer { … }
~~~

### Why?
> HTML/DOMツリーのレンダリングは基本的に上から順番に行われていきます。CSSについても同様ですのでHTMLツリーに合わせたほうが良いです。<br>
> ※汎用的なスタイルがあれば、先に記述したほうがメンテンナンス性が向上しますので、厳密ではないです。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 13.特異性があるセレクタの順番あとにする
### Bad
~~~
.list-item:first-child { … }
.list-item { … }
.list-item:last-child { … }
~~~
### Good
~~~
.list-item { … }
.list-item:first-child { … }
.list-item:last-child { … }
~~~

### Why?
> 特異性があるものを前にするとコードが理解しずらく、場合によって上書きされてしまうこともあるので、理解や影響範囲等が猥雑になります。<br>
> 汎用的なセレクタを前にし、特異性のあるセレクタはその後にしましょう。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 14.ページやコンポーネントを意味するセレクタは、同じ単語で始まるようにする
### Bad
~~~
.front__page__title { … }
.intro__home { … }
.home__text { … }
~~~
### Good
~~~
.home__title { … }
.home__intro { … }
.home__text { … }
~~~

### Why?
> 可読性向上のため。<br>
> 上記は全て「トップページ」で使用するセレクタ名です。<br>
> 「front」「index」「intro」「home」など、どちらもトップページを意味する単語が乱雑になると、特に複数人で作業する場合やCSSを複数ファイルに分割する場合など、管理が難しくなります。<br>
> 共通する単語にすることで、どの箇所かページかの理解が早くなります。<br>
> ※HTMLやCSSなどファイル名も共通すると更に理解が早いです。
<br>

<p><a href="#">ページ上部へ戻る</a></p>

<br>

---

<br>

## 参考文献
- [メンテナブルCSS | 株式会社サイバーエージェント](http://web.archive.org/web/20160702044546/https://www.cyberagent.co.jp/techinfo/techreport/report/id=7926)
- [8 CSS selectors DO’s and DON’Ts](https://medium.com/@aljullu/8-css-selectors-dos-and-don-ts-1e0d23fcf96c)
- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
- [コーディングガイドライン（HTML5）ver1.0](http://met.hanatoweb.jp/guideline/html5/)

以上です。
