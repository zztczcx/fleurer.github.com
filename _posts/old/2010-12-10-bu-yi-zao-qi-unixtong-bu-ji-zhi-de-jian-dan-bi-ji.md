--- 
layout: post
title: "\xE8\xA1\xA5\xE9\x81\x97 - \xE6\x97\xA9\xE6\x9C\x9Funix\xE5\x90\x8C\xE6\xAD\xA5\xE6\x9C\xBA\xE5\x88\xB6\xE7\x9A\x84\xE7\xAE\x80\xE5\x8D\x95\xE7\xAC\x94\xE8\xAE\xB0"
tags: 
- Kernel
- Unix
- "\xE7\xAC\x94\xE8\xAE\xB0"
status: publish
type: post
published: true
meta: 
  _wp_old_slug: ""
  _edit_last: "2"
---
Unix的历史就像杨振宁的家谱一样，是个图。不管是大公司的程序员、学术界的老教授还是开源hacker，意识形态的不同并没有妨碍他们相互抄袭并为之进一步发展。仅仅把linux的成功归功于开源、仿佛一切统统来自新信仰者发起的一场革命(revolution)的看法自是不恰当的。若忽略无数人在背后所花费的时间，而把功劳统统归功于出台出面的英雄，那历史就不成为历史，我们现在所拥有的一切也皆出于偶然。平铺直叙今天linux中的各种机制策略只能一览其天才精巧，可是若要感受背后无数人们的心血付出或者解惑“为什么这样”，Unix背后几十年的演变（evolution）历程就不能不有所了解。

上一篇post里说到早期Unix的同步机制，可是漏了些东西，在这里补一下。

漏掉了早期Unix的同步机制是基于这样的假设，这点很重要：

 * 只有一个CPU
 * 内核是非抢占的

于是

 * 内核操作某对象时不会被其他进程打断
 * 但期间可能会发生中断

从而允许把同步机制做的很简单。
 
还忽略了一个地方，那就是sleep+X_LOCK/X_WANTE机制仅仅是用在“比较长时间”的同步中。比如说一个buffer等待读取一个磁盘块，可能得分两次进入内核才能得到处理。这里需要注意的地方就是sleep/wakeup一定会引起进程切换，很吃性能。在这一点上，大约跟信号量差不多。

拜前面简单的假设所赐，“短时间”内的同步通过简单开关中断即可形成一个临界区，比如：

<pre lang="c">
bflush(dev)
{
	register struct buf *bp;

loop:
	spl6(); //关中断，相当于x86下的cli()
	for (bp = bfreelist.av_forw; bp != &bfreelist; bp = bp->av_forw) {
		if (bp->b_flags&B_DELWRI && (dev == NODEV||dev==bp->b_dev)) {
			bp->b_flags =| B_ASYNC;
			notavail(bp);
			bwrite(bp);
			goto loop;
		}
	}
	spl0(); //开中断，相当于sti()
}
</pre>

这里开关中断的应用，差不多就相当于自旋锁(spin lock，俗称simple lock)。但是更加简单，也没有纠结死锁的必要。

== Drawbacks

机制做的简单，往往正是因为事先对外部情况做了假设。问题当然不少：
 * 扩展性差。有多少种对象就得写出来多少遍类似的同步代码，没有形成某种具体的锁。早期Unix代码之短令人印象深刻，但是不能无视这个事实：后来（仅仅是几年间）Unix代码的爆炸式增长。
 * 伸缩性不好，一放到多核下边就瞬间杯具。

后来Unix移植到了多核心的机器上，这样的机制即已不再适用，很快就被信号量和自旋锁所取代了。至于信号量和自旋锁带来的问题还不是很明白，有空再写好了。
