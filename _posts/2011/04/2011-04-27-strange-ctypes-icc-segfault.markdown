---
layout: post
title: icc で最適化(-O2)かけた共有ライブラリを ctypes から使うと segfault してしまうことがあって困っている
---

# {{ page.title }} #

この不具合が出るコードは最適化なしの icc や、 gcc だと最適化していても、そんな不具合は出ないしユニットテストも通しているので、自分のコードにあるバグでは無い気がする。

ちなみに不具合起こすコードセットは
[tkf / ctypes_icc / source – Bitbucket](https://bitbucket.org/tkf/ctypes_icc/src)
で管理しています。

自分のコードのミスでは無いとは思っていても、糞みたいなミスのせいだと良いなあ、だれか指摘してくれないかなあ、とか淡い期待を抱いています←ぉぃ

## 悩みどころ ##

このコードは、今研究で使っているシミュレーション用のコードを icc で動くか試していたら出会ってしまったもの。
そのコードは ctypes を直接使わずに
[RailGun](http://tkf.bitbucket.org/railgun-doc-ja/index.html)
を使っていたので、RailGunなしでこの挙動を再現しようとして作ったのが↓のコードです。

悩みどころなのは、

- ユニットテストは通しているとはいえ、 segfault するようなコードで研究続けるのが凄く気持ち悪い。
- マシンによって segfault したりしなかったりして再現性が無いので python か intel にバグ報告するのも躊躇する。自分のマシンでしか起こらないような不具合って報告しても良いものか...。
- cypesを介さないでCだけでプログラムを書くとこの不具合が再現できないので、valgrindというツールを使おうとしたんだけどCPython側の処理がうじゃうじゃでてきてついていけない。
- 最適化かけないと起こらない不具合なのでデバッガ(idb/gdb)で見ても意味不明...

...などなど。
もっとCのスキルがあれば、あとは機械語読めたりすれば、頑張りようがあるんだろうか。


## ソース ##

以下の `strange.c` と `run.py` を準備して

    icc -O3  -Wall -std=c99 -shared strange.c -o libstrange.so
    python run.py

ってやると、 segfault を起こす (マシンもある)。

### `strange.c` ###

<script src="https://bitbucket.org/tkf/ctypes_icc/src/456006b3ceaa/strange.c?embed=t">
</script>

### `run.py` ###

<script src="https://bitbucket.org/tkf/ctypes_icc/src/456006b3ceaa/run.py?embed=t">
</script>


## `icc -O{2,3}` だと segfault ##

コンパイラとフラグを網羅的に変えて試すと、 `python run.py` の終了コードは

    gcc -O0: 0
    gcc -O1: 0
    gcc -O2: 0
    gcc -O3: 0
    icc -O0: 0
    icc -O1: 0
    icc -O2: 139
    icc -O3: 139

という感じなので、どうやら `icc -O{2,3}` のみで segfault が起こるみたい。


## マシン毎で違う挙動 ##

3つのPCでの挙動を調べたらそれぞれ違っていたので、比較のためにスペックと挙動をまとめてみるとこんな感じになった:

<table>
  <tr>
    <th></th>
    <th>デスクトップA</th>
    <th>ラップトップ</th>
    <th>デスクトップB</th>
  </tr>
  <tr>
    <th>このポストのコード</th>
    <td>不具合でる</td>
    <td>でない</td>
    <td>でない</td>
  </tr>
  <tr>
    <th>シミュレーション用のコード</th>
    <td>不具合でる</td>
    <td>不具合でる</td>
    <td>でない</td>
  </tr>
  <tr>
    <th><code>uname -m</code></th>
    <td>i868</td>
    <td>i868</td>
    <td>x86_64</td>
  </tr>
  <tr>
    <th>OS (<code>lsb_release -a</code>)</th>
    <td>Ubuntu 10.04.2 LTS</td>
    <td>Ubuntu 10.10</td>
    <td>Scientific Linux SL release 5.5 (Boron)</td>
  </tr>
  <tr>
    <th>icc version</th>
    <td>12.0.0 20101006</td>
    <td>12.0.3 20110309</td>
    <td>12.0.0 20101006</td>
  </tr>
  <tr>
    <th>Python version</th>
    <td>2.6.5</td>
    <td>2.6.6</td>
    <td>2.6.5</td>
  </tr>
  <tr>
    <th>Numpy version</th>
    <td>1.3.0</td>
    <td>1.3.0</td>
    <td>1.5.0b1</td>
  </tr>
</table>
