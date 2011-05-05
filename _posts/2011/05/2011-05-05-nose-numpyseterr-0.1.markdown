---
layout: post
title: Numpy の浮動小数点エラーの扱い方を選ぶための nose プラグイン
---

# {{ page.title }} #

折角シミュレーション用プログラムのテストを書いても浮動小数点エラーを見逃してしまっていたら悲しいですよね。
というわけで、書きました:
[Python Package Index : nose-numpyseterr](http://pypi.python.org/pypi/nose-numpyseterr)

インストール方法:

    easy_install nose-numpyseterr  # または、
    pip install nose-numpyseterr


## 使い方 ##

Numpy の浮動小数点エラーの取扱いは
[numpy.seterr --- NumPy Manual (DRAFT)](http://docs.scipy.org/doc/numpy/reference/generated/numpy.seterr.html)
を見てください。

多分デフォルトでは `'ignore'` か `'print'` です。
手元の Ubuntu だと `all='ignore'` で、野良ビルドした numpy だと `under` だけ `'ignore'` で他は `'print'` でした(何で違うんだろ??)。
浮動小数点エラーの取扱いが `'ignore'` だと、例えば

{% highlight python %}
import numpy

def test_divide():
    1.0 / numpy.array([0])
{% endhighlight %}

を `test_divide.py` という名前で保存して テストすると

    % nosetests test_divide.py
    .
    ----------------------------------------------------------------------
    Ran 1 test in 0.001s

    OK

のように何事もなかったかのようにパスするはずです。


テストはパスして欲しいけど、浮動小数点エラーが起こったかどうかは確認したい場合は、 `--npe-all=print` をつけます:

    % nosetests --npe-all=print test_divide.py
    Warning: divide by zero encountered in divide
    .
    ----------------------------------------------------------------------
    Ran 1 test in 0.001s

    OK

もうちょい詳しい情報が知りたいなら、 `--npe-all=warn` を使います。

    nosetests --npe-all=warn test_divide.py
    test_divide.py:4: RuntimeWarning: divide by zero encountered in divide
      1.0 / numpy.array([0])
    .
    ----------------------------------------------------------------------
    Ran 1 test in 0.001s

    OK

ただ、同じ場所のエラーは一度しか表示されません。


Python のエラーとして扱って欲しい場合は `--npe-all=raise` を使います。

    % nosetests --npe-all=raise test_divide.py
    E
    ======================================================================
    ERROR: test_divide.test_divide
    ----------------------------------------------------------------------
    Traceback (most recent call last):
      File ".../lib/python2.6/site-packages/nose/case.py", line 186, in runTest
        self.test(*self.arg)
      File ".../test_divide.py", line 4, in test_divide
        1.0 / numpy.array([0])
    FloatingPointError: divide by zero encountered in divide

    ----------------------------------------------------------------------
    Ran 1 test in 0.017s

    FAILED (errors=1)

あとは
[nose-pudb](http://pypi.python.org/pypi/nose-pudb/)
で
[pudb](http://pypi.python.org/pypi/pudb)
に落としてデバッグすれば良いんじゃないでしょうか。


## 中身 ##

驚くほどシンプルですw

<script src="https://bitbucket.org/tkf/nose-numpyseterr/src/e4981340d1b5/nosenumpyseterr.py?embed=t">
</script>


## 落とし穴 ##

単純な実装なので、テストコードの中で `numpy.seterr` を使っていると多分上手くうごきません。
もうちょっと書き足せばどうにかなるはずなので、直してよ!って人がいたらコメント等で連絡下さい。
