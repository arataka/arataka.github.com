---
layout: post
title: GitHubのページを開くためのコマンド
---

# {{ page.title }} #

Gitのワーキングディレクトリに居る時にGitHubのプロジェクトページを開くためのコマンドです。

{% highlight sh %}
gith() {
    local P="$(git remote -v 2>/dev/null | grep 'github.com' | head -1)"
    local URL="https://"$(echo $P | sed -r \
        -e 's|.*[\t ](.*)[\t ].*|\1|' -e 's|\.git$||' \
        -e 's|https?://||' -e 's|:|/|' -e 's|^[a-z]*@||')
    [[ -n $URL ]] && gnome-open $URL || echo "No GitHub path found!"
}
{% endhighlight %}

Ubuntu 上の zsh で動きます． bash でも動くと思いますが、未確認。
`gnome-open` の部分を変更すれば、Macとかでも動くはず。

元ネタ: [Open BitBucket from Bash / hg tip](http://hgtip.com/tips/advanced/2009-10-08-open-bitbucket-from-bash/)
