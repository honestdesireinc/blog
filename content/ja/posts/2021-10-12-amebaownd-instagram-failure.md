---
title: "AmebaowndのInstagram画像連携障害が解消されないまま1年が過ぎようとしている"
date: 2021-10-12T10:16:51+09:00
draft: false
toc: true
tag: ['Amebaownd','Instagram','blog']
---
どうも右ねじです。

表題の件、利用者の中でも気づいている人は気づいているのですが、
なかなか気づきにくい障害が発生しています。

<br>
<br>

## 発生している障害について

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://blog.amebaownd.com/posts/11080844/" data-iframely-url="//cdn.iframe.ly/VfDQc6K?card=small"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

昨年10月26日に報告された、Amebaownd でInstagram連携に障害が発生している件。
症状の説明が無いので、どういったことが起きているか説明します。


### Amebaowndとは

Amebaownd は、アメーバブログで有名なサイバーエージェントが運営する、
誰でも簡単にオシャレなブログサイトが作れるサービスです。

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://www.amebaownd.com/" data-iframely-url="//cdn.iframe.ly/6IDJHui"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

PCからはもちろん、iPhone・iPad・Androidアプリもあるため
どんな端末からでも気軽に投稿・編集が可能になっていて、非常に便利。
デザインテーマも豊富で、その上色合いは自由に編集することができる。
独自ドメインも使えるし、アナリティクスにも対応しています。

さらにはデフォルトでTwitterやInstagram連携が用意されていて、
Instagram連携ページはオシャレにまとまったギャラリーのようです。


### Instagram連携障害について

このAmebaownd で発生した障害というのが、「Instagram画像が表示されない」というものになります。

Amebaownd では、サイト全体とブログ記事の中に使用する画像について、
Instagramアカウントを連携していれば、**Instagramへ投稿した画像から呼び出して使うことができる**
という機能があります。

