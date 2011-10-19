---
layout: post
title: matplotlib を Flask から使う方法
---

# {{ page.title }} #

この辺を参考にしたら簡単にできました:

- [Matplotlib in a web application server
  — Howto — Matplotlib v1.0.1 documentation
  ](http://matplotlib.sourceforge.net/faq/howto_faq.html#matplotlib-in-a-web-application-server)
- [Upload a StringIO object with send_file | Flask (A Python Microframework)
  ](http://flask.pocoo.org/snippets/32/)
- [flask.send_file — API — Flask 0.8 documentation
  ](http://flask.pocoo.org/docs/api/#flask.send_file)


コード:

<script src="https://gist.github.com/1299670.js?file=mplonflask.py">
</script>

`/image.png` に直接アクセスすると画像が表示されるかわりにダウンロードされてしまうんだけど、なんでだろう。
Google chrome でも Firefox でもそうなってしまった。

簡単に画像がブラウザから見られるのは良いんだけど、プロファイルとってみると savefig に結構な時間を食われてしまっていたので、頻繁にグラフを書き換えるような場合はキャッシュディレクトリ作って普通に画像をファイルとして吐くのが良いと思う。

本当は
[Cache System
](http://werkzeug.pocoo.org/docs/contrib/cache/#cache-systems)
を使えれば良いんだろうけど、
[SimpleCache
](http://werkzeug.pocoo.org/docs/contrib/cache/#werkzeug.contrib.cache.SimpleCache)
は pickle 可能なやつしかキャッシュできないらしい...
