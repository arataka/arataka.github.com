---
layout: post
title: 興奮・抑制均衡入門 (理論神経科学チュートリアル) のα版を公開します
---

# {{ page.title }} #

このページから読めます: [興奮・抑制均衡入門][tutorial]

まえがきに

> 理工学系の学部三年生くらいから読める, 理論神経科学のトピックの紹介を目指して書いています.  生物・神経科学や大学院レベルの数学・物理の知識は前提としない予定です.

って書いてますがあくまで予定です...  今のところまだちゃんと用語の解説をしていなかったりするので, 理論神経科学の基本的な知識が無いと常にググり続けないと読めないかもしれません.

内容は, ほぼ [van Vreeswijk & Sompolinsky (1998)][vanVreeswijk1998] "Chaotic balanced state in a model of cortical circuits" の解説です.  論文に書いてない部分を埋めたり, タイポを修正したり, ロジックを再構成して分かりやすくしたり (※個人的な意見です), 基礎的な部分も付録で導いたりしています.  技術的には漸近解析, マスター方程式, 平均場近似の応用例をまとめて学べる素材 (になり得るん) じゃないかと思います (この辺, 物理学科の外に居ると学ぶのに苦労するのでは?).

まだまだ書いてない部分も多いですが, それが埋まったら興奮・抑制均衡の最近の発展も紹介したいです.  例えば
[Renart et al. (2010)][Renart2010] "The asynchronous state in cortical circuits" とか
[Roxin et al. (2011)][Roxin2011] "On the Distribution of Firing Rates in Networks of Cortical Neurons"
とか.
ただ, いつ書けるかも分からないのでこの方面に興味があれば [Wolf et al. (2014)][Wolf2014] の素晴らしいレビューから始めるのをおすすめします.
まだチュートリアルでは書けていない, 実験やシミュレーションとの関係も載っています.

[tutorial]: http://balance-tutorial-ja.readthedocs.org
[vanVreeswijk1998]: http://dx.doi.org/10.1162/089976698300017214
[Renart2010]: http://dx.doi.org/10.1126/science.1179850
[Roxin2011]: http://dx.doi.org/10.1523/JNEUROSCI.1677-11.2011
[Wolf2014]: http://dx.doi.org/10.1016/j.conb.2014.01.017


このチュートリアル書いてみて実はあやふやだったり間違って理解したりしていた部分が分かって来たので, やっぱりロジックを自分の言葉で再構成するまでは理解したとは言えないのだなあと再確認しました.
あと, 用語を日本語に翻訳するのって難しい.
<small>なんど英語で書けば良かったと思ったことか...</small>
