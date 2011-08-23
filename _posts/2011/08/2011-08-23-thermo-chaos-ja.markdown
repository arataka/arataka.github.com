---
layout: post
title: SRB測度と自然不変測度の関係を初等的な数学で導けたのでカオスの熱力学の勉強中ノートを公開してみる
---

# {{ page.title }} #

[![Thermodynamics of Chaotic Systems: An Introduction (Beck & Schlögl)
](http://ec2.images-amazon.com/images/I/41MFK9QG4WL._BO2,204,203,200_PIsitb-sticker-arrow-click,TopRight,35,-76_AA240_SH20_OU09_.jpg)
][http://www.amazon.co.jp/gp/product/0521484510?ie=UTF8&amp;tag=toshouldeofgi-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=0521484510]

[カオスの熱力学 (勉強中)](http://tkf.bitbucket.org/thermo-chaos-ja/index.html)
にて絶賛公開中。

Beck & Schlögl の
[Thermodynamics of Chaotic Systems: An Introduction
](http://www.amazon.co.jp/gp/product/0521484510?ie=UTF8&amp;tag=toshouldeofgi-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=0521484510)
に[出会ってから
](http://arataka.wordpress.com/2009/02/25/mathematics-methods-of-statistical-mechanics/)
早くも二年 (早い!)。
自分のやってる研究に関係無いこともあってなかなか気合を入れて読む機会
が無かったのだけど、ラボが夏休みに入って良い機会だし、と思ってここ
二週間くらいでちょくちょく読んでみた。

この本、現代数学に疎くてもカオスについてかなり学べるし、(統計)熱力学的を
ちゃんと勉強したこと無いからどこかでやらないとなーと思っていた自分には、
一石二鳥の本だった。

ただ、この本の19章の議論の結構骨になっている部分で、「論文の結果を載せて
終わり」になっている部分があり、議論が完結していなくてとてもむずむず
していてしょうがなかった。仕方ないなーちょっと数学やりなおしてから再挑戦
かなーと思いつつ、最後の頼みの綱の前ラボの数学者の方にお伺いのメールを
送ってやりとりをしていたところ、自己解決してしまった。忙しいのにいっぱい
メールしてすいません＞＜!（ぉぃ。 やっぱり最初にクマさんぬいぐるみメソッド
を使うべきだったか...。

問題だった部分は Gibbs 測度 と
[Perron-Frobenius 演算子との関係
](http://tkf.bitbucket.org/thermo-chaos-ja/gibbs-measures-and-srb-measures.html#perron-frobenius)
と、
[SRB 測度 と 自然不変測度
](http://tkf.bitbucket.org/thermo-chaos-ja/gibbs-measures-and-srb-measures.html#srb)
の関係。
数学やってる人からだと怒られそうだけど、これくらい感覚的に分かっていない
と納得出来ないんだよなあ。
