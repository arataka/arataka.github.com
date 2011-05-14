---
layout: post
title: MathJax を導入。
---

# {{ page.title }} #

MathJax は、
`\\( \exp(i \pi) = -1 \\)` と書くと \\( \exp(i \pi) = -1 \\) が、

    $$
      I(t) := \lim_{\Delta t \to 0} \frac{1}{\Delta t}
      \int_{t}^{t+\Delta t} J \sum_{f} \delta(s - t^{(f)}) ds
    $$

と書くと

$$
  I(t) := \lim_{\Delta t \to 0} \frac{1}{\Delta t}
  \int_{t}^{t+\Delta t} J \sum_{f} \delta(s - t^{(f)}) ds
$$

が表示されるライブラリー!!

(もうひとつの displayed math 用の表記 `\[...\]` は markdown
のマークアップとかぶって使えなかった。)

[インストール方法](http://www.mathjax.org/docs/1.1/platforms/index.html)
は
[恐ろしく簡単](https://github.com/arataka/arataka.github.com/commit/8d1767b48230e0d7beab36ccbfdb319601a050d1)
でした。

[大抵のブラウザ](http://www.mathjax.org/resources/browser-compatibility/)
で動いて、
[数式がスケール](http://www.mathjax.org/demos/scaling-math/)
して、
[コピペ](http://www.mathjax.org/demos/copy-and-paste/)
出来るらしいです。
すげー。
