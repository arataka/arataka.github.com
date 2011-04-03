---
layout: post
title: google-diff-match-patchを使って文章の差分を単語単位でとるCLIプログラムを書いた
---

# {{ page.title }} #

[![oogle-diff-match-patch by takafumi_a, on Flickr][fig_img]][fig_link]

[fig_img]: http://farm6.static.flickr.com/5026/5584640439_08e2ded198_z.jpg
[fig_link]: http://www.flickr.com/photos/arataka/5584640439/

...と言っても実は
[google-diff-match-patch](http://code.google.com/p/google-diff-match-patch/)
っていうライブラリを使えば簡単にできるって話で、そのデモサイト:
[Diff, Match and Patch: Demo of Diff](http://neil.fraser.name/software/diff_match_patch/svn/trunk/demos/demo_diff.html)
と同じことが出来るCLIを書いただけ。要Python。

Python無かったりインストール面倒な人は、デモサイトの出力結果をHTMLメールにコピペして使えば良いんじゃないかな。

あと、自分で確認できれば良い時は wdiff っていうコマンドを使えば単語単位で diff がとれる。`--terminal` オプションをつければ見易くなるのでおすすめ。Ubuntuなら `sudo apt-get install wdiff wdiff-doc` でインストール出来る。

## google-diff-match-patch をダウンロードしてインストール ##

{% highlight sh %}
wget http://google-diff-match-patch.googlecode.com/files/diff_match_patch_20110217.zip
unzip diff_match_patch_20110217.zip
cp diff_match_patch_20110217/python/diff_match_patch.py ~/pymodules/ #任意
{% endhighlight %}

`~/pymodules/` は `$PYTHONPATH` に設定されている適当なディレクトリ。
面倒なら次にダウンロードするスクリプト(`gdmp.py`)と同じディレクトリに置けばOK。

## 文章の差分をとる方法 ##

[Command line tool for google-diff-match-patch — Gist](https://gist.github.com/899325)
をダウンロードして使う。これが、今回書いたやつ。

{% highlight sh %}
wget https://gist.github.com/raw/899325/gdmp.py
python gdmp.py FILE1 FILE2 -o diff.html
{% endhighlight %}

これでdiff.htmlに差分が出力されるので、ブラウザで開いてHTMLメールに張り付けるなりファイルをそのままメールするなりすれば良い。

LaTeXファイルを扱う時は、 `detex` でLaTeXコマンドを消してから差分をとれば良い。zshなら、

{% highlight sh %}
python gdmp.py <(detex -l FILE1.tex) <(detex -l FILE2.tex) -o diff.html
{% endhighlight %}

でOK。

論文とかを人に添削してもらう時に、どこを変更したかを分かりやすく伝えたい時が
ある。ワードなり使ってれば良いんだろうけど、LaTeXや普通のテキストファイルを
扱ってくれるプログラムが見つからなかったので書いてみた、という話でした。
