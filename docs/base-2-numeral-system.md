# 基数-2 数字系统

> 原文:[https://www.geeksforgeeks.org/base-2-numeral-system/](https://www.geeksforgeeks.org/base-2-numeral-system/)

我们已经研究过计算机是用 0 和 1 工作的，这是位的一部分，位有两种情况，就像开关有开和关两种功能。为了方便起见，我们将 1 和 0 称为开和关。这些被称为位，这是被称为二进制数字的最小单位。
我们通常在一个十进制系统中工作，在这个系统中，0 到 9 这 10 个数字在一个序列中，加减乘除的全部工作都是用这些数字或数字完成的。在计算机 0 和 1 中，这两个数字写下了设备中输入的所有信息。

**字节**

1.  一个比特根本没有用，所以当它和其他比特结合在一起时，只有一个完整的意义是由任何数据或信息组成的。对我们来说，这一系列的 8 个比特是重要的，被称为字节。这是最重要和最基本的单位。整个计算机的存储结构是以千字节和兆字节来计算的。
2.  所有的活动都是用这些字节完成的。存储信息字节对计算机来说是一个临时的东西，可以以任何形式使用，所以计算机与数据一起做两个重要的工作，第一个是与数字一起工作，或者我们可以说，作为一个数学计算是与数字一起进行的，与科学一起进行不同的活动，在一个字节中，我们可以以两种方式存储数据:数字系统或符号系统。
3.  实际上，两种形式的数据在字节上没有区别，唯一的区别是如何知道 bite 有一个数字或符号，我们必须知道我们将如何使用这些数据。

#### 二进制数

1.  我们知道，在十进制系统中，我们从右到左执行数字，如数字 1、10、100、1000、10000、100000、100000 等。
2.  这就是所谓的一，十，一百，一千，一万，十万，十万，等等。这个数字系统的含义是以 10 为基数，因为它有 10 个数字 0，1，2，3，4，5，6，7，8 和 9。
3.  但是二进制数字系统的基数是 2，因为所有的数字都被计数成两个数字，分别是 0 和 1。因此，当我们写整个二进制数字系统时，比特位置是从右向左执行的，数值是 1，2，4，8，16，32，64，128 等的两倍。
4.  请记住，位序列是从右向左的，最初它是从零开始的。最佳值与序列有关系，每个位的数字值是 2。示例位序列有 3，值为 2 意味着 8，就像这样，可以理解其他位。
5.  在计算机中，所有的数列都是以二进制形式保存的，在这种形式下，它们被加、减、除、乘或任何其他算术运算都是通过这种形式完成的。任何数字都可以写成二进制，所以没有区别。
6.  任何十进制都可以转换成二进制，它有一种特殊的方式，但这不属于本文的主题，这就是为什么我们要离开这里，在本文中，我们将只讨论等于二进制数字的前 16 个十进制。

<figure class="table">

| 十进制 | 二进制 |
| Zero | Zero |
| one | one |
| Two | Ten |
| three | Eleven |
| four | One hundred |
| five | One hundred and one |
| six | One hundred and ten |
| seven | One hundred and eleven |
| eight | One thousand |
| nine | One thousand and one |
| Ten | One thousand and ten |
| Eleven | One thousand and eleven |
| Twelve | One thousand one hundred |
| Thirteen | One thousand one hundred and one |
| Fourteen | One thousand one hundred and ten |
| Fifteen | One thousand one hundred and eleven |

</figure>

为了将任何二进制系统转换成十进制系统，每个位都被添加，因为实际上只有一个位被添加，因为零位没有值，例如日记系统 1101 有 31 个位，其中第一个位的值为 8 秒，第三个位的值为 4，在添加这些位后，我们得到 13，这就是为什么二进制系统 1101 等于十进制系统 13。

我们存储一个字母，以便一口就签入，就像 ok，如果我们要写 ASHA BISHT，并且想要存储它，那么我们需要 10 个字节。在这 9 个字母中，有一个空格，每个空格有一个不同的字节，如下所示:

<figure class="table">

| A | S | H | A |   | B | 我 | S | H | T |

所以我们知道，每个比特有 8 位，每个比特有两个值 0 和 1，这就是为什么根据数学规则，1 字节有 2 次方 8 位，这意味着可以形成 256 个不同的组，这意味着 1 字节有 0 到 255，这意味着总值 256 系列将被显示，它有另一个含义，一个比特有 256 个不同的符号或字母存储在其中。

<figure class="table">

| 信 | ASCII 码 | 电子商务代码 |
| A | 01000001 | Eleven million and one |
| B | 01000010 | Eleven million and ten |
| C | 01000011 | Eleven million one hundred |
| D | 01000101 | Eleven million one hundred and one |

字母和符号以字节的形式存储，这种方式被称为编码系统。两种已知的系统是 ASCII 或美国信息交换标准代码或 EBCDIC 或扩展二进制十进制交换代码。

</figure>

</figure>