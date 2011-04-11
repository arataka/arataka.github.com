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
[fig_link_2]: http://www.flickr.com/photos/arataka/5610051566/

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


## datehist.py ##

何か変更あれば，最新版は
[tkf's gist: 913543 — Gist](https://gist.github.com/913543)
にあげときます．

{% highlight python %}
#!/usr/bin/env python

"""
Plot histogram from list of dates

Usage
=====
Feed newline separated unix time via STDIN.

Ex.1: plot repository activity::

    hg log --template '{date}\\n' | datehist.py -t `hg root`
    git log --format='%at' | datehist.py -t `git rev-parse --show-toplevel`

"""

import sys
import datetime

import numpy
from matplotlib import pyplot
from matplotlib.dates import YearLocator, MonthLocator, DateFormatter
from matplotlib.dates import epoch2num, date2num


def num_now():
    """
    Return the current date in matplotlib representation
    """
    return date2num(datetime.datetime.now())


def get_limit(past):
    """
    Get the date `past` time ago as the matplotlib representation
    """
    return num_now() - float(past) * 365


def read_dates(limit, stream=sys.stdin):
    """
    Read newline-separated unix time from stream
    """
    dates = []
    for line in stream:
        num = epoch2num(float(line.strip()))
        dates.append(num)
        if num < limit:
            break
    stream.close()
    return dates


def plot_datehist(dates, bins, title=None):
    (hist, bin_edges) = numpy.histogram(dates, bins)
    width = bin_edges[1] - bin_edges[0]

    fig = pyplot.figure()
    ax = fig.add_subplot(111)
    ax.bar(bin_edges[:-1], hist / width, width=width)
    ax.set_xlim(bin_edges[0], num_now())
    ax.set_ylabel('Events [1/day]')
    if title:
        ax.set_title(title)

    # set x-ticks in date
    # see: http://matplotlib.sourceforge.net/examples/api/date_demo.html
    ax.xaxis.set_major_locator(YearLocator())
    ax.xaxis.set_major_formatter(DateFormatter('%Y'))
    ax.xaxis.set_minor_locator(MonthLocator())
    # format the coords message box
    ax.format_xdata = DateFormatter('%Y-%m-%d')
    ax.grid(True)

    fig.autofmt_xdate()
    return fig


def main():
    from optparse import OptionParser
    parser = OptionParser(usage='PRINT_UNIX_TIME | %prog [options]')
    parser.add_option("-p", "--past", default="3",
                      help="how many years to plot histogram. (default: 3)")
    parser.add_option("-o", "--out", default=None,
                      help="output file. open gui if not specified.")
    parser.add_option("-b", "--bins", default=50, type=int,
                      help="number of bins for histogram. (default: 50)")
    parser.add_option("-t", "--title")
    parser.add_option("-d", "--doc", default=False, action="store_true",
                      help="print document")
    (opts, args) = parser.parse_args()

    if opts.doc:
        print __doc__
        return

    dates = read_dates(get_limit(opts.past))
    fig = plot_datehist(dates, opts.bins, title=opts.title)

    if opts.out:
        fig.savefig(opts.out)
    else:
        pyplot.show()


if __name__ == '__main__':
    main()
{% endhighlight %}
