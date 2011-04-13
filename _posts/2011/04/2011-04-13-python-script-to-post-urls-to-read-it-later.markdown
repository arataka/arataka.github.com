---
layout: post
title: Read It LaterにURLをまとめてポストするPythonスクリプト
---

# {{ page.title }} #

[Read It Later](http://readitlaterlist.com/)
は、AndroidやiPhoneから色々なページをオフラインで読めるようにしてくれる
サービス/アプリ。
まとめてタグ付けしたり投稿したりが面倒なのでコマンドラインから投稿できる
スクリプト書きましたよ!

## 準備 ##

1. [tkf's gist: 915752 — Gist](https://gist.github.com/915752)
   から `ril.py` を落とす。
2. [Surgo / RIL / overview – Bitbucket](https://bitbucket.org/Surgo/ril/)
   をインストールする。
   `readitlater/`ディレクトリをPythonがモジュールとして認識できるところにおく。
   面倒だったら、 `ril.py` と同じディレクトリにおく。
3. [Read It Later: Developer API: Signup](http://readitlaterlist.com/api/signup/)
   で API Key を取る。

## 使い方 ##

    ril.py -a <API_KEY> -u <USER_NAME> -p <PASS_WORD> --tags <TAG_1,TAG_2,..> <URL_FILE>

もし、 `<API_KEY>`, `<USER_NAME>`, `<PASS_WORD>` がなければプロンプト
が出てくるのでそこから入力。
パスワードはコマンドラインから入れないほうがいいかも。

`<URL_FILE>` は、一行ごとにURLが入っているテキスト:

    https://gist.github.com/915752
    https://bitbucket.org/Surgo/ril/
    http://arataka.github.com/2011/04/13/python-script-to-post-urls-to-read-it-later.html

URLのあとにスペースを空ければタイトルも入れられる:

    https://gist.github.com/915752 tkf's gist: 915752 — Gist
    https://bitbucket.org/Surgo/ril/ Surgo / RIL / overview – Bitbucket
    http://arataka.github.com/2011/04/13/python-script-to-post-urls-to-read-it-later.html Read It LaterにURLをまとめてポストするPythonスクリプト

タイトルは入れないと Read It Later にアクセスしたときにURLがタイトル代わりに
表示されちゃうので入れておいたほうが良い。

`<URL_FILE>` を省略すると標準入力から読み込みます。
その他のオプションについては `ril.py --help` を見てね!

## `ril.py` の中身 ##

<script src="https://gist.github.com/915752.js?file=ril.py">
</script>
