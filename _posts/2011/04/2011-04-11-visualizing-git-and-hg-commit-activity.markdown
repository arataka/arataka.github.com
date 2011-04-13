---
layout: post
title: MercurialやGitのコミット頻度などを可視化するPythonスクリプトを書いてみた
---

# {{ page.title }} #

いくつかのオープンソースなソフトがあった時は，開発が活発なほうを選びたい．
[Google Code](http://code.google.com/) とかだと activity を出してくれてりするけど，

1. 同じ activity の測り方で比較したい．

2. そもそも activity 表示してくれてないサイトだと比較できない．

3. 今は盛り上がってるよ，じゃなくて継続的に盛り上がってるか知りたい．

などなど問題があるので，自力でやってみた．

その出力が↓にあるNumpyのリポジトリの activity (一日あたりのコミット数)の推移．
2006年あたりから盛り上がってるねーということが分かる．

[![repo-act-numpy by takafumi_a, on Flickr][fig_img_1]][fig_link_1]

[fig_img_1]: http://farm6.static.flickr.com/5303/5610051566_08c5ca8a96.jpg
[fig_link_1]: http://www.flickr.com/photos/arataka/5610051566/

ちなみに時刻が並んでいるデータ(点過程って言えば正確かな?)だったら何でもパイプ経由で食わせられるので，他の用途にも使えるはず．

今回使うスクリプト(`datehist.py`)は
[tkf's gist: 913543 — Gist](https://gist.github.com/913543)
からダウンロード出来ます．
このポストの一番下にも載っけてあります．Numpyとmatplotlibが必要です．

## 使い方 ##

Activity を測りたいリポジトリのワーキングディレクトリで，以下を実行．
MercurialやGit以外の方法は使ってないので知らない...:

{% highlight sh %}
hg log --template '{date}\\n' | datehist.py
git log --format='%at' | datehist.py
{% endhighlight %}

`datehist.py` に食わす標準入力 (`hg log` や `git log` の出力)はこんな感じ．
コミットがあった時間の unix time を一行ごとにひたすら吐いてくれる．:

    1298586880
    1298516219
    1298426531
    1298426393
    1298418897
    1298407083
    1298387222
    1298387170
    1295910432
    (...以下略)

引数 `-t` (省略可)で出力グラフのタイトルを与えられるので，ワーキングディレクトリのあるフルパスをタイトルに使いたければ

{% highlight sh %}
hg log --template '{date}\\n' | datehist.py -t `hg root`
git log --format='%at' | datehist.py -t `git rev-parse --show-toplevel`
{% endhighlight %}

でOK.


## 応用例: 分散バグ管理システムはどれが元気あるかを調べてみた ##

比較したのは，次の4つのプロジェクト

1. [b](http://www.digitalgemstones.com/projects/b/) (Mercurialのプラグイン)
2. [Bugs Everywhere](http://bugseverywhere.org/be/show/HomePage) (Python製)
3. [Ditz](http://ditz.rubyforge.org/) (Ruby製)
4. [pitz](http://pitz.tplus1.com/) (DitzをPythonで書き直し)

[![screenshot-2011-04-04-185810 by takafumi_a, on Flickr][fig_img_2]][fig_link_2]

[fig_img_2]: http://farm6.static.flickr.com/5144/5588561616_2ae2ee5c2f.jpg
[fig_link_2]: http://www.flickr.com/photos/arataka/5588561616/

結論: どれもあんまり元気ないなあ...

とりあえず，もろもろの理由から b を使ってみることにした．


## `datehist.py` の 改善点 ##

この方法だと，いちいちローカルに clone 作る必要があるのが難点．
リモートのリポジトリのログを見る方法って探せばありそう(←探せ)だし，
そうすればwebアプリ的な感じにも出きるよね．
誰かやってくれないかなあ（ぉぃ

* 追記 (2011-04-12)

  - Mercurialだと無理みたい:  
    [4.23. How can I do a "hg log" of a remote repository? - FAQ - Mercurial](http://mercurial.selenic.com/wiki/FAQ#FAQ.2BAC8-CommonProblems.How_can_I_do_a_.22hg_log.22_of_a_remote_repository.3F)
  - Gitも無理そう:  
    [git - git log of remote repositories.](http://git.661346.n2.nabble.com/git-log-of-remote-repositories-td4899042.html)


## datehist.py ##

何か変更あれば，最新版は
[tkf's gist: 913543 — Gist](https://gist.github.com/913543)
にあげときます．

<script src="https://gist.github.com/913543.js?file=datehist.py"></script>
