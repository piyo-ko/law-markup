# 法律にマークアップを追加しつつ読んでみよう

## これは何？
法律の条文には、括弧の入れ子や、長く複雑な係り受けがあって、ぱっと一読したときに迷子になることがある。
じっくり眺めて文の構造を一応は把握したとしても、時間が経って読み直すとき、また迷子になったりもする。
そこで、括弧の入れ子構造、名詞句の入れ子構造、どの句とどの句が並列されているのか、などをマークアップすれば、読むときの助けになるのではないかと考えた。
また、その法律の中で特に定義を与えられている語句も、マークアップした方が便利だろうと思った。

そのようにマークアップしたものが本当に読みやすいかどうか、とりあえず自分用の実験として、[「個人情報の保護に関する法律」をマークアップしつつ読んでみた](https://piyo-ko.github.io/law-markup/example/415AC0000000057_20201212_502AC0000000044.xml)。

## 作業内容
1. [e-Gov法令検索](https://elaws.e-gov.go.jp/)で[個人情報の保護に関する法律](https://elaws.e-gov.go.jp/document?lawid=415AC0000000057_20201212_502AC0000000044)を開き、XML 形式でファイルをダウンロードした。
2. この XML ファイルを加工することにした。
なお、私は XSLT が分からないので、スタイルづけには単純に CSS だけを使う。
3. XML ファイルを加工する上で新たに導入する 要素は以下の通り。
    * 括弧の入れ子用に `paren` 要素を導入 (入れ子は三重までを想定してスタイルを定義）
    * 名詞句の入れ子構造、どの句とどの句が並列されているのか、あるいはその他の日本語の構文上の何らかの塊の範囲などを示すために `chunk` 要素を導入 (入れ子は三重までを想定してスタイルを定義）
    * 「及び」「並びに」「又は」「若しくは」は文の構造を読み解くのに便利なので、これらを目立たせるために `and-or` 要素を導入
    * その法律の中で特に定義を与えられている語句を示すために `defined` 要素を導入
    * 元の法律の条文にないメモを追記するのに使うために `memo` 要素を導入
4. CSS はとりあえず適当なスタイルづけにしてあり、アクセシビリティの考慮はできていない (自分用の実験なので)。
5. XML ファイルへのタグの追加は、適当にテキストエディタで一括置換したり、条文を読んで考えつつ `chunk` の範囲を決めたり、という感じで作業した。
大変ローテクである。
`chunk` の付け方が不適当である (文の係り受けの解釈を間違っている) 可能性があり、タグづけの妥当性については無保証である ([間違いの御指摘](https://twitter.com/pi__yo__ko) を頂ければ幸甚です)。
6. 他の条への参照にリンクが使えれば更に便利だが、それは別の話なので (また、ブラウザで XML ファイルを開いたときに使えるリンクの仕方が分からなかったので)、今回はリンクは作業の対象外とした。


## 作業してみての感想
自分にとっては読みやすくなったので、こうしたタグ付け・スタイル付けは、ある程度は有効な気がした（ただ、タグ付けする作業の過程でじっくり本文を読んだから、読みやすく感じるようになっただけなのかもしれない、とも思う）。

他人がタグ付けした、自分にとって初見の条文が読みやすくなる方法であるのかどうかは、まだ分からない。



