---
title: "AWSのインスタンスを消し忘れるくせに2段階認証アプリは消すアホが、公証役場で外国文認証を取得することになった話"
date: 2021-03-06T12:57:31+09:00
draft: false
toc: true
meta_image: "https://user-images.githubusercontent.com/76581368/110194529-fc114700-7e7b-11eb-865d-aeb35245e709.png"
tags: ["やらかしリカバリ","AWS"]
---
右ねじです。長らくお待たせしました。
お待ちかねの、失敗のリカバリシリーズ新作です。

今回は、**AWSのインスタンスを残したまま2段階認証アプリを消してみました！**
<!--more-->

#### やらかしリカバリシリーズとは
うっかり者の右ねじが何かやらかしたとき、
よく考えればそんなに焦る必要はないのに、
テンパってどんどん悪い方向への想像が止まらなくなって、
勢いに任せて失敗をリカバリしようとして、
全ての対応が終わった後に
「なんだったんだ…」
という気持ちを整理するために書いている
ノンフィクション狂騒曲です。

特に縦読みとかではありません。西尾維新でもカゲロウプロジェクトでもありません。

・前回
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">冷蔵庫が冷えてなかった代わりに、ぼくの肝が冷えた話 <a href="https://t.co/ZCyK5dM0B4">https://t.co/ZCyK5dM0B4</a> <a href="https://twitter.com/hashtag/%E5%86%B7%E8%94%B5%E5%BA%AB?src=hash&amp;ref_src=twsrc%5Etfw">#冷蔵庫</a> <a href="https://twitter.com/hashtag/%E4%BF%AE%E7%90%86%E6%89%8B%E9%85%8D%E3%83%AC%E3%83%9D?src=hash&amp;ref_src=twsrc%5Etfw">#修理手配レポ</a></p>&mdash; 右ねじの法則 (@Rightscrew) <a href="https://twitter.com/Rightscrew/status/1368055002007175171?ref_src=twsrc%5Etfw">March 6, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## 始まりは一通のメール
3/3、メールボックスを見てたらこんなのが来ていました。
<img src="https://user-images.githubusercontent.com/76581368/110194726-37604580-7e7d-11eb-9061-3dce23c6b892.png" width=50%>
去年の2月あたり、AWS認定の勉強のために、AWSの無料枠を使っていろいろやってました。
その時に作ったインスタンス、何か消し忘れたっぽいな…。
とりあえずログインして、金額見てみるか。

あ。

## AWSにログインできない
AWSには、ルートアカウントとIAMユーザーアカウントのどちらかでログインできます。
僕は確か、勉強が終わったタイミングでIAMユーザーは消していたはずなので、
ルートアカウントでログインしようとしました。
そしたら、メールアドレス・パスワードを入力後、MFA認証コード(2段階認証)を要求されました。

2段階認証自体は、iPhoneを使ってる人だったら見慣れてると思いますし、最近増えてきてるのでイメージわきますよね？Webサイトにログインするとき、電話番号にSMSで認証コードが送られてくるやつです。

AWSの場合、それが電話番号宛にSMS送られるんじゃなくて、
認証用のアプリに1分毎に更新されるコードが表示されています。
<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://apps.apple.com/jp/app/google-authenticator/id388497605" data-iframely-url="//cdn.iframe.ly/wDD105x?iframe=card-small"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>
こういうやつですね。

僕はこれを設定していたアプリを、**「もうAWS使ってねーし消すか」** って消しました。

だってスマホのホーム画面が雑然としてたんだもん…

## 2段階認証を解除してもらおう
AWSにログインできなくても実務上は困らないけど、請求がこれからも来つづけてしまうため、ログインして止めたい。
今後のために2段階認証を解除してもらおう。
AWSの問い合わせフォームに情報を入れたら、30分以内に電話が来ました。

AWSに登録していた電話番号にかけてもらい、本人確認ができれば、その場で2段階認証を解除してもらえます。

ですが僕は解除してもらえませんでした。

なぜなら、**AWSに登録していた電話番号は、解約してしまっていたからです。**

マジで何でこんなことになる？ぷよぷよか？

