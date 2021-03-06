--- 
layout: post
title: "\xE6\x8A\xBD\xE8\xB1\xA1\xE4\xBB\xA3\xE6\x95\xB0\xE4\xB8\x8E\xE8\xAE\xA1\xE7\xAE\x97-Monoid"
tags: 
- Algbera
- Math
- Monoid
- "\xE7\xBF\xBB\xE8\xAF\x91"
status: publish
type: post
published: true
meta: 
  _edit_last: "2"
---
作者：Mark C. Chu-Carroll
翻译：Fleurer
原文：<a href="http://scienceblogs.com/goodmath/2008/02/abstract_algebra_and_computati.php">http://scienceblogs.com/goodmath/2008/02/abstract_algebra_and_computati.php</a>

在前两篇post，我们以范畴的角度观察了群论。范畴论给了我们一个全新的视角来理解对偶。与传统代数不同，范畴论的对偶是从groupoid中出现的，而群则被视为是带对偶的更简单的结构。

看其它的代数结构也是同样。比如环（rings），换个视角，也可以见到一个大不相同的环。

在看范畴论下的环之前，我们不妨先看个简单点的结构。在范畴中，环是通过monoid表示的。不过Monoid绝不仅仅只是环前面的开胃菜，它本身就是好东西。

它们的魅力在什么地方？首先，它们是范畴和代数之间的一座桥梁。我们知道，范畴中的groupoid（广群）使得群论无缝地归入了范畴论。Monoid也可以同样：它们也有范畴中的等价物。而且，Monoid还有地地道道的实际应用——你可以用Monoid表示计算。而且也许不广为人知，计算机科学中很多得力的基础工具其实都是Monoid。

我们先用代数的视角看下，呆会再换到范畴视角。在抽象代数中，Monoid正好跟复合函数的思想一致。开窍了吧，范畴论的基本思路就是复合函数的抽象化！

Monoid跟群类似，是一组支持二元运算的值的集合。Monoid更简单——它只要组合，不要逆元。我们令Monoid里面值的集合为M，二元运算为º，就有三条性质：

1.	封闭性（Closure）: ∀a,m∈M: aºb ∈ M
2.	单位元（Identity）: ∃ i∈M : ∀f∈M : iºf = fºi = f.
3.	结合律（Associativity）: ∀ a,b,c∈M: (aºb)ºc = aº(bºc).

这就是了。有这几条性质，想想函数和复合函数，套进去就满靠谱了。这对大多数函数都适用，于是所有的函数都成了对象，比如定义域和值域都是自然数的函数。封闭性要求两个简单完全函数复合的结果依然是简单完全函数；单位元可以是一个函数f(x)=x；交换律是交换表达式中元素的顺序，不影响最终结果。这都是复合函数天生的性质。

如果拿monoid像群一样，给它加一个操作又会怎样？答案对我们学计科的同学再熟悉不过了：有限自动机！

取一个monoid，(M,º)。我们可以在集合S上定义这monoid的一个操作，也就是：*:M×S→S，取M的一个值和S的一个值，得S的一个值。这个monoid操作显示了两条性质——都是来自monoid。

1.	Identity: ∀s∈S, i*s=s.
2.	Associativity: ∀a,b∈M, ∀s∈S: a*(b*s) = (aºb)*s.

这意味着什么？意味着我们给这个monoid加上了函数应用。这个monoid操作就是M中函数的应用。

这样，有了一个组可组合的函数，一个可以应用到函数的特定集合。可以得到什么？

一台自动机——也就是一种数学上的计算模型。

这个自动机是怎么出来的？

在这个monoid操作里，monoid的每个成员都是函数，也就是值到值的映射；组合符将这些函数链到一起。对自动机来说，monoid中的每个成员都是计算中的一个步骤，组合符将这些步骤连续起来。这还不是完整的计算——但已经靠一个简单的形式，前进了一大步。

多想想。还记得lambda演算？它就是一个表示计算的逻辑工具，里面除了函数什么都没有。想到了吧，我们刚刚只是重新发明了lambda演算的一部分，以抽象代数的思路。

在以后的post里面我会多讲些——不过我得先给你过上一遍，在范畴论里面这些东西都是什么样子——下一步往哪走，在范畴的大陆上清晰无比。
