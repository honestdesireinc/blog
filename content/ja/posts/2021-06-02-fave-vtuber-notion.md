---
title: "推しVTuberのアーカイブサイトをNotionでサクっと作った"
date: 2021-06-02T23:35:19+09:00
draft: false
toc: true
tags: ['VTuber','にじさんじ','黛灰','来栖夏芽']
meta_image: "https://user-images.githubusercontent.com/76581368/120514063-ddcdcf80-c407-11eb-8c2d-7134d6010f41.png"
---

## 成果物
黛灰のアーカイブサイト：[黛灰.vlog](https://www.notion.so/mayuzumikai/vlog-92176004090b4f79966119faf94f2bab)
来栖夏芽のアーカイブサイト：[来栖夏芽archives](https://www.notion.so/natsumevlog/vlog-cb48f84b66ae4c99a22c3d6829a6e467)
<!--more-->
<br>

## なぜこんなことをしたのか？
+ Notionくんのことを気になってた
+ Youtubeチャンネルの検索機能だと物足りなかった
+ 黛灰が「[レヴィ・エリファ　アーカイブス](https://levi-archives.site/)」について、「俺もこういうのほしい」と言っていた

主に3.がメインの理由で、[その配信](https://youtu.be/Yx-sk-trWCo?t=11962)を観た翌日暇だったから作った。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">黛灰の配信アーカイブスを簡単に作ってみたけど、どう見えるのかのテスト<a href="https://t.co/ingPLQrhvK">https://t.co/ingPLQrhvK</a></p>&mdash; 右ねじの法則 (@Rightscrew) <a href="https://twitter.com/Rightscrew/status/1394496166973173764?ref_src=twsrc%5Etfw">May 18, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<br>

## Notionのよかったところ
- Webサイトとして使える
- データベースが高速で検索もソートもできる
- カレンダービュー、ギャラリービューが便利

データベースは本当に早いし機能も気が利いてる。関数が特殊で覚える気にならないくらいかな。
これがSpreadsheetとの決定的な違い。

#### カレンダービュー
これが結構、推し活にもいいんです

![来栖夏芽archivesのカレンダービュー](https://user-images.githubusercontent.com/76581368/120504574-38aef900-c3ff-11eb-9117-7c643e4e9c08.png)

「このライバーさんは○曜日と○曜日の配信が多いんだな」ということや、「昼配信が多い/夜配信が多いんだな」とかがひと目でわかるし、
もともと推している人が見ても、「推しはすっごくがんばってるなぁ」と誇らしい気持ちになれるのが良いと思った。

#### ギャラリービュー
今の所「プレイ済みゲーム」をまとめて見れるようにしている。
Youtubeのチャンネルで検索することもできるんだけど、誰とコラボしたか、何をプレイしたかとかを書いてないこともあるし。

![黛灰.vlogのギャラリービュー](https://user-images.githubusercontent.com/76581368/120504266-f4235d80-c3fe-11eb-8dc1-888214d9ef23.png)

再生リストでまとめてくれていたりもするけど…
Youtubeくんの再生リスト画面って、サムネ&再生リストタイトル&再生リスト特有のサムネに被さる表示があって、個人的には探しやすいと思えない。
それよりは、ゲームタイトル一行だけのブロックが並んでたほうが見やすいな～と思った。

しかも勝手にアルファベット順に並んでくれる。君はなんて可愛らしい子なんだ！

<br>

## 実装
NotionはZapierと連携できるし、ZapierでYoutubeの新規動画をトリガーにできると知っていたので

{{< boxmd >}}
Youtubeでチャンネルの新規動画投稿
↓
Zapierが検知
↓
Notionのデータベースに登録
{{< /boxmd >}}

と設定した。

![黛灰.vlogのデータベース](https://user-images.githubusercontent.com/76581368/120504511-292fb000-c3ff-11eb-8a71-e0dc53e9b75b.png)

新規動画がアップされると新規レコードが追加され、連携が成功した。
プレミア公開動画は、

{{< boxmd >}}
プレミア公開設定時に、その時点で新規登録
↓
プレミア公開後に、動画公開日時のみ更新
{{< /boxmd >}}

という動きになるみたいだ。

データベースを作るところは、1件1件作っていては埒が明かないので、
Google Colaboratory上にコピーして使えるツールを使った。

参考サイト：
<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://blog.codecamp.jp/programming-api-youtube" data-iframely-url="//cdn.iframe.ly/lCt7DAt?card=small"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://qiita.com/shimajiroxyz/items/283b57537de8b1bc9add" data-iframely-url="//cdn.iframe.ly/XBOZ4kf?card=small"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

SEをやっておきながらコーディングはやったことがないので、
コピペで実装してみたら、以下2点うまくいかなかった。

+ 上だと、5件分しか抽出できない
+ 下だとかなりの件数を一括で出力できるが、たまにクラッシュさせる動画が存在してデータが欠ける

下の方であれば拾えるデータの量としては多いので、引っかかったところだけ手動でデータ投入するのも良かったんだけど、
やりたくなくて別の手段がないか調べていたら、こんなものを見つけた。

<div class="iframely-embed"><div class="iframely-responsive" style="padding-bottom: 50%; padding-top: 120px;"><a href="https://ipr.tokyo/" data-iframely-url="//cdn.iframe.ly/W1s0QYE"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

本来は、どのインフルエンサーに案件動画を発注するのが効果的かを調べるためのサービスらしい。
これを使うと、チャンネル動画の情報をCSV出力することができた。

これはトライアル申し込みから実際に使えるまで4日くらいかかったので、その間に別のことをした。

<br>

## コラボ情報・ゲームタイトル情報の入力
Notionのデータベースにはタグ付けデータを登録できるので、動画を開きながら
・これはコラボなのか、ソロなのか
・コラボなら誰とか、ユニット名があるか
・ゲーム配信なのか雑談か
・ゲーム配信なら何のゲームをしているか
を登録していった。

![](https://user-images.githubusercontent.com/76581368/120508397-a4df2c00-c402-11eb-8d1d-07dd00183972.png)

このようにリストが出てきて、既に登録したものと同じだったら選ぶだけ。
なければ文字列を打ち込んで、新規登録する。

完了するとこんな感じに、カラフルになる。
![](https://user-images.githubusercontent.com/76581368/120505193-b6730480-c3ff-11eb-958a-45c2f48ca48f.png)

…言いたいことはわかる。そう、これは人力だ。
けどこれはYoutubeの検索機能で拾えないものを拾えるようにするためだから仕方ない。

<br>

## Search engine indexing をON
Notionはもともとメモアプリなので、
基本的には大勢にシェアするサービスじゃない。
(そりゃそうだ、アクセスが超来るようになったら
メンテナンスコストが激増して商売上がったりになる)

そのため、検索エンジンで表示する機能は、月$4の有料オプションになっている。

#### なかなかGoogleに反映されない
なんでだろうと思って色々見直したりしたんだけど、結局わからなかったので、問い合わせた。
慣れない英語でどうにかわかったのは、
・「Notionのコンテンツそれ自体をGoogleに登録してくれる機能じゃない」
・「このページヘのリンクがWeb上にあれば、Google検索に引っかかるようになる」
こういうことらしかった。

恐らくTrelloの件とかもあったからか、あらかじめnoindexが付いてるんだと思う。

僕がこの記事を書いているのはまさに、作ったNotionページへのリンクをWeb上に貼るためです。

<br>

## 運用について
推しの配信は見るので、アーカイブが上がる頃には
ジャンル・コラボ情報も、プレイしたゲームもわかってる。
ということで、思い出にほくほくしながら、データベースに情報を追加している。

気をつけないといけないのは、
アーカイブが上がった後には新規レコードが登録されているため、
その後でアーカイブが限定公開になったら、手動でレコードを消しておいたほうがいいだろう。

<br>

## 悩みどころ
本人のチャンネル動画しか登録していないため、コラボ相手の方の枠しかなかった場合は乗ってないこと。
その辺はもう、非公式Wikiを見ながら入れていくしか無いのかも知れない。

<br>



## 作ってみた結果

正直言って、作った自分に一番刺さってる。
カレンダー眺めてるだけで幸せだし、おもろそうなアーカイブ見つけて見に行ったり。
黛灰のポケモン配信や、まななつハウスの拡張配信とかね。
作ってよかった本当に。。

なんとなくNotionでできることがわかったのも良かった。
会社に導入するつもりにはならないけど、何か個人プロジェクトをやる時、旅行の計画を立てるときにはいいかもしれない。