# 用行或列的最大 GCD 替换每个矩阵元素

> 原文： [https://www.geeksforgeeks.org/replace-matrix-element-maximum-gcd-row-column/](https://www.geeksforgeeks.org/replace-matrix-element-maximum-gcd-row-column/)

给定`n`行和`m`列的矩阵。 任务是将每个矩阵元素替换为其行或列的最大公因数，以最大者为准。 也就是说，对于每个元素`(i, j)`，请从第`i`行的 GCD 或第`j`行的 GCD 中将其替换，以较大者为准。

**示例**：

```
Input : mat[3][4] = {1, 2, 3, 3,
                     4, 5, 6, 6
                     7, 8, 9, 9}  
Output :  1 1 3 3
          1 1 3 3
          1 1 3 3
For index (0,2), GCD of row 0 is 1, GCD of row 2 is 3.
So replace index (0,2) with 3 (3>1). 

```



这个想法是我们在这里讨论的概念 [LCM 的数组](https://www.geeksforgeeks.org/lcm-of-given-array-elements/)，用于查找行和列的 GCD。

使用**暴力**，我们可以遍历矩阵的元素，找到与该元素对应的行和列的 GCD 并将其替换为两者中的最大值。

一种有效的**方法**是分别为行和列制作大小为`n`和`m`的两个数组。 并存储每一行​​和每一列的 GCD。 大小为`n`的数组将包含每一行的 GCD，大小为`m`的数组将包含每一列的 GCD。 并用其对应的行 GCD 或列 GCD 的最大值替换每个元素。

以下是此方法的实现：

## C++ 

```cpp

// C++ program to replace each each element with 
// maximum of GCD of row or column. 
#include<bits/stdc++.h> 
using namespace std; 
#define R 3 
#define C 4 

// returning the greatest common divisor of two number 
int gcd(int a, int b) 
{ 
    if (b == 0) 
        return a; 
    return gcd(b, a%b); 
} 

// Finding GCD of each row and column and replacing 
// with each element with maximum of GCD of row or 
// column. 
void replacematrix(int mat[R][C], int n, int m) 
{ 
    int rgcd[R] = { 0 }, cgcd[C] = { 0 }; 

    // Calculating GCD of each row and each column in  
    // O(mn) and store in arrays. 
    for (int i = 0; i < n; i++) 
    { 
        for (int j = 0; j < m; j++) 
        { 
            rgcd[i] = gcd(rgcd[i], mat[i][j]); 
            cgcd[j] = gcd(cgcd[j], mat[i][j]); 
        } 
    } 

    // Replacing matrix element 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < m; j++) 
            mat[i][j] = max(rgcd[i], cgcd[j]); 
} 

// Driven Program 
int main() 
{ 
    int m[R][C] = 
    { 
        1, 2, 3, 3, 
        4, 5, 6, 6, 
        7, 8, 9, 9, 
    }; 

    replacematrix(m, R, C); 

    for (int i = 0; i < R; i++) 
    { 
        for (int j = 0; j < C; j++) 
            cout << m[i][j] << " "; 
        cout<<endl; 
    } 

    return 0; 
} 

```

## Java

```java
// Java program to replace each each element with 
// maximum of GCD of row or column. 
import java .io.*; 
  
class GFG 
{ 
      static int R = 3; 
      static int C = 4; 
  
      // returning the greatest common  
      // divisor of two number 
      static int gcd(int a, int b) 
      { 
         if (b == 0) 
         return a; 
         return gcd(b, a%b); 
      } 
  
// Finding GCD of each row and column and  
// replacing with each element with maximum 
// of GCD of row or column. 
static void replacematrix(int [][]mat, int n, int m) 
{ 
    int []rgcd = new int[R] ; 
    int []cgcd = new int[C]; 
  
    // Calculating GCD of each row and each column in  
    // O(mn) and store in arrays. 
    for (int i = 0; i < n; i++) 
    { 
        for (int j = 0; j < m; j++) 
        { 
            rgcd[i] = gcd(rgcd[i], mat[i][j]); 
            cgcd[j] = gcd(cgcd[j], mat[i][j]); 
        } 
    } 
  
    // Replacing matrix element 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < m; j++) 
            mat[i][j] = Math.max(rgcd[i], cgcd[j]); 
} 
  
// Driver program 
    static public void main (String[] args){ 
    int [][]m = 
    { 
        {1, 2, 3, 3}, 
        {4, 5, 6, 6}, 
        {7, 8, 9, 9}, 
    }; 
  
    replacematrix(m, R, C); 
  
    for (int i = 0; i < R; i++) 
    { 
        for (int j = 0; j < C; j++) 
        System.out.print(m[i][j] + " "); 
        System.out.println(); 
    } 
    } 
} 
  
//This code is contributed by vt_m.
```

## Python3

```py
# Python3 program to replace each each element  
# with maximum of GCD of row or column. 
  
R = 3
C = 4
  
# returning the greatest common  
# divisor of two number 
def gcd(a, b): 
    if (b == 0): 
        return a 
    return gcd(b, a % b) 
  
# Finding GCD of each row and column  
# and replacing with each element with  
# maximum of GCD of row or column. 
def replacematrix(mat, n, m): 
  
    rgcd = [0] * R  
    cgcd = [0] * C 
  
    # Calculating GCD of each row and each  
    # column in O(mn) and store in arrays. 
    for i in range (n): 
        for j in range (m): 
          
            rgcd[i] = gcd(rgcd[i], mat[i][j]) 
            cgcd[j] = gcd(cgcd[j], mat[i][j]) 
  
    # Replacing matrix element 
    for i in range (n): 
        for j in range (m): 
            mat[i][j] = max(rgcd[i], cgcd[j]) 
  
# Driver Code 
if __name__ == "__main__": 
  
    m = [[1, 2, 3, 3], 
         [4, 5, 6, 6], 
         [7, 8, 9, 9]] 
  
    replacematrix(m, R, C) 
  
    for i in range(R): 
        for j in range (C): 
            print ( m[i][j], end = " ") 
        print () 
      
# This code is contributed by ita_c
```

## C#

```cs
// C# program to replace each each element with 
// maximum of GCD of row or column. 
using System; 
  
class GFG 
{ 
      static int R = 3; 
      static int C = 4; 
    
      // returning the greatest common  
      // divisor of two number 
      static int gcd(int a, int b) 
      { 
        if (b == 0) 
        return a; 
        return gcd(b, a%b); 
      } 
  
// Finding GCD of each row and column and 
// replacing with each element with maximum 
// of GCD of row or column. 
static void replacematrix(int [,]mat, int n, int m) 
{ 
    int []rgcd = new int[R] ; 
    int []cgcd = new int[C]; 
  
    // Calculating GCD of each row and each column in  
    // O(mn) and store in arrays. 
    for (int i = 0; i < n; i++) 
    { 
        for (int j = 0; j < m; j++) 
        { 
            rgcd[i] = gcd(rgcd[i], mat[i,j]); 
            cgcd[j] = gcd(cgcd[j], mat[i,j]); 
        } 
    } 
  
    // Replacing matrix element 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < m; j++) 
            mat[i,j] = Math.Max(rgcd[i], cgcd[j]); 
} 
  
// Driver program 
    static public void Main (){ 
    int [,]m = 
    { 
        {1, 2, 3, 3}, 
        {4, 5, 6, 6}, 
        {7, 8, 9, 9}, 
    }; 
  
    replacematrix(m, R, C); 
  
    for (int i = 0; i < R; i++) 
    { 
        for (int j = 0; j < C; j++) 
        Console.Write(m[i,j] + " "); 
        Console.WriteLine(); 
    } 
    } 
} 
  
//This code is contributed by vt_m.
```

输出：

```
1 1 3 3 
1 1 3 3 
1 1 3 3 
```

时间复杂度：`O(mn)`。

辅助空间：`O(m + n)`。