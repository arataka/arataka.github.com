---
layout: post
title: 単純固有値ってなんだっけ
---

# {{ page.title }} #

最近とある文献を読んでいたら **単純固有値** という言葉が出てきて、
「ああ縮退してない固有値って意味なんだろうな」と思いつつ、
そして文脈からもそれっぽいんだけど、不安なのでちょっとググってみた。


[Online Applied Analysis with MATHEMATICA
](http://www.sci.u-toyama.ac.jp/~fkubo/mathemat/math0024.htm>):

> 得られた固有値が互いに異なることを確認せよ． 即ち，固有値は
> **単純固有値** しかない．

[非対称行列の左固有ベクトルと右固有ベクトルの直交性について - Yahoo!知恵袋
](http://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q1336943908>):

> a) 固有値が半単純な場合（重複度と同じだけ固有ベクトルが採れる場合）
>    \[...\]
> b) 固有値が単純でも半単純でもない場合（重複度と同じだけ固有ベクトル
>    が採れない場合）

[固有値についてーページランクベクトルとペロン・フロベニウスの定理
](http://www.geocities.jp/existenzueda/eigenvalue.htm):

> 一般に、ペロン・フロベニウスの定理は、次の内容とされています。
> 非負の行列Ａが、既約であれば、 \[...\]
> ② 絶対値最大の固有値は、Ａの固有方程式の単純根である。
> （ｒは、 **単純固有値** である。）

あんまり情報ねぇ... 「○○の時、固有値を単純といいます」的な
定義がどこかに載っていることを期待していたのに。
ググってすぐ情報が出てこないとちょっとずつ不安になってくる。
←情報化社会の弊害。


英語訳は 単純 = simple であってるよな? と思って調べたけど、
これまた情報が少ない。一応、

[J-GLOBAL - Analysis of dynamica・・・ 【文献】
](http://jglobal.jst.go.jp/public/20090422/200902050372803443):

> Analysis of dynamical bifurcations in the case of **nonsimple** eigenvalues.
> \[...\]
> 固有値が **単純でない** 場合の動的２分岐の解析

というのを見つけたので多分当たっている。


"simple eigenvalue" の定義は簡単に見つかった:

[Pauls Online Notes : Linear Algebra - Eigenvalues and Eigenvectors
](http://tutorial.math.lamar.edu/Classes/LinAlg/EVals_Evects.aspx):

> **Definition 3**: Suppose \\(A\\) is an \\(n \times n\\)
> matrix and that \\(\lambda_1, \lambda_2, ..., \lambda_n\\) is
> the complete list of all the eigenvalues of \\(A\\) including
> repeats.  If \\(\lambda\\) occurs exactly once in this list then
> we call a **simple eigenvalue**.  If \\(\lambda\\) occurs
> \\(k \ge 2\\) times in the list we say that has **multiplicity** of
> \\(k\\).

... という訳で、 **単純固有値** = **simple eigenvalue** =
**縮退していない固有値** でOKな模様。


<strike>洋書で勉強してると、
たまーに日本語の文献読んだ時に用語分からなくてつれーわー</strike>

嘘ですぅぅぅぅ勉強不足ですぅぅぅひぃぃぃぃ。
