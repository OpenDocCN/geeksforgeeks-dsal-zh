# 按特定顺序就地转换矩阵

> 原文： [https://www.geeksforgeeks.org/in-place-convert-matrix-in-specific-order/](https://www.geeksforgeeks.org/in-place-convert-matrix-in-specific-order/)

编写代码以特定方式转换矩阵，而无需使用额外的空间。

```

Input:
      1 2 3
      4 5 6
      7 8 9

Output:
      1 6 7
      2 5 8
      3 4 9

```

乍一看，这个问题似乎与寻找矩阵的转置类似。 但是，如果仔细看，您会发现输出矩阵中的每个偶数列在输入矩阵中都有对应行的元素以相反的顺序排列。

 **我们强烈建议您最小化浏览器，然后自己尝试。** 

通过对输入矩阵进行一些修改，可以轻松地将问题转换为矩阵转置。 如果我们反转输入矩阵中存在的每个偶数行，则可以使用[给定的解决方案](https://www.geeksforgeeks.org/inplace-m-x-n-size-matrix-transpose/)按所需顺序转换矩阵，并且也无需使用任何辅助存储器。

以下是该想法的 C++ 实现。

```

// Program for convert matrix in specific order 
// using in-place matrix transpose 
#include <bits/stdc++.h> 
#define HASH_SIZE 128 
using namespace std; 

// Non-square matrix transpose of matrix of size r x c 
// and base address A 
void transformMatrix(int *A, int r, int c) 
{ 
    // Invert even rows 
    for (int i = 1; i < r; i = i + 2) 
        for (int j1 = 0, j2 = c - 1; j1 < j2; j1++, j2--) 
            swap(*(A + i*c + j1), *(A + i*c + j2)); 

    // Rest of the code is from below post 
    // http://tinyurl.com/j79j445 
    int size = r*c - 1; 
    int t; // holds element to be replaced, eventually 
           // becomes next element to move 
    int next; // location of 't' to be moved 
    int cycleBegin; // holds start of cycle 

    bitset<HASH_SIZE> b; // hash to mark moved elements 

    b.reset(); 
    b[0] = b[size] = 1; 
    int i = 1; // Note that A[0] and A[size-1] won't move 
    while (i < size) 
    { 
        cycleBegin = i; 
        t = A[i]; 
        do
        { 
            // Input matrix [r x c] 
            // Output matrix 1 
            // i_new = (i*r)%(N-1) 
            next = (i*r)%size; 
            swap(A[next], t); 
            b[i] = 1; 
            i = next; 

        }  while (i != cycleBegin); 

        // Get Next Move (what about querying 
        // random location?) 
        for (i = 1; i < size && b[i]; i++) 
            ; 
    } 
} 

// A utility function to print a 2D array of size 
// nr x nc and base address A 
void Print2DArray(int *A, int nr, int nc) 
{ 
    for (int r = 0; r < nr; r++) 
    { 
        for (int c = 0; c < nc; c++) 
            printf("%4d", *(A + r*nc + c)); 

        printf("\n"); 
    } 

    printf("\n"); 
} 

// Driver program to test above function 
int main(void) 
{ 
    int A[][4] = {{1, 2, 3, 4}, 
                 {5, 6, 7, 8}, 
                 {9, 10, 11, 12}}; 

    int r = 3, c = 4; 

    cout << "Given Matrix:\n"; 
    Print2DArray((int *)A, r, c); 

    transformMatrix((int *)A, r, c); 

    cout << "Transformed Matrix:\n"; 
    Print2DArray((int *)A, c, r); 

    return 0; 
} 

```

输出：

```
Given Matrix:
   1   2   3   4
   5   6   7   8
   9  10  11  12

Transformed Matrix:
   1   8   9
   2   7  10
   3   6  11
   4   5  12

```

