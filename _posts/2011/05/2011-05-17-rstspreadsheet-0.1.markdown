---
layout: post
title: Sphinx/Docutils で表計算をするための拡張 reStructuredSpreadsheet を書きました
---

# {{ page.title }} #

[Python Package Index : rstspreadsheet 0.1](http://pypi.python.org/pypi/rstspreadsheet/0.1)
にあります。
ここに書いてある例が出来ることのすべてです。
セルの値を計算する式は Python で書きます。
なので、 Python で出来ることは全てできます!!
ただしエラー処理をまったくやっていないので注意して使ってね☆(ぉ

(危なっかしいのでちゃんとエラー処理してくれ...とか要望あればコメントください。)

ちょとしたレポートを書く時に sphinx は便利で、
[matplotlib の plot directive](http://matplotlib.sourceforge.net/sampledoc/extensions.html#inserting-matplotlib-plots)
を使うとレポートのビルドとプロットを一緒にやってくれてすごく嬉しい。
ただ、理論式に色々と値をぶちこんでみるときに使えそうな拡張が無かった。
なので作りましたとさ。
