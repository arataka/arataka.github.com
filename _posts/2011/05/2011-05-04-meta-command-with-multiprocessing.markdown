---
layout: post
title: パラメタの組み合わせを一気に走らせるメタコマンド (マルチプロセス対応)
---

# {{ page.title }} #

[メタコマンド実行スクリプトを Python で書いてみた - ny23の日記](http://d.hatena.ne.jp/ny23/20110416/p1)
に触発されて、使ってたスクリプトをちょっと強化したバージョン(`metarun.py`)を晒してみる。

## 使い方 ##

こんな感じでパラメタの全組み合わせ(直積)を走らせてくれる。
`--dry-run` (`-n`) オプションで実際に走らせるコマンドを表示してみる:

    % metarun.py --dry-run echo param-a=1,2 param-b=x,y
    echo --param-a 1 --param-b x
    echo --param-a 1 --param-b y
    echo --param-a 2 --param-b x
    echo --param-a 2 --param-b y

実際に走らせるとこんな感じ:

    % metarun.py echo param-a=1,2 param-b=x,y          
    echo --param-a 1 --param-b x
    --param-a 1 --param-b x
    echo --param-a 1 --param-b y
    --param-a 1 --param-b y
    echo --param-a 2 --param-b x
    --param-a 2 --param-b x
    echo --param-a 2 --param-b y
    --param-a 2 --param-b y

元のコマンドも表示される仕様でウザいけど気にしない（ぉ

`--format` (`-f`) オプションで、 `%(a)s` みたいな Python の文字列フォーマットが使える。
パラメタにあわせてデータを吐く場所を変える時とかに使う。

    metarun.py -nf 'python script.py -a %(a)s -b %(b)s --data=data/%(b)s%(a)s' a=1,2 b=x,y
    python script.py -a 1 -b x --data=data/x1
    python script.py -a 1 -b y --data=data/y1
    python script.py -a 2 -b x --data=data/x2
    python script.py -a 2 -b y --data=data/y2

複数プロセスを使うときは、 `--processes` (`-p`) オプションでプロセス数を指定。
普通に動かすと3秒かかるジョブが、

    % time tools/metarun.py -f 'sleep %(sec)s' sec=1,1,1
    sleep 1
    sleep 1
    sleep 1
    tools/metarun.py -f 'sleep %(sec)s' sec=1,1,1
    0.09s user 0.03s system 3% cpu 3.123 total

`-p 3` をつけると1秒で終わりました!:

    % time tools/metarun.py -f 'sleep %(sec)s' sec=1,1,1 -p 3
    sleep 1
    sleep 1
    sleep 1
    tools/metarun.py -f 'sleep %(sec)s' sec=1,1,1 -p 3
    0.10s user 0.07s system 14% cpu 1.143 total

この例だとジョブの数とプロセス数が等しいけど、ジョブの数が多い場合でも
[multiprocessing.Pool](http://docs.python.org/library/multiprocessing.html#multiprocessing.pool.multiprocessing.Pool)
が勝手に空いたプロセスでどんどんジョブを実行してくれるはず。
multiprocessing モジュールすばらしい!!

## `metarun.py` ##

<script src="https://gist.github.com/953918.js?file=metarun.py">
</script>
