---
layout: post
title: icc でコンパイルした共有ライブラリって gcc でコンパイルされたプログラムから使えないのか!
---

# {{ page.title }} #

つまり普通の gcc でコンパイルされた Python からは、拡張モジュールとしても ctypes を通しても使えないってことかー!

... という訳で、[昨日悩んでいた問題](strange-ctypes-icc-segfault.html)は解決してしまった模様。
[numpy - Segfault occurs when my shared library is optimized by icc -O3 or -O2 and used via Python ctypes - Stack Overflow](http://stackoverflow.com/questions/5809337/segfault-occurs-when-my-shared-library-is-optimized-by-icc-o3-or-o2-and-used-vi)
で質問したらtalonmiesさんという方が瞬殺してくれました。ありがとう!
Stack Overflow 初めて使ったけど、良いシステムですね。

この問題はシミュレーションやってる人には結構深刻だよなあ。
解決するにはふたつ方法がある:

1. Python とか Numpy とか、関連するモジュールを全部 icc でビルドする。
2. シミュレーションプログラムを単体で動くように全部書き換えて Python とはパイプやファイル経由でデータをやりとりする。

どっちも厳しいな...
前者(1)はそもそもコンパイル通せるのかという問題と、コンパイラが違うバージョンのPythonをどう共存させるかって問題がある。
prefix オプションで違う場所にインストールする感じになるんだろうか。
あとその場合って virtualenv で管理出来るんだろうか。

後者(2)はそもそもその方法をやるのが嫌でPythonのC拡張やらctypesやらに手を出してきた経緯があるので、この便利さを知ったあとでそっちに戻るのは悲しい。
堅実な方法ではあるのだけど。


残る疑問は、Stack Overflowでもコメントに書いたけど以下の2点:

1. gcc とは関係なく実行出来るはずの pypy がなんで C のライブラリを読み込む ctypes を実装出来ているのか。
   ([PyPy’s ctypes implementation — PyPy v1.5-alpha documentation](http://codespeak.net/pypy/dist/pypy/doc/ctypes-implementation.html))
2. gcc とは関係なく実行出来るはずの Haskell のライブラリを Python の ctypes から読み込むことが出来るのか。
   ([PythonVsHaskell - PythonInfo Wiki](http://wiki.python.org/moin/PythonVsHaskell))

[ELF](http://ja.wikipedia.org/wiki/Executable_and_Linkable_Format) やら
[ABI](http://ja.wikipedia.org/wiki/Application_Binary_Interface) やら
知らなかったキーワードが出てきたので、もうちょっと調べる必要がありそうだ。
