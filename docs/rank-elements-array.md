# 数组中所有元素的排名

> 原文： [https://www.geeksforgeeks.org/rank-elements-array/](https://www.geeksforgeeks.org/rank-elements-array/)

给定`N`个整数数组，允许重复。 如果所有元素都不同，则它们按升序从 1 到`N`排列。 如果说有`x`个具有特定值的重复元素，则应为每个元素分配一个等级，该等级等于`x`个连续等级的算术平均值。

**示例**：

```
Input : 20 30 10
Output : 2.0 3.0 1.0

Input : 10 12 15 12 10 25 12
Output : 1.5, 4.0, 6.0, 4.0, 1.5, 7.0, 4.0
10 is the smallest and there are two 10s so 
take the average of two consecutive ranks 
1 and 2 i.e. 1.5 . Next smallest element is 12\. 
Since, two elements are already ranked, the 
next rank that can be given is 3\. However, there 
are three 12's so the rank of 2 is (3+4+5) / 3 = 4.
Next smallest element is 15\. There is only one 15 
so 15 gets a rank of 6 since 5 elements are ranked. 
Next element is 25 and it gets a rank of 7.

Input : 1, 2, 5, 2, 1, 60, 3
Output : 1.5, 3.5, 6.0, 3.5, 1.5, 7.0, 5.0

```

首次输入的说明：

**方法 I（简单）**：

考虑到没有重复的元素。 在这种情况下，每个元素的等级仅是 1 加上数组中较小元素的数量。 现在，如果数组包含重复的元素，则也可以通过考虑不相等的元素来修改等级。 如果恰好有小于`e`的`r`个元素和等于`e`的`s`个元素，则`e`得到的等级为：

```
(r + r+1 + r+2 ... r+s-1)/s 

[Separating all r's and applying 
natural number sum formula]
= (r*s + s*(s-1)/2)/s
= r + 0.5*(s-1)

```

算法：

```
function rankify(A)
    N = length of A
    R is the array for storing ranks
    for i in 0..N-1
        r = 1, s = 1
        for j in 0..N-1
            if j != i and A[j] < A[i]
                r += 1
            if j != i and A[j] = A[i]
                s += 1
        // Assign Rank to A[i]
        R[i] = r + 0.5*(s-1)
    return R

```

该方法的实现如下：

## C++ 

```cpp

// CPP Code to find rank of elements 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find rank 
void rankify(int* A , int n) { 

    // Rank Vector 
    float R[n] = {0}; 

    // Sweep through all elements in A for each 
    // element count the number of less than and 
    // equal elements separately in r and s. 
    for (int i = 0; i < n; i++) { 
        int r = 1, s = 1; 

        for (int j = 0; j < n; j++) { 
            if (j != i && A[j] < A[i]) 
                r += 1; 

            if (j != i && A[j] == A[i]) 
                s += 1;      
        } 

        // Use formula to obtain rank 
        R[i] = r + (float)(s - 1) / (float) 2; 

    }  

    for (int i = 0; i < n; i++) 
        cout << R[i] << ' '; 

    } 

// Driver Code 
int main() { 
    int A[] = {1, 2, 5, 2, 1, 25, 2}; 
    int n = sizeof(A) / sizeof(A[0]); 

    for (int i = 0; i < n; i++) 
    cout << A[i] << ' '; 
    cout << '\n'; 

    rankify(A, n); 

    return 0; 
} 

// This code is contributed by Gitanjali. 

```

## Java

```java

// Java Code to find rank of elements 
public class GfG { 

    // Function to print m Maximum elements 
    public static void rankify(int A[], int n) 
    { 
        // Rank Vector 
        float R[] = new float[n]; 

        // Sweep through all elements in A 
        // for each element count the number 
        // of less than and equal elements 
        // separately in r and s 
        for (int i = 0; i < n; i++) { 
            int r = 1, s = 1; 

            for (int j = 0; j < n; j++)  
            { 
                if (j != i && A[j] < A[i]) 
                    r += 1; 

                if (j != i && A[j] == A[i]) 
                    s += 1;      
            } 

        // Use formula to obtain  rank 
        R[i] = r + (float)(s - 1) / (float) 2; 

        }  

        for (int i = 0; i < n; i++) 
            System.out.print(R[i] + "  "); 

    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int A[] = {1, 2, 5, 2, 1, 25, 2}; 
        int n = A.length; 

        for (int i = 0; i < n; i++) 
            System.out.print(A[i] + "    "); 
            System.out.println(); 
            rankify(A, n); 
    } 
} 

// This code is contributed by Swetank Modi 

```

## Python3

```py

# Python Code to find  
# rank of elements 
def rankify(A): 

    # Rank Vector 
    R = [0 for x in range(len(A))] 

    # Sweep through all elements 
    # in A for each element count 
    # the number of less than and  
    # equal elements separately 
    # in r and s. 
    for i in range(len(A)): 
        (r, s) = (1, 1) 
        for j in range(len(A)): 
            if j != i and A[j] < A[i]: 
                r += 1
            if j != i and A[j] == A[i]: 
                s += 1       

        # Use formula to obtain rank 
        R[i] = r + (s - 1) / 2

    # Return Rank Vector 
    return R 

if __name__ == "__main__": 
    A = [1, 2, 5, 2, 1, 25, 2] 
    print(A) 
    print(rankify(A)) 

```

## C# 

```cs

// C# Code to find rank of elements 
using System; 

public class GfG { 

    // Function to print m Maximum 
    // elements 
    public static void rankify(int []A, int n) 
    { 
        // Rank Vector 
        float []R = new float[n]; 

        // Sweep through all elements 
        // in A  for each element count 
        // the number  of less than and 
        // equal elements separately in 
        // r and s 
        for (int i = 0; i < n; i++) { 
            int r = 1, s = 1; 

            for (int j = 0; j < n; j++)  
            { 
                if (j != i && A[j] < A[i]) 
                    r += 1; 

                if (j != i && A[j] == A[i]) 
                    s += 1;  
            } 

        // Use formula to obtain rank 
        R[i] = r + (float)(s - 1) / (float) 2; 

        }  

        for (int i = 0; i < n; i++) 
            Console.Write(R[i] + " "); 

    } 

    // Driver code 
    public static void Main() 
    { 
        int []A = {1, 2, 5, 2, 1, 25, 2}; 
        int n = A.Length; 

        for (int i = 0; i < n; i++) 
            Console.Write(A[i] + " "); 
            Console.WriteLine(); 
            rankify(A, n); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP Code to find rank of elements  

// Function to find rank  
function rankify($A , $n)  
{  

    // Rank Vector  
    $R = array(0);  

    // Sweep through all elements in A for each  
    // element count the number of less than and  
    // equal elements separately in r and s.  
    for ($i = 0; $i < $n; $i++)  
    {  
        $r = 1; 
        $s = 1;  

        for ($j = 0; $j < $n; $j++)  
        {  
            if ($j != $i && $A[$j] < $A[$i])  
                $r += 1;  

            if ($j != $i && $A[$j] == $A[$i])  
                $s += 1;      
        }  

        // Use formula to obtain rank  
        $R[$i] = $r + (float)($s - 1) / (float) 2;  

    }  

    for ($i = 0; $i < $n; $i++)  
        print number_format($R[$i], 1) . ' ';  
}  

// Driver Code 
$A = array(1, 2, 5, 2, 1, 25, 2);  
$n = count($A); 
for ($i = 0; $i < $n; $i++)  
echo $A[$i] . ' ';  
echo "\n";  

rankify($A, $n);  

// This code is contributed by Rajput-Ji 
?> 

```

**输出**：

```
[1, 2, 5, 2, 1, 25, 2]
[1.5, 4.0, 6.0, 4.0, 1.5, 7.0, 4.0]

```

时间复杂度为`O(N * N)`，而空间复杂度为`O(1)`（不包括保持等级所需的空间）

**方法 II（高效）**：

在此方法中，创建另一个元组数组`T`。 元组的第一个元素存储值，而第二个元素引用数组中值的索引。 然后，使用每个元组的第一个值以升序对`T`进行排序。 排序后，可以保证相等的元素相邻。 然后简单地走下`T`，找到相邻元素的编号，并为每个这些元素设置等级。 使用每个元组的第二个成员来确定值的索引。

Algorithm

```
function rankify_improved(A)
    N = Length of A 
    T = Array of tuples (i,j), 
        where i = A[i] and j = i
    R = Array for storing ranks
    Sort T in ascending order 
    according to i

    for j in 0...N-1
        k = j 

        // Find adjacent elements
        while A[k] == A[k+1]
            k += 1 

        // No of adjacent elements
        n = k - j + 1

        // Modify rank for each
        // adjacent element
        for j in 0..n-1

            // Get the index of the
            // jth adjacent element
            index = T[i+j][1]
            R[index] = r + (n-1)*0.5

        // Skip n ranks
        r += n

        // Skip n indices
        j += n

    return R

```

该方法的 Python 实现在下面给出：

## Python3

```py

# Python code to find  
# rank of elements 
def rankify_improved(A): 

    # create rank vector 
    R = [0 for i in range(len(A))] 

    # Create an auxiliary array of tuples 
    # Each tuple stores the data as well 
    # as its index in A 
    T = [(A[i], i) for i in range(len(A))] 

    # T[][0] is the data and T[][1] is 
    # the index of data in A 

    # Sort T according to first element 
    T.sort(key=lambda x: x[0]) 

    (rank, n, i) = (1, 1, 0) 

    while i < len(A): 
        j = i 

        # Get no of elements with equal rank 
        while j < len(A) - 1 and T[j][0] == T[j + 1][0]: 
            j += 1
        n = j - i + 1

        for j in range(n): 

            # For each equal element use formula 
            # obtain index of T[i+j][0] in A 
            idx = T[i+j][1] 
            R[idx] = rank + (n - 1) * 0.5

        # Increment rank and i 
        rank += n 
        i += n 

    return R 

if __name__ == "__main__": 
    A = [1, 2, 5, 2, 1, 25, 2] 
    print(A) 
    print(rankify_improved(A)) 

```

输出：

```
[1, 2, 5, 2, 1, 25, 2]
[1.5, 4.0, 6.0, 4.0, 1.5, 7.0, 4.0]
```

时间复杂度取决于排序过程，通常为`O(N Log N)`。 辅助空间为`O(N)`，因为我们需要存储索引和值。