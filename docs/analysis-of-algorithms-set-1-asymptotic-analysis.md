# 算法分析|集合 1(渐近分析)

> 原文:[https://www . geesforgeks . org/analysis-of-algorithms-set-1-渐近分析/](https://www.geeksforgeeks.org/analysis-of-algorithms-set-1-asymptotic-analysis/)

***为什么要进行性能分析？***
有很多重要的东西需要注意，比如用户友好性、模块化、安全性、可维护性等。为什么要担心性能？
这个问题的答案很简单，只有具备性能，我们才能拥有以上所有的东西。所以业绩就像货币一样，我们可以通过它来购买上面所有的东西。学习表演的另一个原因是——速度很有趣！
总结一下，业绩==规模。想象一下，一个文本编辑器可以加载 1000 页，但可以每分钟拼写检查 1 页，或者一个图像编辑器需要 1 个小时将图像向左旋转 90 度，或者……你明白了。如果一个软件功能不能应付用户需要执行的大规模任务，那就等于死了。

 ***给定一个任务的两个算法，我们如何找出哪一个更好？***
一种天真的方法是——实现两种算法，并在计算机上运行两个程序以获得不同的输入，然后看看哪一个花费的时间更少。这种算法分析方法存在很多问题。
1)对于某些输入，第一种算法可能比第二种算法性能更好。对于某些输入，second 表现更好。
2)对于某些输入，第一种算法在一台机器上表现更好，而第二种算法在另一台机器上对某些其他输入表现更好，这也是可能的。

[渐近分析](http://en.wikipedia.org/wiki/Asymptotic_analysis)是分析算法时处理上述问题的大思路。在渐近分析中，我们根据输入大小来评估算法的性能(我们不测量实际运行时间)。我们计算，一个算法所花费的时间(或空间)如何随着输入大小而增加。
例如，让我们考虑排序数组中的搜索问题(搜索给定的项目)。一种搜索方式是线性搜索(增长顺序是线性的)，另一种是二分搜索法搜索(增长顺序是对数的)。为了理解渐近分析如何在分析算法时解决上述问题，假设我们在快速计算机上运行线性搜索 **A** 和在慢速计算机上运行二分搜索法 **B** ，我们为两台计算机选择常数值，以便它准确地告诉我们给定机器执行搜索需要多长时间(秒)。假设 **A** 的常数为 0.2， **B** 的常数为 1000，这意味着 A 比 B 强大 5000 倍，对于输入数组大小 n 的小值，快速计算机可能需要更少的时间。但是，在输入数组大小达到一定值后，与线性搜索相比，二分搜索法肯定会开始花费更少的时间，即使二分搜索法是在一台慢速机器上运行的。原因是二分搜索法相对于输入规模的增长顺序是对数的，而线性搜索的增长顺序是线性的。因此，机器相关常数在输入大小达到一定值后总是可以忽略。
下面是这个例子的一些运行时间:
**线性搜索运行时间在 A** 上以秒为单位:0.2 * n
**二分搜索法运行时间在 B** 上以秒为单位:1000*log(n)

```
------------------------------------------------
|n      | Running time on A | Running time on B |
-------------------------------------------------
|10     | 2 sec             | ~ 1 h             |
-------------------------------------------------
|100    | 20 sec            | ~ 1.8 h           |
-------------------------------------------------
|10^6   | ~ 55.5 h          | ~ 5.5 h           |
-------------------------------------------------
|10^9   | ~ 6.3 years       | ~ 8.3 h           |
------------------------------------------------- 
```

***渐近分析总是有效吗？***
渐近分析并不完美，但这是分析算法的最佳方法。例如，假设在一台机器上有两种排序算法，分别花费 1000nLogn 和 2nLogn 的时间。这两种算法都是渐近相同的(增长顺序是 nLogn)。所以，用渐近分析，我们不能判断哪一个更好，因为我们忽略了渐近分析中的常数。
同样，在渐近分析中，我们总是讨论大于常数值的输入大小。有可能那些大的输入从来没有给过你的软件，一个渐进慢的算法总是在你的特定情况下表现得更好。所以，你最终可能会选择一个算法，这个算法对你的软件来说是渐进地慢，但是更快。

下一步–[算法分析|集合 2(最差、平均和最佳情况)](https://www.geeksforgeeks.org/analysis-of-algorithms-set-2-asymptotic-analysis/)

**参考文献:**
[麻省理工学院算法导论视频讲座 1](http://www.youtube.com/watch?v=JPyuH4qXLZ0)。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。