## AWS請求に関するエンジニアのやらかしブログが頭をよぎる
ここまでやらかしが続いてしまったため、思考はどんどんマイナス方向に落ちていきます。
AWSの請求でやらかしといえば、AWSへのログインに必要なキーを、GithubやTerraformに公開してしまっていて、第三者に不正利用されて高額な請求になってしまうというもの。
![](https://user-images.githubusercontent.com/76581368/110196931-49e17b80-7e8b-11eb-830f-ebd843a3feb4.png)
自分もこういう失敗をやりそうだと思っていたので、興味をもって読んでいました。
僕の場合は勉強のためにインスタンス作っていただけなので、どこにも公開してないはずだけど…
もしかしたら…
自分では気づかないどこかに…

そう思うと気が気じゃなく、即座に2段階認証解除申請を進めました。


## 2段階認証解除申請書類を用意する
電話のあとすぐ、こんなメールが来ました。
<img src="https://user-images.githubusercontent.com/76581368/110195679-44336800-7e82-11eb-84b5-256de9dfb653.png" width=60%>
<br>

<img src="https://user-images.githubusercontent.com/76581368/110196070-65498800-7e85-11eb-8cea-d96e13cf6fc8.png" width=60%>
<br>

![](https://user-images.githubusercontent.com/76581368/110196089-86aa7400-7e85-11eb-8914-a0113aec01ca.png)

うわ～～～～～めんどくさそうな文面でとっても読みたくない

要は、[このPDF](https://aws-support-documents.s3-us-west-2.amazonaws.com/Forms/MFAIndividualIdentityVerificationFormAffidavit.pdf)に記名して印刷したうえで、
**公証役場**に行って**外国文認証**の手続きをしてもらい、
それをPDF化しなさいということでした。

めっちゃ時間かかりそう。

僕の家には複合機が無いので、PDFを作ったらコンビニの複合機で印刷する必要がある。
そしてスキャンするにもまたコンビニへ…もうプリンター買おうかな
書類は用意できたけど、時刻はもう20時。そんな時間に公証役場、開いてるわけないよね…？
![](https://user-images.githubusercontent.com/76581368/110196357-4e0b9a00-7e87-11eb-80ba-9b6a48fe4e31.png)
そりゃそうですわ。
平日しかやってない&閉まるのが早いのも解釈一致。

3/4(木)、在宅勤務だったのでPCを持ち出し、テザリングでNWつなぎっぱなしにして行ってきました。

## 渋谷公証役場

![](https://user-images.githubusercontent.com/76581368/110194171-76d96280-7e7a-11eb-9d6f-0557e3e18084.png)
渋谷公証役場は、タワレコ前の神南郵便局のビルの8Fにありました。


<br>

![](https://user-images.githubusercontent.com/76581368/110194173-7b9e1680-7e7a-11eb-9217-712977b2d38c.png)
めっちゃ小規模オフィスだった


![](https://user-images.githubusercontent.com/76581368/110194163-6b863700-7e7a-11eb-96b2-481f41a6d685.png)

認証申込書を書く。
外国文認証をしてもらうのに必要なところを教えてもらいながら記入する。

※アメリカの場合は、州を記入してください。　って書いてあるけど、
わからなかったらアメリカだけでいいって言ってもらえました。

外務省までの認証、認証の英訳文は別に要らないんだけど、手数料変わらないって言われたのでせっかくだからつけてもらいました。

所要時間は1時間かからないくらい。
色々聞きながら受付してもらい、
受付の後5分くらい待って、
公証人さんに呼ばれて書類にサインして、
10分くらい待って書類もらって、
支払いして終了。

## これが認証の英訳文だ！！

![](https://user-images.githubusercontent.com/76581368/110194177-7f319d80-7e7a-11eb-9ef8-b8f67b575a3b.png)

ちょっと最近色んなフォント入れてたから、ラブリーなフォントにしておいた

## これが外務省までの認証だ！！

![](https://user-images.githubusercontent.com/76581368/110194179-822c8e00-7e7a-11eb-8af9-adc4ea15f5d1.png)

おぉ～～～～～なんかよくわからんけど、お墨付きだ

トータルで4ページにまたがる書類になったけど、見開きで割り印がされているので、
スキャンするときには分解してはいけない。分解すると無効になります。

書類全体をスキャンしてPDFにし、免許と公共料金の支払い明細PDFと一緒にメールに貼り付けて送信。
あとは、2段階認証を解除してもらえるのを待つだけ。

ちなみにメール送信したのが3/4の13:17。

2段階認証が解除されたのが、3/5の16:11。

## 48時間後に対面した請求額

![](https://user-images.githubusercontent.com/76581368/110197060-3e428480-7e8c-11eb-9655-9d3c86ed61de.png)

$1.32

143円。

不正利用とかではなく、勉強用に使っていたCloud9用のEC2が残っていて、それのストレージ(EBS)が無料なのはアカウント開設から12か月だったため、1年経って請求が始まったのでした。

よかった～～～～～～～～！！！！！！！！

## 教訓がたくさんあります
1. AWSを無料利用枠でいじったあと、終わったらちゃんと全部消すこと
2. EC2だけ消してもEBSは消えないから個別に消すこと
3. 2段階認証アプリは不用意に消さないこと、機種変更する場合ちゃんと引継ぎをすること
4. 携帯電話番号を解約する前に、各種サービスに登録していないか確認すること
5. AWSのキーペアを第三者に見えるところに公開しないこと

最後は自分のじゃないけどね、改めて学びとしておきたいなと思います。


というわけで、**AWSのインスタンスを消し忘れるくせに2段階認証アプリは消すアホが、公証役場で外国文認証を取得することになった話**　でした。

僕としてはこれ以上この、やらかしリカバリシリーズは続けたくないのですが…
またお目にかかったら、笑っていただければ幸いです。

ねぇ笑って？