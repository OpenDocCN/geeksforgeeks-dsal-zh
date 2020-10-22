# 矩阵查询

> 原文： [https://www.geeksforgeeks.org/queries-in-a-matrix/](https://www.geeksforgeeks.org/queries-in-a-matrix/)

给定大小为`m x n`（`1 < = m, n < = 1000`）的矩阵`M`。 最初按行主顺序依次填充从 1 到`m x n`的整数。 任务是处理操纵`M`的查询列表，以使每个查询都是以下三个之一。

1.  `R(x, y)`：交换`M`的第`x`和`y`行，其中`x`和`y`从 1 到`m`变化。

2.  `C(x, y)`：交换`M`的第`x`和`y`列，其中`x`和`y`在 1 到`n`之间变化。

3.  `P(x, y)`：在第`x`行和第`y`列打印元素，其中`x`从 1 到`m`变化，而`y`从 1 到`n`变化。

请注意，给定矩阵存储为典型的 2D 数组，索引从 0 开始，但是`x`和`y`的值从 1 开始。

例子：

```
Input : m = 3, n = 3
        R(1, 2)
        P(1, 1)
        P(2, 1)
        C(1, 2)
        P(1, 1)
        P(2, 1)
Output: value at (1, 1) = 4
        value at (2, 1) = 1
        value at (1, 1) = 5
        value at (2, 1) = 2
Explanation:
The matrix is {{1, 2, 3}, 
               {4, 5, 6},
               {7, 8, 9}}
After first R(1, 2) matrix becomes, 
              {{4, 5, 6}, 
               {1, 2, 3}, 
               {7, 8, 9}}
After first C(1, 2) matrix becomes, 
              {{5, 4, 6}, 
               {2, 1, 3}, 
               {8, 7, 9}}

Input : m = 1234, n = 5678
        R(1, 2)
        P(1, 1)
        P(2, 1)
        C(1, 2)
        P(1, 1)
        P(2, 1)
Output: value at (1, 1) = 5679
        value at (2, 1) = 1
        value at (1, 1) = 5680
        value at (2, 1) = 2

```



解决此问题的**简单解决方案**是手动完成所有查询，这意味着当我们不得不交换行时，只需交换第`x`行和第`y`行的元素，并且类似地进行列沼泽。 但是这种方法的时间复杂度可能为`q * O(m)`或`q * O(n)`，其中`q`是查询数，所需辅助空间为`O(m * n)`。

解决此问题的有效方法**几乎不需要数学观察**。 在这里，我们给出矩阵中的元素按行主要顺序从 1 到`mxn`依次填充，因此我们将利用此给定方案并解决此问题。

*   创建一个辅助数组`rows[m]`，并将其值从 0 到`m-1`依次填充。

*   创建另一个辅助数组`cols[n]`并依次将其值从 0 填充到`n-1`。

*   现在，对于查询`R(x, y)`，只需将`rows[x-1]`的值替换为`rows[y-1]`。

*   现在，对于查询`C(x, y)`，只需将`cols[x-1]`的值与`cols[y-1]`交换即可。

*   现在，对于查询`P(x, y)`，只需跳过您已经看到的列数，并通过`rows[x-1] * n + cols[y-1] + 1`计算`(x, y)`处的值。

以下是上述想法的实现。

## C++ 

```cpp

// C++ implementation of program 
#include<bits/stdc++.h> 
using namespace std; 

// Fills initial values in rows[] and cols[] 
void preprocessMatrix(int rows[], int cols[], 
                     int m, int n) 
{ 
    // Fill rows with 1 to m-1 
    for (int i=0; i<m; i++) 
        rows[i] = i; 

    // Fill columns with 1 to n-1 
    for (int i=0; i<n; i++) 
        cols[i] = i; 
} 

// Function to perform queries on matrix 
// m --> number of rows 
// n --> number of columns 
// ch --> type of query 
// x --> number of row for query 
// y --> number of column for query 
void queryMatrix(int rows[], int cols[], int m, 
                 int n, char ch, int x, int y) 
{ 
    // perform queries 
    int tmp; 
    switch(ch) 
    { 
    case 'R': 

        // swap row x with y 
        swap(rows[x-1], rows[y-1]); 
        break; 

    case 'C': 

        // swap coloumn x with y 
        swap(cols[x-1], cols[y-1]); 
        break; 

    case 'P': 

        // Print value at (x, y) 
        printf("value at (%d, %d) = %d\n", x, y, 
                   rows[x-1]*n + cols[y-1]+1); 
        break; 
    } 
    return ; 
} 

// Driver program to run the case 
int main() 
{ 
    int m = 1234, n = 5678; 

    // row[] is array for rows and cols[] 
    // is array for coloumns 
    int rows[m], cols[n]; 

    // Fill initial values in rows[] and cols[] 
    preprocessMatrix(rows, cols, m, n); 

    queryMatrix(rows, cols, m, n, 'R', 1, 2); 
    queryMatrix(rows, cols, m, n, 'P', 1, 1); 
    queryMatrix(rows, cols, m, n, 'P', 2, 1); 
    queryMatrix(rows, cols, m, n, 'C', 1, 2); 
    queryMatrix(rows, cols, m, n, 'P', 1, 1); 
    queryMatrix(rows, cols, m, n, 'P', 2, 1); 
    return 0; 
} 

```

## C++

```cpp
// C++ implementation of program 
#include<bits/stdc++.h> 
using namespace std; 
  
// Fills initial values in rows[] and cols[] 
void preprocessMatrix(int rows[], int cols[], 
                     int m, int n) 
{ 
    // Fill rows with 1 to m-1 
    for (int i=0; i<m; i++) 
        rows[i] = i; 
  
    // Fill columns with 1 to n-1 
    for (int i=0; i<n; i++) 
        cols[i] = i; 
} 
  
// Function to perform queries on matrix 
// m --> number of rows 
// n --> number of columns 
// ch --> type of query 
// x --> number of row for query 
// y --> number of column for query 
void queryMatrix(int rows[], int cols[], int m, 
                 int n, char ch, int x, int y) 
{ 
    // perform queries 
    int tmp; 
    switch(ch) 
    { 
    case 'R': 
  
        // swap row x with y 
        swap(rows[x-1], rows[y-1]); 
        break; 
  
    case 'C': 
  
        // swap coloumn x with y 
        swap(cols[x-1], cols[y-1]); 
        break; 
  
    case 'P': 
  
        // Print value at (x, y) 
        printf("value at (%d, %d) = %d\n", x, y, 
                   rows[x-1]*n + cols[y-1]+1); 
        break; 
    } 
    return ; 
} 
  
// Driver program to run the case 
int main() 
{ 
    int m = 1234, n = 5678; 
  
    // row[] is array for rows and cols[] 
    // is array for coloumns 
    int rows[m], cols[n]; 
  
    // Fill initial values in rows[] and cols[] 
    preprocessMatrix(rows, cols, m, n); 
  
    queryMatrix(rows, cols, m, n, 'R', 1, 2); 
    queryMatrix(rows, cols, m, n, 'P', 1, 1); 
    queryMatrix(rows, cols, m, n, 'P', 2, 1); 
    queryMatrix(rows, cols, m, n, 'C', 1, 2); 
    queryMatrix(rows, cols, m, n, 'P', 1, 1); 
    queryMatrix(rows, cols, m, n, 'P', 2, 1); 
    return 0; 
}
```

## Java

```java
// Java implementation of program  
class GFG  
{ 
  
    // Fills initial values in rows[] and cols[]  
    static void preprocessMatrix(int rows[], int cols[], 
                                        int m, int n)  
    { 
        // Fill rows with 1 to m-1  
        for (int i = 0; i < m; i++) 
        { 
            rows[i] = i; 
        } 
  
        // Fill columns with 1 to n-1  
        for (int i = 0; i < n; i++)  
        { 
            cols[i] = i; 
        } 
    } 
  
    // Function to perform queries on matrix  
    // m --> number of rows  
    // n --> number of columns  
    // ch --> type of query  
    // x --> number of row for query  
    // y --> number of column for query  
    static void queryMatrix(int rows[], int cols[], int m, 
                            int n, char ch, int x, int y)  
    { 
        // perform queries  
        int tmp; 
        switch (ch)  
        { 
            case 'R': 
  
                // swap row x with y  
                swap(rows, x - 1, y - 1); 
                break; 
  
            case 'C': 
  
                // swap coloumn x with y  
                swap(cols, x - 1, y - 1); 
                break; 
  
            case 'P': 
  
                // Print value at (x, y)  
                System.out.printf("value at (%d, %d) = %d\n", x, y, 
                        rows[x - 1] * n + cols[y - 1] + 1); 
                break; 
        } 
        return; 
    } 
  
    static int[] swap(int[] arr, int i, int j)  
    { 
        int temp = arr[i]; 
        arr[i] = arr[j]; 
        arr[j] = temp; 
        return arr; 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        int m = 1234, n = 5678; 
  
        // row[] is array for rows and cols[]  
        // is array for coloumns  
        int rows[] = new int[m], cols[] = new int[n]; 
  
        // Fill initial values in rows[] and cols[]  
        preprocessMatrix(rows, cols, m, n); 
  
        queryMatrix(rows, cols, m, n, 'R', 1, 2); 
        queryMatrix(rows, cols, m, n, 'P', 1, 1); 
        queryMatrix(rows, cols, m, n, 'P', 2, 1); 
        queryMatrix(rows, cols, m, n, 'C', 1, 2); 
        queryMatrix(rows, cols, m, n, 'P', 1, 1); 
        queryMatrix(rows, cols, m, n, 'P', 2, 1); 
    } 
} 
  
// This code contributed by Rajput-Ji
```

## C#

```cs
// C# implementation of program  
using System; 
  
class GFG  
{ 
  
    // Fills initial values in rows[] and cols[]  
    static void preprocessMatrix(int []rows, int []cols, 
                                        int m, int n)  
    { 
        // Fill rows with 1 to m-1  
        for (int i = 0; i < m; i++) 
        { 
            rows[i] = i; 
        } 
  
        // Fill columns with 1 to n-1  
        for (int i = 0; i < n; i++)  
        { 
            cols[i] = i; 
        } 
    } 
  
    // Function to perform queries on matrix  
    // m --> number of rows  
    // n --> number of columns  
    // ch --> type of query  
    // x --> number of row for query  
    // y --> number of column for query  
    static void queryMatrix(int []rows, int []cols, int m, 
                            int n, char ch, int x, int y)  
    { 
        // perform queries  
        int tmp; 
        switch (ch)  
        { 
            case 'R': 
  
                // swap row x with y  
                swap(rows, x - 1, y - 1); 
                break; 
  
            case 'C': 
  
                // swap coloumn x with y  
                swap(cols, x - 1, y - 1); 
                break; 
  
            case 'P': 
  
                // Print value at (x, y)  
                Console.Write("value at ({0}, {1}) = {2}\n", x, y, 
                        rows[x - 1] * n + cols[y - 1] + 1); 
                break; 
        } 
        return; 
    } 
  
    static int[] swap(int[] arr, int i, int j)  
    { 
        int temp = arr[i]; 
        arr[i] = arr[j]; 
        arr[j] = temp; 
        return arr; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int m = 1234, n = 5678; 
  
        // row[] is array for rows and cols[]  
        // is array for coloumns  
        int []rows = new int[m]; int []cols = new int[n]; 
  
        // Fill initial values in rows[] and cols[]  
        preprocessMatrix(rows, cols, m, n); 
  
        queryMatrix(rows, cols, m, n, 'R', 1, 2); 
        queryMatrix(rows, cols, m, n, 'P', 1, 1); 
        queryMatrix(rows, cols, m, n, 'P', 2, 1); 
        queryMatrix(rows, cols, m, n, 'C', 1, 2); 
        queryMatrix(rows, cols, m, n, 'P', 1, 1); 
        queryMatrix(rows, cols, m, n, 'P', 2, 1); 
    } 
} 
  
/* This code contributed by PrinciRaj1992 */
```

输出：

```
value at (1, 1) = 5679
value at (2, 1) = 1
value at (1, 1) = 5680
value at (2, 1) = 2
```

时间复杂度：`O(q)`，`q =`查询数。

腋窝空间：`O(m + n)`。