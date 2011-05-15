---
layout: post
title: Docutils の table node を作る例
---

# {{ page.title }} #

Docutils は python のドキュメントを書くのに使われているのに、
そのドキュメント自体はあまり書かれてなくて
["Use the Source, Luke!" なんておっしゃる](http://docutils.sourceforge.net/docs/howto/rst-directives.html)
のでがんばってソースを読まないと使い方がよく分からない。

勝手に table を作ってくれるオレオレ directive を作りたいなーと思ったので書いてみた例です。
`my-table-2x2` という何の意味もない directive を作ってみました。

<script src="https://gist.github.com/973504.js">
</script>
