# Adobe 面试体验|第 40 集(MTS-1 的校内)

> 原文:[https://www . geesforgeks . org/adobe-面试-体验-设置-校园 40/](https://www.geeksforgeeks.org/adobe-interview-experience-set-40-on-campus/)

**线上测试:**
编码:时间:90 分钟
共有三道编码题如下:

1.  一个男人从他的房子开始拿着几个平底锅蛋糕。现在他在到家之前会去 K 个地方。在每个地方，他可以买一个蛋糕，卖一个蛋糕或者什么都不做。但是他必须在到家之前卖掉 L 蛋糕。找到他旅途中任何时候能吃的最大蛋糕数量。n、K、L 作为输入给出
    例:对于 5 3 1，输出:7
2.  确切的问题我不记得了。你必须找到数组中最大的连续子数组。基本上是一个关于卡丹算法
    **解** : [GeeksforGeeks Link](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/) 的问题
3.  有一段文字。有一个模式。该模式包含一个*符号，可以用 0 个或更多字母(任何字母)替换。例如，如果 aa*b 中的模式，aaab、aab、aaccb 等都是有效的模式。你必须找到该模式在文本中出现的次数。

MCQ: 50 分钟
有 45 道基于逻辑推理、数据解读和初等数学的题。一个建议是，从最后开始，他们比一开始容易得多。

大约有 16 名学生被选中参加面试。

 **第一轮**

1.  他问我排序算法。然后他问我快速排序和合并排序有什么区别，什么时候用什么？
    我告诉他 merge sort 是稳定的，而 quick sort 具有 o(n^2 的最坏情况复杂性)但是在 quick sort 中，我们不需要合并已排序的数组。对于数组，我们使用快速排序，对于链表，我们使用合并排序
2.  编写包含浮动的链表合并排序的代码
    **解决方案** : [GeeksforGeeks Link](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)
3.  然后，他告诉我通过交换节点中的数据在链表中进行冒泡排序，并问除了复杂性之外，这里还有什么问题？
    我被告知，查找列表通常包含大量数据，因此交换数据会导致相当大的开销并降低性能。他似乎对这个答案很满意。
4.  像 5.7 这样的浮点如何在 CPU 内部表示？
    我不得不说说 IEEE 的符号。我不记得那些，所以无法回答。
5.  关于操作系统、线程、进程、它们的区别、分页等问题很少
6.  您必须编写一个通用的比较函数来进行排序。例如，假设有一个学生类包含主题 X、Y、z 的标记。您必须编写一个比较函数，用于根据用户希望的任何字段进行排序。
    提示:使用函数指针
7.  给出了两个数字，你必须在不使用*运算符的情况下将它们相乘，并且还必须给出这样做所需的最小加法数。
    **解决方案** : [极客论坛链接](https://www.geeksforgeeks.org/multiply-two-numbers-without-using-multiply-division-bitwise-operators-and-no-loops/)

 **第二轮**
面试官又看了看我的简历，告诉我做了不少项目。但是我的项目没有问题。

1.  设计一个缓存来存储任何类型的数据。
    由于我们不知道要存储什么数据，所以必须返回 void 指针。现在首先我用一个数组来实现。然后我用 LRU 来替换页面。为了跟踪最近最少使用的元素，我使用了堆。我被告知要进一步优化它。所以首先用堆来表示缓存，然后最后用存储在散列表中的节点地址来表示双向链表。还为缓存和替换编写了设置和获取函数的代码。
    面试官帮了大忙，把我推向了正确的解决方案
2.  给出了一个 C 代码，要求我找出错误。这是一个棘手的问题，涉及内存空间中的指针和字符对齐以及分段错误。
3.  关于函数重载的几个问题
    **解决方案** : [GeeksforGeeks Link](https://www.geeksforgeeks.org/overloading-in-java/)
4.  给出了列车的到达时间和离开时间，你必须找到列车所需的最小站台数。
    **解决方案** : [极客论坛链接](https://www.geeksforgeeks.org/minimum-number-platforms-required-railwaybus-station/)

 **第 3 轮**
这一轮详细讨论了我的实习项目。然后问了以下问题:

1.  当我们经常分配和释放内存时会发生什么？
    关于操作系统如何分配内存、碎片化、如何避免(压缩)进行了长时间的讨论。
2.  压实是如何工作的？他在问 algo
    告诉他内存块可以用 0(空闲)和 1(占用)来表示。压缩意味着最终移动所有的 0。我告诉他数组和链表各自的算法。
3.  解除分配是如何发生的，在解除分配过程中应该注意什么？
    我告诉他，我们可以使用 realloc()重用内存，而不是频繁地分配和释放内存。realloc()上有几个问题。
4.  为什么非常大的数组的行主遍历比列主遍历快？
    告诉他内部缓存可以带来的好处
5.  你必须走一段距离，你可以走 1、2 或 3 步。找出做 s0 的许多方法。
    给出了递归解和 dp 解。
    T2 解决方案:[极客论坛链接](https://www.geeksforgeeks.org/count-number-of-ways-to-cover-a-distance/)

 **第 4 轮(最后一轮 HR)**

1.  这基本上是一轮人力资源问题，比如为什么是 adobe？
2.  如果你得到另一份工作，你将如何决定接受哪一份？
3.  你的位置偏好是什么？等等被问到。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Adobe](https://practice.geeksforgeeks.org/company/Adobe/) !