--- 
layout: post
title: "\xE7\xAC\x94\xE8\xAE\xB0, lambda\xE6\xBC\x94\xE7\xAE\x97\xE5\x92\x8C\xE7\xBB\x84\xE5\x90\x88\xE5\xAD\x90"
tags: 
- FP
- lambda
- "\xE7\xAC\x94\xE8\xAE\xB0"
status: publish
type: post
published: true
meta: 
  _edit_last: "2"
---
看了几天wikipedia, 记一点自己的理解. 当然, 理解能力有限, 不一定正确.

还是关于lambda演算, 貌似church发明这东西是为了解决可计算性问题的判定, 也就是那个传说中的church-图灵论题. 同为形式系统(什么是形式系统...囧), 人们都说这东西跟图灵机的运算能力等价, 我觉得这种等价关系应该是在数学上, 而且是忽略中间的演算步骤的, 如1+1与1+34-78+96-51貌似就可以算是等价的.

lambda演算貌似有三个性质, 即alpha替换,  beta规约, eta替换, 在函数式语言编译器的优化中貌似有很多用处, 具体就不了解了. 那帮数学家大胡子貌似专好用希腊字母吓唬人, 数学里貌似从来就没有过命名规范! ... alpha替换貌似用来表示一个lambda表达式的等价关系, 如 λx.x+1与λy.y+1就是等价关系, 把x换成y, 依然还是那个lambda表达式;  beta规约貌似易理解些, 拿程序做类比的话貌似就是函数调用了, 如((λ.x.λy.x+y) 2)就可以规约成λy.2+y, 即把函数的参数替换成另一个表达式, 去掉一阶lambda;  eta替换貌似也是用来表示lambda表达式的等价关系, 如果 λx.f(x)==λx.g(x), 那么f==g.

一个lambda就是一个只有一个参数的函数, 要多个参数的函数就套多个阶的lambda, 像这样 λa.λb.a+b . 在(λb.a+b)中, a貌似就是自由变量, 不受这个lambda的约束. 由于(λb.a+b)这个函数中含有自由变量a, 所以这个函数只能在提供a这一自由变量的函数中存在而不能被自由传递或者调用. 而haskell curry大人发明的所谓组合子, 貌似就是没有自由变量的函数, 由于没有自由变量, 函数的自由传递就有了保证. 靠, map, filter, foldr, fst .... 你们全家都是组合子! 用有限数量的组合子就可以表示出特定范畴的所有运算, 也就是组合子语言, 传说中有个SK组合子语言, 只用S和K两个组合子就图灵完备了. map reduce filter貌似也可也看作是一门组合子语言, 单靠它们貌似就可以完成几乎所有的list操作. 呃, 还有那个一直以来让我闻之色变的monad, 貌似也是个组合子语言, 它里面只有>>=和return两个组合子...

貌似不需要把它们看得太复杂吧...概念都很简单...就像在学的高数和线代, 知道里面就那点东西, 可就是一个题都不会做...囧