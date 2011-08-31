---
layout: post
title: 8月は少し広めに勉強していたので読んだ本をまとめる
---

# {{ page.title }} #

ラボが夏休みに入ると自分のペースでがっつり勉強しても良いんじゃないか、
という気になり色々と手を広げてみました。


## Thermodynamics of Chaotic Systems: An Introduction (Beck & Schlögl) ##

[![Thermodynamics of Chaotic Systems: An Introduction (Beck & Schlögl)
](http://ec2.images-amazon.com/images/I/41MFK9QG4WL._BO2,204,203,200_PIsitb-sticker-arrow-click,TopRight,35,-76_AA240_SH20_OU09_.jpg)
](http://www.amazon.co.jp/gp/product/0521484510?ie=UTF8&amp;tag=toshouldeofgi-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=0521484510)

詳しくは
[SRB測度と自然不変測度の関係を初等的な数学で(略)
](2011-08-23-thermo-chaos-ja.html)
にも書いた。
[カオスの熱力学 (勉強中)](http://tkf.bitbucket.org/thermo-chaos-ja/index.html)
でこの本を参考にしてオレオレ議論を進めた部分をまとめた。


## Statistical Physics of Spin Glasses Information Processing (Nishimori) ##

[![Statistical Physics of Spin Glasses Information Processing (Nishimori)
](http://ec2.images-amazon.com/images/I/41-WdI8q62L._BO2,204,203,200_PIsitb-sticker-arrow-click,TopRight,35,-76_AA300_SH20_OU09_.jpg)
](http://www.amazon.co.jp/gp/product/0198509413/ref=as_li_ss_il?ie=UTF8&tag=toshouldeofgi-22&linkCode=as2&camp=247&creative=7399&creativeASIN=0198509413)
![](http://www.assoc-amazon.jp/e/ir?t=&l=as2&o=9&a=0198509413)

この本は、ラボの理論系セミナーで出てきた replica trick
([レプリカ法 - 機械学習の「朱鷺の杜Wiki」
](http://ibisforest.org/index.php?%E3%83%AC%E3%83%97%E3%83%AA%E3%82%AB%E6%B3%95)
← 分野は違うけどやってることは同じ)
がその時はよく分からなくて悔しかったので、3章まで読んだ。
まあまあエグい(面倒だけどやれば出来る)計算が多くて楽しかったw。
↑のリンクにもあるけど、自然数に成り立つからと言って \\( n \to 0 \\)
の計算に使っちゃう物理なノリが大好きです(ぉぃ)。

本当は、後の方の章にある perceptron の記憶容量なんかが専門に近い
(と言えば近い)部分なんだけど、まあノリ分かったし、必要な時にやればいいや。


## Introduction to Lebesgue Integration (WWL Chen) ##

これは、
[ここから手に入る
](http://rutherglen.science.mq.edu.au/wchen/lnilifolder/lnili.html)
online book。

あれ。なんでこれ読んだんだっけ? あ、そうだ。

1. ↑の Beck & Schlögl で良く分からない箇所があるけど、
   Equilibrium States and the Ergodic Theory of Anosov Diffeomorphisms (Bowen)
   読めば分かりそうだ:

   [![Equilibrium States and the Ergodic Theory of Anosov Diffeomorphisms (Bowen)
   ](http://ws.assoc-amazon.jp/widgets/q?_encoding=UTF8&Format=_SL110_&ASIN=3540776052&MarketPlace=JP&ID=AsinImage&WS=1&tag=toshouldeofgi-22&ServiceVersion=20070822)
   ](http://www.amazon.co.jp/gp/product/3540776052/ref=as_li_ss_il?ie=UTF8&tag=toshouldeofgi-22&linkCode=as2&camp=247&creative=7399&creativeASIN=3540776052)
   ![](http://www.assoc-amazon.jp/e/ir?t=&l=as2&o=9&a=3540776052)

2. 数学が激しすぎるな... weak-* topology てなんぞー。

3. お、ラボにあった Functional Analysis (Reed & Simon)
   に weak-* topology 載ってるから、こいつで勉強しよう。

   [![I: Functional Analysis (Reed & Simon)
   ](https://images-na.ssl-images-amazon.com/images/I/51QwEU2KgbL._SL100_.jpg)
   ](http://www.amazon.co.jp/gp/product/0125850506/ref=as_li_ss_tl?ie=UTF8&tag=toshouldeofgi-22&linkCode=as2&camp=247&creative=7399&creativeASIN=0125850506)
   ![](http://www.assoc-amazon.jp/e/ir?t=&l=as2&o=9&a=0125850506)

4. Preliminaries が読めない><!
   Lebesgue 積分の説明があっさりしすぎてて、昔ちょっとやったはずなのに
   思い出せない。ちょっとやっただけじゃダメだったか...

...って流れだったな。

この本、恐ろしく平易に書かれているのですぐに読めるのですごくお勧め。
ただし、メジャーな測度論から Lebesgue 積分に入る方法ではなく、
積分から測度に入っていく方法をとっているので、他の解析学の本とセット
で使おうとすると相性が悪い。 **って読んだ後に気づいた（笑）。**

この講義ノート
([ルベーグ積分速講 (山上 滋)
](http://sss.sci.ibaraki.ac.jp/teaching/integral/integral2007.pdf))
が多分同じスタンスで、こんなことが書いてある:

> 翻って、もうひとつの方向性である「積分から測度」ですが、 \[...\]
> 「積分の計算・評価が効率的かつ安全にできれば、測度論はあってもなくても
> 良い」といった利用者には、福音となり得るものでしょう。


### 脱線: 関数解析とか実解析あたり、知ってたほうが良いんだろうか ###

... というのが最近の悩みだったりする。
上の Bowen 本が読めなかったのもそうだし、去年は遅延微分方程式の解析
の論文を読もうとして結構苦労したし。ただ、このあたりの数学に強く
なったからと言って、どれほど神経科学におけるモデリング能力が上がる
のかは結構謎なんだよなあ。必要な論文が読めないのは困るけど、去年
は上手く回避出来たし。ただ、これからもし必要になるんだったら PhD
の初期で知ってたほうが絶対に良いよな...。

[Screencasts on Functional Analysis | Explaining mathematics
](http://explainingmaths.wordpress.com/g14fun-functional-analysis-2009-10/)
にある、 screencasts をみながらちょくちょく勉強するのも面白い
んじゃないかと考えたりもしている。


## Real analysis (Royden) ##

[![Real analysis (Royden)
](http://ec5.images-amazon.com/images/I/51a6UkXXYbL._SL500_AA300_.jpg)
](http://www.amazon.co.jp/gp/product/0135113555/ref=as_li_ss_il?ie=UTF8&tag=toshouldeofgi-22&linkCode=as2&camp=247&creative=7399&creativeASIN=0135113555)
![](http://www.assoc-amazon.jp/e/ir?t=&l=as2&o=9&a=0135113555)

この本は3章くらいピックアップして読んで、 Bowen 本に挑戦しようと
思ったけど芋づる式に分からない所が出てきて前の方の章に引き戻されて
いくので、危険を察して今は読まないことにしたw

多分、この本を読んでるあたりで
[SRB測度と自然不変測度の関係を初等的な数学で(略)
](2011-08-23-thermo-chaos-ja.html)
にある初等的な方法を思いついたので、今は良いか、という気分になったのだと
思われる。
ただ、↑に書いた、実解析どうしようかなーという悩みがあるし、
読もうかな...読みたいな...しかし時間が...。


## 確率と確率過程の基礎 (森 真) ##

[![確率と確率過程の基礎 (森 真)
](http://ws.assoc-amazon.jp/widgets/q?_encoding=UTF8&Format=_SL110_&ASIN=432001717X&MarketPlace=JP&ID=AsinImage&WS=1&tag=toshouldeofgi-22&ServiceVersion=20070822)
](http://www.amazon.co.jp/gp/product/432001717X/ref=as_li_ss_il?ie=UTF8&tag=toshouldeofgi-22&linkCode=as2&camp=247&creative=7399&creativeASIN=432001717X)
![](http://www.assoc-amazon.jp/e/ir?t=&l=as2&o=9&a=432001717X)

決定論的な系はまあまあ勉強していたけど確率過程は苦手だった
(しかも理論神経科学はどっちもよく使う!)
のでざっくり読めそうなこの本で勉強した。

こんなこと

> これ読み終わった。確率過程は無勉強だったけど、物理で使える程度には分
> かったかな。最後のほうの章は、数式にミスが増えてきて、「ああ、書いて
> て疲れちゃったんだな」とか思いながら読んでた。 > 確率と確率過程の基礎:
> 森 真: 本 http://amzn.to/pWq4yf
> --- [Twitter / @tkf](http://twitter.com/#!/tkf/status/107441818123247616)

...や、こんなこと

> エルゴード定理の証明が雑過ぎて読めなかったので、これに挑戦したけど2ペー
> ジ目でダメだったw > [math/0608251] Easy and nearly simultaneous
> proofs of the Ergodic ... http://bit.ly/n8GurI
> --- [Twitter / @tkf](http://twitter.com/#!/tkf/status/107442849615851521)

> なんであれ全部自明なんだよ！みたいな。
> --- [Twitter / @tkf](http://twitter.com/#!/tkf/status/107443001076355073)

...を考えながら読んでた。

ちなみに、 エルゴード定理の証明は
[Probability and Stochastic Processes with Applications (Oliver Knil)
](http://www.math.harvard.edu/~knill/teaching/math144_1994/probability.pdf)
(←PDF) を読んだらまあまあ理解できた。
まあまあなのは、いくつか理解出来ない部分があったのと、
書いてあることが理解出来ないから自分で別ルート見つけたけどこれは
あってるか自信ないぞ、という部分があったということ。
この辺の基礎的な数理物理っぽい部分はあんまりありがたみが今は理解
出来ないので、またふらりと気になった時までお預けということで。

しかし、確率過程勉強してても気になる部分は力学系関連だというw


## おまけ ##

[Probabilistic aspects of entropy (Hans-Otto Georgii)
](http://www.mathematik.uni-muenchen.de/~georgii/papers/Dresden.pdf)
にあった、ノイマンがシャノンにしたエントロピーに関するエピソード:

> When Shannon had invented his quantity and consulted
> von Neumann how to call it, von Neumann replied:
> "Call it entropy. It is already in use under that name
> and besides, it will give you a great edge in debates
> because nobody knows what entropy is anyway."

に感動した。
Maxwell's Demon: Entropy, Information, Computing (H. S. Leff)

[![Maxwell's Demon: Entropy, Information, Computing (H. S. Leff)
](http://ws.assoc-amazon.jp/widgets/q?_encoding=UTF8&Format=_SL110_&ASIN=0750300574&MarketPlace=JP&ID=AsinImage&WS=1&tag=toshouldeofgi-22&ServiceVersion=20070822)
](http://www.amazon.co.jp/gp/product/0750300574/ref=as_li_ss_il?ie=UTF8&tag=toshouldeofgi-22&linkCode=as2&camp=247&creative=7399&creativeASIN=0750300574)
![](http://www.assoc-amazon.jp/e/ir?t=&l=as2&o=9&a=0750300574)

からの孫引きです。
