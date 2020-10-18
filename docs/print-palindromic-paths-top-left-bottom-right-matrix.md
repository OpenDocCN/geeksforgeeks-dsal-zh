# 在矩阵中从左上到右下打印所有回文路径

> 原文： [https://www.geeksforgeeks.org/print-palindromic-paths-top-left-bottom-right-matrix/](https://www.geeksforgeeks.org/print-palindromic-paths-top-left-bottom-right-matrix/)

给定一个仅包含较低字母字符的矩阵，我们需要在给定的矩阵中打印所有回文路径。 路径定义为从左上角的单元格到右下角的单元格的一系列单元格。 我们只能从当前单元格左右移动。 我们不能斜着走。

**例如**：

```
Input : mat[][] = {"aaab", 
                   "baaa"
                   "abba"}
Output :aaaaaa, aaaaaa, abaaba

Explanation :
aaaaaa (0, 0) -> (0, 1) -> (1, 1) -> 
       (1, 2) -> (1, 3) -> (2, 3)    
aaaaaa (0, 0) -> (0, 1) -> (0, 2) -> 
       (1, 2) -> (1, 3) -> (2, 3)    
abaaba (0, 0) -> (1, 0) -> (1, 1) -> 
       (1, 2) -> (2, 2) -> (2, 3)

```

输出数组中元素的顺序无关紧要。



这个想法很简单。 我们从左上角`(0, 0)`开始，探索到右下角的所有路径。 如果路径变成回文，我们将其打印出来。

## C++ 

```cpp

// C++ program to print all palindromic paths 
// from top left to bottom right in a grid. 
#include<bits/stdc++.h> 
using namespace std; 
#define N 4 
bool isPalin(string str) 
{ 
    int len = str.length() / 2; 
    for (int i = 0; i < len; i++)  
    { 
        if (str[i] != str[str.length() - i - 1]) 
            return false; 
    } 
    return true; 
} 

// i and j are row and column indexes of current cell  
// (initially these are 0 and 0). 
void palindromicPath(string str, char a[][N], 
                            int i, int j, int m, int n) 
{ 

    // If we have not reached bottom right corner, keep 
    // exlporing 
    if (j < m - 1 || i < n - 1)  
    { 
        if (i < n - 1) 
            palindromicPath(str + a[i][j], a, i + 1, j, m, n); 
        if (j < m - 1) 
            palindromicPath(str + a[i][j], a, i, j + 1, m, n); 
    }  

    // If we reach bottom right corner, we check if 
    // if the path used is palindrome or not. 
    else { 
        str = str + a[n - 1][m - 1]; 
        if (isPalin(str)) 
            cout<<(str)<<endl; 
    } 
} 

// Driver code  
int main() 
{ 
    char arr[][N] = { { 'a', 'a', 'a', 'b' }, 
                    { 'b', 'a', 'a', 'a' }, 
                    { 'a', 'b', 'b', 'a' } }; 
    string str = ""; 
    palindromicPath(str, arr, 0, 0, 4, 3); 
    return 0; 
} 

// This code is contributed by andrew1234 

```