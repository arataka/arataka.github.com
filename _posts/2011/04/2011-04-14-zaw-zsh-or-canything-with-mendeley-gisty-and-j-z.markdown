---
layout: post
title: Anything.elライクなCUIのzaw.zshやcanythingをMendeleyやgistyやz(もしくはj)と使う設定
---

# {{ page.title }} #

こんなの↓をやる設定です
(zaw.zsh で Mendely で管理している論文PDFを選んでいる様子):

[![zaw-mendeley.gif][fig_img_1]][fig_link_1]

[fig_img_1]: https://lh5.googleusercontent.com/_SAwQBQ7QF-E/TaXBwp6tnKI/AAAAAAAAAZw/D4aXfeWLKKg/s800/zaw-mendeley.gif
[fig_link_1]: https://picasaweb.google.com/lh/photo/j39yVxLpdSRnq_vXG17k8w?feat=embedwebsite

シェル環境で使える anything.el ライクな環境は
zaw.zsh と canything のふたつがある (もっとあるかも?)。

## zaw.zsh ##

- [zsh でも anything.el っぽいの - memo](http://u7fa9.org/memo/HEAD/archives/2011-02/2011-02-22_1.rst)
- [nakamuray/zaw - GitHub](https://github.com/nakamuray/zaw)
- [zshのanything.elやunite.vimっぽい機能を実現するzaw.zshの簡単な紹介と、予めsourceを指定したキーバインドを設定する方法 - kei_qメモ](http://d.hatena.ne.jp/kei_q/20110309/1299681144)
- [zaw.zshでgit show-branchの出力を眺めつつコミットを選択したい。 - hchbaw記](http://d.hatena.ne.jp/hchbaw/20110302/1299072457)

zsh の魔術(ウィジェット)なのでカスタマイズするのにとっつきにくかった。

設定は、ウィジェットを定義したファイルを source すればOK。
例えば、

    source path/to/zaw-mendeley.zsh

を `.zshrc` で `zaw.zsh` を source したあとの行に加える。


## canything ##

- [canything: CUIでAnything](http://filmlang.org/soft/canything)
- [keiji/canything - GitHub](https://github.com/keiji/canything)

パイプで受け渡しができて使いやすい

    <候補を出力するコマンド> | canything | <絞り込んだ結果を受け取るコマンド>`

という具合に使える。

ただ、空白をあけて複数の単語で絞り込み、っていう使い方が出来ないのが難点。

使い方は [canything: CUIでAnything](http://filmlang.org/soft/canything) にある。
例えば、 `.zshrc` で下に書いてある `ja` とか `gy` ようなシェル関数を定義すれば良い。


## Mendeley で管理しているPDFファイルを絞り込んで開く ##

[Mendeley](http://www.mendeley.com/)
は論文を管理してくれるソフトウェア+ウェブサービス。
ローカルにあるディレクトリにPDFを著者名や年や論文名を含めた
ファイル名で保存してくれるので、それを使って絞り込める。
一番上の画像でやってるのがそれ。

<script src="https://bitbucket.org/tkf/zaw-sources/src/tip/zaw-mendeley.zsh?embed=t">
</script>

→
[Bitbucket で `zaw-mendeley.zsh` のソースを見る](https://bitbucket.org/tkf/zaw-sources/src/tip/zaw-mendeley.zsh)


## gisty で管理しているリポジトリのワーキングディレクトリに一覧から選んで移動 ##

[gisty](https://github.com/swdyh/gisty)は、 [Gist](https://gist.github.com/)
の管理をしてくれるコマンド。
([gistコマンドよりちょっと便利なgisty - SWDYH](http://d.hatena.ne.jp/swdyh/20081207/1228655198))
`gist list` ってやればリポジトリ一覧を見せてくれるんだけど、
ディレクトリ名がランダムで分かりにくいのでanythingライクに絞り込めると便利。

<script src="https://bitbucket.org/tkf/zaw-sources/src/tip/zaw-gisty.zsh?embed=t">
</script>

→
[Bitbucket で `zaw-gisty.zsh` のソースを見る](https://bitbucket.org/tkf/zaw-sources/src/tip/zaw-gisty.zsh)

canything バージョン:

{% highlight sh %}
gy(){
    local choice="`gisty list | canything`"
    if [ $? -eq 0 ]
    then
	local gitdir=`echo $choice | cut -d":" -f1`
	local destpath=$GISTY_DIR/$gitdir
	if [ -n "$gitdir" -a -d "$destpath" ]
	then
	    cd $destpath
	fi
    fi
}
{% endhighlight %}


## z (もしくはj) を使って、よく使うディレクトリへ一覧から選んで移動 ##

z/j はよく行くディレクトリに一発でジャンプできるコマンド。
過去に行ったディレクトリを記録しててくれて、その頻度からジャンプ先を勝手に選んでくれる。
例えば、 `~/repos/arataka.github.com/` なるディレクトリでよく作業をしているなら、 `z arataka` とやれば一発でそこに行ける。
このコマンドにも anything ライクに使えるようにした。

ちなみに、 z/j には色々なバージョンがある(下)。
z が最新バージョンで、特別な設定なしでも zsh で使えるので、使うなら z が良いはず。

- [rupa/z - GitHub](https://github.com/rupa/z)
- [rupa/j2 - GitHub](https://github.com/rupa/j2)
- [rupa/j - GitHub](https://github.com/rupa/j/)

[zaw.zshでディレクトリスタックを選択したい。 - hchbaw記](http://d.hatena.ne.jp/hchbaw/20110224/zawzsh)
とやりたいことは似ているけど、ディレクトリスタックだとそのセッション以外で行ったディレクトリにアクセス出来ないのが難点。
z/j だと過去に行ったディレクトリならどこへでも行けるし、よく使うものほど上に来るので使いやすいと思う。

<script src="https://bitbucket.org/tkf/zaw-sources/src/tip/zaw-z.zsh?embed=t">
</script>

→
[Bitbucket で `zaw-z.zsh` のソースを見る](https://bitbucket.org/tkf/zaw-sources/src/tip/zaw-z.zsh)

canything バージョン:

{% highlight sh %}
ja(){
    local destpath=`j 2>&1 | sed -n -e '2,$p' | sed 's/^[0-9\\. ]*//' | tac | canything`
    if [ $? -eq 0 -a -n "$destpath" -a -d "$destpath" ]
    then
	cd $destpath
    fi
}
{% endhighlight %}
