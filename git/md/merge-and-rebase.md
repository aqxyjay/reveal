<!-- .element: class="fragment visible"--> 

# Merging
# V.S.
# Rebasing

---

### 抛个问题

大家和在合入代码的时候有没有遇到过...

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/f1016851.png)

--

### 再抛个问题

大家在审核代码的时候有没有到过...

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/c6db36e5.png)

--

### 还有一个...

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/4f1f5a75.png)
<!-- .element: style="height: 550px;"--> 

--

### 最后一个......

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/58345abd.png)

---

## 现在开始正题

主角a 和 主角b

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/eb4f2803.png)

--

配角卢岸卓和配角田野都在修改master分支

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/ad288cd4.png)

岸卓快了一步，Push到了master

--

从此，master和田野产生了差异

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/15a0a294.png)

就这样，master和田野的故事开始了...

---

## Merging

田野要把自己的修改Push到master

--

第一步要从master更新

```git
git pull
```

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/02db830e.png)
<!-- .element: class="fragment visible"-->

--

第二步要Push

```git
git push
```

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/9df32534.png)
<!-- .element: class="fragment visible" style="height: 500px;"--> 

--

这样，田野就把自己的修改Push到master了

但是有人问了
<!-- .element: class="fragment visible"-->

你标题是Merging，怎么在将Pull
<!-- .element: class="fragment visible"-->

```git
git pull
```
<!-- .element: class="fragment visible"-->

等价于
<!-- .element: class="fragment visible"--> 

```git
git fetch
git merge
```
<!-- .element: class="fragment visible"--> 

---

## Rebasing

田野要把自己的修改Push到master

--

第一步要从master更新，我们换个方式

1. 将master抓取到本地
```git
git fetch
```

2. 将本地修改变基
```git
git rebase
```

--

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/72b51208.png)
<!-- .element: style="height: 550px;"--> 

--

第二步要Push

```git
git push
```

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/83d9dde5.png)
<!-- .element: class="fragment visible"-->

--

Rebase的原理是这样的

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/d031f821.png)
<!-- .element: class="fragment visible" style="height: 500px;"-->

---

## 总结

在主角a、b和配角岸卓、田野的表演下，我们已经清楚Merging和Rebasing的优缺点了

 - Merging会导致额外的一次Merge提交记录
 - Rebasing会在已经提交得记录上进行补充提交，不会有额外的记录
 
所以，以后大家多用Rebasing。

P.S. 再有Merge记录的提交，审核时不会再合入。

--

### 如何用TortoiseGit来Rebase

![](https://img.zhangchunxin.com/reveal/git/merge-and-rebase/rebase.gif)

---

### 附录

 - [Git权威指南 - 蒋欣 - iSource](http://isource-pages.huawei.com/iSource/gotgit/index.html)
 - [Git Merge vs. Rebase: What’s the Diff? - Michael Aranda - HackerNoon](https://hackernoon.com/git-merge-vs-rebase-whats-the-diff-76413c117333)

