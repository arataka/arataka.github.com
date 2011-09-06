---
layout: post
title: hg out で待たされるのが苦痛なのでローカルにキャッシュしてくれる Mercurial 拡張を書いた
---

# {{ page.title }} #


## `hg out` の不満点 ##

Git より Mercurial のほうが好きだけど、 Git のほうが勝っていると
感じる点は、この `git status` の出力。

    % git status
    # On branch master
    # Your branch is ahead of 'origin/master' by 1 commit.
    #
    nothing to commit (working directory clean)

この出力を見れば、 push する必要があるかどうか一目瞭然で素晴らしい。
しかもこれ、今まで何を push したかローカルリポジトリが覚えているらしく、
origin/master にアクセスせずにこの出力を返してくれる。

Mercurial で同じ事をするには `hg out` を使うんだけど、これは
行き先のリポジトリにアクセスしているっぽいので非常にまたされる。
確かにそのほうが正確な結果が分かるかもしれないけど、てっとり
早く答えが知りたいときもあるじゃん!! という訳で書いた。


## インストール/使い方 ##

[tkf / hgcachedoutgoing / overview — Bitbucket
](https://bitbucket.org/tkf/hgcachedoutgoing/)
から
[`cout.py`
](https://bitbucket.org/tkf/hgcachedoutgoing/src/tip/cout.py)
をダウンロードして、

    [extensions]
    cout = /path/to/cout.py

を `~/.hgrc` に追加すると使えるはず。

適当なリポジトリに行って

    hg cout

と打つと、 push しなければいけない change set があるかどうか教えてくれる。
デフォルトの path がどこかのリモートマシーンの場合、一度目はそこにアクセス
するので遅いけど、二度目からはキャッシュを使うので、一瞬で結果が出るはず。
`hg push` する度にキャッシュを更新する hook を勝手に加える仕様なので、
一人で使うようのリポジトリとかだとほぼ `hg out` の代わりに使えるんじゃないで
しょうか。

初めての Mercurial 拡張なのと、リポジトリを見れば分かるけどテストが
皆無なのでバグが結構あるはず。

参考:

- [WritingExtensions - Mercurial
  ](http://mercurial.selenic.com/wiki/WritingExtensions)
- [MercurialApi - Mercurial
  ](http://mercurial.selenic.com/wiki/MercurialApi)
- [python - Mercurial Extension with no/default options - Stack Overflow
  ](http://stackoverflow.com/questions/4274517/mercurial-extension-with-no-default-options>)


## おまけ ##

以下のコードを適当な名前で保存して Mercurial リポジトリ内で実行すると、
Mercurial をハックするのに必要なモジュールをインポートしつつ、
Mercurial リポジトリのインスタンス(コマンド関数に与えられる引数)
もロードしてくれた状態で ipython が始まるのですこぶる便利。


Mercurialに限らず、スクリプトから ipython を実行するのっていろいろと応用
ききそう。


{% highlight python %}
import IPython

def get_ns(path='.'):
    import mercurial.hg as hg
    import mercurial.ui
    ui = mercurial.ui.ui()
    repo = hg.repository(ui, path=path)
    return {
        'hg': hg,
        'ui': ui,
        'repo': repo,
        }

embedshell = IPython.Shell.IPShellEmbed()
embedshell(local_ns=get_ns())
{% endhighlight %}


参考:
[How to embed an IPython shell in your application | Oh Brave New World!
](https://mybravenewworld.wordpress.com/2007/11/27/how-to-embed-an-ipython-shell-in-your-application/)
