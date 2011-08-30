---
layout: post
title: CA certificate が invalid だと Mercurial に怒られたけど、実は google code がリポジトリのリンクを変えていたのが原因だった。
---

# {{ page.title }} #

Mercurial には
[subrepository](http://mercurial.selenic.com/wiki/Subrepository)
といって、リポジトリをどんどんネストしていく便利な機能があるんだけど
それ関連でハマったことのメモ。

ついさっき、 google code に置いてあるリポジトリを subrepository
として持っているリポジトリで `hg push` とやると、

    pushing subrepo XXX to https://XXX.googlecode.com/hg
    abort: invalid certificate for XXX with fingerprint XX:XX:...(略)

と怒られてしまう問題に遭遇。


CA certificate 関連だと、この辺

- [CACertificates - Mercurial
  ](http://mercurial.selenic.com/wiki/CACertificates)
- [Getting Started - The Go Programming Language
  ](http://golang.org/doc/install.html)
- [tortoisehg / thg / issues / #63 - Cannot pull/push to https server
  with self-signed certificate --- Bitbucket
  ](https://bitbucket.org/tortoisehg/thg/issue/63/cannot-pull-push-to-https-server-with-self)

...を参考にすれば解決するかな、と思って

    hg push --insecure
    hg push --config web.cacerts=
    hg push --config web.cacerts=/etc/ssl/certs/ca-certificates.crt

とかを色々試していたけど上手くいかない。

これ、実は google code の URL が

    https://XXX.googlecode.com/hg

から

    https://code.google.com/p/XXX/

に変わっていたのが原因。なので、 `.hgsub` の

    XXX = https://XXX.googlecode.com/hg

の行を

    XXX = https://code.google.com/p/XXX/

に変更すればOK!

なんて分かりにくいエラーメッセージなんだ...
そして google code はいつの間に URL 変わったんだ...

という訳で、 CA certificate 関連で怒られていると思いきや、 URL
が変わっているだけ、ってことがあるので気をつけたいですね!!
