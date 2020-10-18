# 查找矩阵中给定行的所有置换行

> 原文： [https://www.geeksforgeeks.org/find-permuted-rows-given-row-matrix/](https://www.geeksforgeeks.org/find-permuted-rows-given-row-matrix/)

给我们一个由正整数和行号组成的`m * n`矩阵。 任务是在给定矩阵中找到所有行，这些行是给定行元素的排列。 还假定每一行中的值都是不同的。

例子：

```
Input : mat[][] = {{3, 1, 4, 2}, 
                   {1, 6, 9, 3},
                   {1, 2, 3, 4},
                   {4, 3, 2, 1}}
        row = 3    
Output: 0, 2
Rows at indexes 0 and 2 are permutations of
row at index 3.

```



**简单解决方案**是对所有行逐一排序并检查所有行。 如果任何行与给定行完全相等，则意味着当前行是给定行的排列。 此方法的时间复杂度将为`O(m * n log n)`。

**有效方法**是使用哈希。 只需为给定的行创建[哈希集](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)。 创建哈希集后，遍历其余行，并针对每一行检查其所有元素是否存在于哈希集中。

## CPP

```

// C++ program to find all permutations of a given row 
#include<bits/stdc++.h> 
#define MAX 100 

using namespace std; 

// Function to find all permuted rows of a given row r 
void permutatedRows(int mat[][MAX], int m, int n, int r) 
{ 
    // Creating an empty set 
    unordered_set<int> s; 

    // Count frequencies of elements in given row r 
    for (int j=0; j<n; j++) 
        s.insert(mat[r][j]); 

    // Traverse through all remaining rows 
    for (int i=0; i<m; i++) 
    { 
        // we do not need to check for given row r 
        if (i==r) 
            continue; 

        // initialize hash i.e; count frequencies 
        // of elements in row i 
        int j; 
        for (j=0; j<n; j++) 
            if (s.find(mat[i][j]) == s.end()) 
                break; 
        if (j != n) 
           continue; 

        cout << i << ", "; 
    } 
} 

// Driver program to run the case 
int main() 
{ 
    int m = 4, n = 4,r = 3; 
    int mat[][MAX] = {{3, 1, 4, 2}, 
                      {1, 6, 9, 3}, 
                      {1, 2, 3, 4}, 
                      {4, 3, 2, 1}}; 
    permutatedRows(mat, m, n, r); 
    return 0; 
} 

```