![](https://user-images.githubusercontent.com/76581368/136882640-2c267dc1-865a-4fae-a07f-cd2958375556.png)

これは、無料ユーザーの中では重宝されている機能でした。
Amebaownd は無料ユーザーだと、使用できる画像ストレージ容量に制限があり、
それが**1GB**と、かなり厳しいのです。
ところがこのInstagram連携を使うと、その画像ストレージを使用せずに
いくらでも画像を表示させることができます。

この機能を使ってサイトに画像を表示させていた場合、**リンク切れになって表示されなくなる**
というのが、今回の障害の内容になります。

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://www.honestdesireinc.com/posts/6453160/" data-iframely-url="//cdn.iframe.ly/NuktMuj?card=small"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

このように、1枚目の画像以外（これだけInstagram連携じゃないため）
すべての画像がリンク切れになって、消えてしまっています。

これではどんな文章が書かれていても、情報が伝わらないどころか、
画像が出なくなっているのに対処していない、サボっているようにも見えてしまい
せっかく見に来てくれた方からの印象が最悪になってしまいます。

### 原因はAmeba側画像ストレージ？

詳しい原因や対処法などは一切どこにも公開されていないため、推測になります。

今回の障害は1ユーザーではなく全体的に発生していて、
またInstagramとの連携という局所的な問題ということから、
**Instagram画像を取得した後に問題が発生したのではないか**と推測します。

理由としては、本件について問い合わせるとAmebaownd サポートより「Instagramのアカウントを再連携して、画像を貼り直してください」とアナウンスされ、
そのとおり実行すると画像が表示されること、
そして、後述する「暫定対応方法」のところで、どの画像を持ってこようとしていたかを調べることができるためです。

もしもInstagramとの連携が機能として破綻しているのであれば、
画像を貼り直しても表示されないはずです。
また、もし「どの投稿の画像かがわからなくなった(データが消失した)」のであれば、暫定対応方法のように
どの画像を持ってきたかは調べられないはず。

Amebaowndでは、Instagram連携を使った画像のURLは、このように出てきます。

![](https://user-images.githubusercontent.com/76581368/136884518-bf39051f-a27e-4dab-881d-6a9ae30f9401.png)

ここから察するに、Amebaownd は画像を連携するときにInstagramから画像データを取得して、
それをAmebaownd側に溜め込んでおくストレージがあるのだと思われます。
これは、Instagram Graph APIのリクエスト回数の制限に抵触しないためでしょう。
画像を表示する度にInstagram側のAPIを呼んでいたら、アクセス数が多いと連携が使えなくなってしまいます。

![](https://user-images.githubusercontent.com/76581368/136886041-28c43a16-7238-4bd1-926c-9c2c91c0c15f.png)

そして、今回の障害では、もしかしたらですが、
そのストレージに障害が発生してしまい、
Instagramから取得してあった画像が消失してしまったのではないかと、
僕は推測しています。

あくまで僕個人の推測で、確かな情報ではございません。


僕は当初、この件を「Amebaownd運営は解決済みだと思っているのでは？」と考えていましたが、
解決済みの障害の場合、下の記事のように復旧した旨が追記されているので、
Amebaownd運営としても未解決の問題だと認識しているのではないか、と推測しています。

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://blog.amebaownd.com/posts/21738002/" data-iframely-url="//cdn.iframe.ly/ta7dYAj?card=small"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

{{< boxmd >}}
2021年9月29日 9:00 追記。
発生しておりました障害ですが、8:50頃までに復旧いたしました。
{{< /boxmd >}}

<br>
<br>


## この障害の恐ろしい点

この障害は、更新頻度が高いサイトや、
過去記事をあまり振り返らないサイトを運営しているユーザーにとっては、
非常に気づきにくいです。

日々記事を投稿していくにつれ、2020年10月26日以前に投稿した、
画像がリンク切れしているページは、運営者の目に触れづらくなっていきます。

しかし、Google検索などでサイトに訪れた方は、
その記事が10月26日以前に投稿されたかどうかなど関係ありません。

サイト運営者が気づかないうちに、訪問者やサーチエンジンからの
評価が下がっていってしまう可能性があるというのが、恐ろしいところです。

<br>
<br>


## サイバーエージェント側としては、対応するメリットがない

また、この障害が発生していることに気づいているユーザーが少ないうちは、
サイバーエージェントとしては対応するのは、メリットがありません。

画像ストレージという、どんどん容量を食っていくであろうものについて
Amebaowndは有料機能として、画像ストレージ無制限を謳っています。

この不具合が困るようであれば、1GBの画像ストレージを使うべきで、
それに満足がいかないのであれば、有料ユーザーになって無制限のストレージを使うべき。

対応してしまうと有料ユーザーを増やす障害にこそなれ、
むしろデメリットでさえあります。

障害発生をきっかけに、この機能を廃止してしまい、
そちら側に舵を切るというのも、経営判断としては致し方ないのかなと思います。

<br>
<br>


## 障害についての説明不足感

とはいえ、そうであればそう説明すべきで、
障害対応しているのであればその状況報告をすべきではないか？
という気持ちは拭えません。

現状、障害について認識しているユーザーの一人としては、
なにもせず放置されているなぁと感じます。
正直言うと、障害が発生していることを忘れさせたい、
改めて告知することで再認識されないようにしたいのかなとも、勘ぐってしまいます。

どういった症状が発生していて、こういう対応をしています、くらいは
告知してほしいところです。

<br>
<br>



## 根本対応

### もしもAmebaownd側ストレージの障害で画像がロストしていたら

Instagram連携したと思われる画像を、全て再取得してほしい。

![](https://user-images.githubusercontent.com/76581368/136886471-d954101b-edca-4edb-949f-afef513a9adf.png)

こちらは画像がロストしている部分の、記事投稿画面のソースです。
画像がロストしている場合、先程とは違いこのように現れます。
記事情報の中に、Instagram連携で取得した画像であるという情報がありますから、
それをもとにAPIを呼び、画像を再取得するというのを、
少しずつ順次実行して、画像ストレージを復活させてくれれば、画像は戻って来るのではないかと思います。

推測が外れていて、全然違う原因だよということであれば、どうしたらいいか外部の僕にはわかりません。

<br>
<br>

## 暫定対応方法(ユーザー側)
ブログ記事が少ない場合は、画像を一枚ずつ貼り直すという荒業で対処することもできます。

デベロッパーツールを使ってブログエディタのソースを見ると、
**「どのInstagram画像を連携しようとしていたか」**を調べることができるので、
それを探し出すことで、もう一度連携しなおせます。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">AmebaOwndでInstagram画像が表示できなくなった件につき、<br>手動で復活させる方法を動画にしました。<br><br>もし他にもっといいやり方をご存じの方がいらっしゃったら、共有いただけますと幸いです。<br><br>公式の障害情報についてはこちら<br>↓<a href="https://t.co/FQ2FC4WLoh">https://t.co/FQ2FC4WLoh</a><a href="https://twitter.com/hashtag/amebaownd?src=hash&amp;ref_src=twsrc%5Etfw">#amebaownd</a> <a href="https://t.co/7aV5YX0MOA">pic.twitter.com/7aV5YX0MOA</a></p>&mdash; 右ねじの法則 (@Rightscrew) <a href="https://twitter.com/Rightscrew/status/1327546323432718336?ref_src=twsrc%5Etfw">November 14, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

ただし、非常に面倒なので、
旅行記やガジェットの使い方報告がメインの僕のブログでは、
心が折れてやめてしまいました。

そのため、僕のこのブログは、画像がほとんどリンク切れになって死んでしまっています。

<br>
<br>

## 症状に気づいている方々のツイート

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">ホームページの写真はインスタから引用しているのですが、たまに表示されていないことがあるようです。何か考えた方が良いかも…。<br><br>【障害のお知らせ】ソーシャルメディア連携に関しまして｜Ameba Ownd Blog <a href="https://t.co/UD0tr5LLRE">https://t.co/UD0tr5LLRE</a> <a href="https://twitter.com/hashtag/amebaownd?src=hash&amp;ref_src=twsrc%5Etfw">#amebaownd</a> <a href="https://twitter.com/hashtag/%E3%83%9B%E3%83%BC%E3%83%A0%E3%83%9A%E3%83%BC%E3%82%B8?src=hash&amp;ref_src=twsrc%5Etfw">#ホームページ</a></p>&mdash; 牧友会 (@makino_alumni) <a href="https://twitter.com/makino_alumni/status/1447104001929990146?ref_src=twsrc%5Etfw">October 10, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">【障害のお知らせ】Instagram画像の表示不具合に関しまして｜Ameba Ownd Blog <a href="https://t.co/FVYHculb9T">https://t.co/FVYHculb9T</a> <a href="https://twitter.com/hashtag/amebaownd?src=hash&amp;ref_src=twsrc%5Etfw">#amebaownd</a> <a href="https://twitter.com/hashtag/%E3%83%9B%E3%83%BC%E3%83%A0%E3%83%9A%E3%83%BC%E3%82%B8?src=hash&amp;ref_src=twsrc%5Etfw">#ホームページ</a> <br>（これ、去年の８月のなんじゃが、まだ復旧してないのかしら？？？）</p>&mdash; ざこん (@zakontheowl) <a href="https://twitter.com/zakontheowl/status/1414734504577552385?ref_src=twsrc%5Etfw">July 12, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">最近、仕様が変わったのか、連携がうまくいっていないのかHPで使用している <a href="https://twitter.com/hashtag/amebaownd?src=hash&amp;ref_src=twsrc%5Etfw">#amebaownd</a> に <a href="https://twitter.com/hashtag/Instagram?src=hash&amp;ref_src=twsrc%5Etfw">#Instagram</a> の写真が反映されず、やや困っています😅<br><br>早く復旧しますよう…✨ <a href="https://t.co/h7BW6JRG35">pic.twitter.com/h7BW6JRG35</a></p>&mdash; 佐藤 雄紀 (@yukisato_piano) <a href="https://twitter.com/yukisato_piano/status/1321083668027351043?ref_src=twsrc%5Etfw">October 27, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">FF外からすみません。その後、解消されましたか？私のサイトはPCでも連携画像が表示されない現象が今も繰返されていて、事務局に問い合わせても「調査にお時間いただきます」と３ヶ月以上も経っています。<br>しかも、1GBしかない画像ストレージを使ってくださいといわれました（笑）</p>&mdash; しんこ (@heureuse0925) <a href="https://twitter.com/heureuse0925/status/1369650411959820288?ref_src=twsrc%5Etfw">March 10, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>


このやり取りをしてから半年が過ぎ、障害発生から数えるともうすぐ1年になります。
