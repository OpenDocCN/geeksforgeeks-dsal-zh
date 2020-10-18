# 子矩阵总和查询

> 原文： [https://www.geeksforgeeks.org/submatrix-sum-queries/](https://www.geeksforgeeks.org/submatrix-sum-queries/)

给定大小为`M x N`的矩阵，需要大量查询来查找子矩阵和。 查询的输入是要求和的子矩阵的左上和右下索引。

如何预处理矩阵，以便可以在`O(1)`时间内执行子矩阵和查询。

**示例**：

```
tli :  Row number of top left of query submatrix
tlj :  Column number of top left of query submatrix
rbi :  Row number of bottom right of query submatrix
rbj :  Column number of bottom right of query submatrix

Input: mat[M][N] = {{1, 2, 3, 4, 6},
                    {5, 3, 8, 1, 2},
                    {4, 6, 7, 5, 5},
                    {2, 4, 8, 9, 4} };
Query1: tli = 0, tlj = 0, rbi = 1, rbj = 1
Query2: tli = 2, tlj = 2, rbi = 3, rbj = 4
Query3: tli = 1, tlj = 2, rbi = 3, rbj = 3;

Output:
Query1: 11  // Sum between (0, 0) and (1, 1)
Query2: 38  // Sum between (2, 2) and (3, 4)
Query3: 38  // Sum between (1, 2) and (3, 3)

```

**我们强烈建议您最小化浏览器，然后自己尝试。**

这个想法是首先创建一个辅助矩阵`aux[M][N]` ，以便`aux[i][j]`将元素的和存储在从`(0, 0)`到`(i, j)`的子矩阵中。 构造`aux[][]`后，我们可以在`O(1)`时间内计算`(tli, tlj)`和`(rbi, rbj)`之间的子矩阵和。 我们需要考虑`aux[rbi][rbj]`并减去所有不必要的元素。 以下是在`O(1)`时间内计算子矩阵和的完整表达式。

```
Sum between (tli, tlj) and (rbi, rbj) is,
   aux[rbi][rbj] - aux[tli-1][rbj] - 
   aux[rbi][tlj-1] + aux[tli-1][tlj-1]

The submatrix aux[tli-1][tlj-1] is added because  
elements of it are subtracted twice.

```

**插图**：

```
mat[M][N] = {{1, 2, 3, 4, 6},
             {5, 3, 8, 1, 2},
             {4, 6, 7, 5, 5},
             {2, 4, 8, 9, 4} };

We first preprocess the matrix and build
following aux[M][N]
aux[M][N] = {1,  3,   6,  10, 16}
            {6,  11,  22, 27,  35},
            {10, 21,  39, 49,  62},  
            {12, 27,  53, 72,  89} }

Query : tli = 2, tlj = 2, rbi = 3, rbj = 4  

Sum between (2, 2) and (3, 4) = 89 - 35 - 27 + 11
                              = 38

```

**如何建立`aux[M][N]`？**

1.  将`mat[][]`的第一行复制到`aux[][]`。

2.  将矩阵按列求和并存储。

3.  在步骤 2 中对更新矩阵`aux[][]`进行逐行求和。

下面是基于上述思想的程序。

## C++ 

```cpp

// C++ program to compute submatrix query sum in O(1) 
// time 
#include<iostream> 
using namespace std; 
#define M 4 
#define N 5 

// Function to preprcess input mat[M][N].  This function 
// mainly fills aux[M][N] such that aux[i][j] stores sum 
// of elements from (0,0) to (i,j) 
int preProcess(int mat[M][N], int aux[M][N]) 
{ 
   // Copy first row of mat[][] to aux[][] 
   for (int i=0; i<N; i++) 
      aux[0][i] = mat[0][i]; 

   // Do column wise sum 
   for (int i=1; i<M; i++) 
      for (int j=0; j<N; j++) 
         aux[i][j] = mat[i][j] + aux[i-1][j]; 

   // Do row wise sum 
   for (int i=0; i<M; i++) 
      for (int j=1; j<N; j++) 
         aux[i][j] += aux[i][j-1]; 
} 

// A O(1) time function to compute sum of submatrix 
// between (tli, tlj) and (rbi, rbj) using aux[][] 
// which is built by the preprocess function 
int sumQuery(int aux[M][N], int tli, int tlj, int rbi, 
                                              int rbj) 
{ 
    // result is now sum of elements between (0, 0) and 
    // (rbi, rbj) 
    int res = aux[rbi][rbj]; 

    // Remove elements between (0, 0) and (tli-1, rbj) 
    if (tli > 0) 
       res = res - aux[tli-1][rbj]; 

    // Remove elements between (0, 0) and (rbi, tlj-1) 
    if (tlj > 0) 
       res = res - aux[rbi][tlj-1]; 

    // Add aux[tli-1][tlj-1] as elements between (0, 0) 
    // and (tli-1, tlj-1) are subtracted twice 
    if (tli > 0 && tlj > 0) 
       res = res + aux[tli-1][tlj-1]; 

    return res; 
} 

// Driver program 
int main() 
{ 
   int mat[M][N] = {{1, 2, 3, 4, 6}, 
                    {5, 3, 8, 1, 2}, 
                    {4, 6, 7, 5, 5}, 
                    {2, 4, 8, 9, 4} }; 
   int aux[M][N]; 

   preProcess(mat, aux); 

   int tli = 2, tlj = 2, rbi = 3, rbj = 4; 
   cout << "\nQuery1: " << sumQuery(aux, tli, tlj, rbi, rbj); 

   tli = 0, tlj = 0, rbi = 1, rbj = 1; 
   cout << "\nQuery2: " << sumQuery(aux, tli, tlj, rbi, rbj); 

   tli = 1, tlj = 2, rbi = 3, rbj = 3; 
   cout << "\nQuery3: " << sumQuery(aux, tli, tlj, rbi, rbj); 

   return 0; 
} 

```

## Java

```java

// Java program to compute submatrix query  
// sum in O(1) time 
class GFG { 

    static final int M = 4; 
    static final int N = 5; 

    // Function to preprcess input mat[M][N].  
    // This function mainly fills aux[M][N]  
    // such that aux[i][j] stores sum of  
    // elements from (0,0) to (i,j) 
    static int preProcess(int mat[][], int aux[][]) 
    { 

        // Copy first row of mat[][] to aux[][] 
        for (int i = 0; i < N; i++) 
            aux[0][i] = mat[0][i]; 

        // Do column wise sum 
        for (int i = 1; i < M; i++) 
            for (int j = 0; j < N; j++) 
                aux[i][j] = mat[i][j] +  
                                aux[i-1][j]; 

        // Do row wise sum 
        for (int i = 0; i < M; i++) 
            for (int j = 1; j < N; j++) 
                aux[i][j] += aux[i][j-1]; 

        return 0; 
    } 

    // A O(1) time function to compute sum  
    // of submatrix between (tli, tlj) and  
    // (rbi, rbj) using aux[][] which is  
    // built by the preprocess function 
    static int sumQuery(int aux[][], int tli,  
                    int tlj, int rbi, int rbj) 
    { 

        // result is now sum of elements  
        // between (0, 0) and (rbi, rbj) 
        int res = aux[rbi][rbj]; 

        // Remove elements between (0, 0)  
        // and (tli-1, rbj) 
        if (tli > 0) 
            res = res - aux[tli-1][rbj]; 

        // Remove elements between (0, 0)  
        // and (rbi, tlj-1) 
        if (tlj > 0) 
            res = res - aux[rbi][tlj-1]; 

        // Add aux[tli-1][tlj-1] as elements  
        // between (0, 0) and (tli-1, tlj-1)  
        // are subtracted twice 
        if (tli > 0 && tlj > 0) 
            res = res + aux[tli-1][tlj-1]; 

        return res; 
    } 

    // Driver code 
    public static void main (String[] args) 
    { 
        int mat[][] = {{1, 2, 3, 4, 6}, 
                       {5, 3, 8, 1, 2}, 
                       {4, 6, 7, 5, 5}, 
                       {2, 4, 8, 9, 4}}; 

        int aux[][] = new int[M][N]; 

        preProcess(mat, aux); 

        int tli = 2, tlj = 2, rbi = 3, rbj = 4; 
        System.out.print("\nQuery1: "
            + sumQuery(aux, tli, tlj, rbi, rbj)); 

        tli = 0; tlj = 0; rbi = 1; rbj = 1; 
        System.out.print("\nQuery2: "
            + sumQuery(aux, tli, tlj, rbi, rbj)); 

        tli = 1; tlj = 2; rbi = 3; rbj = 3; 
        System.out.print("\nQuery3: " 
            + sumQuery(aux, tli, tlj, rbi, rbj)); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python 3 program to compute submatrix  
# query sum in O(1) time 

M = 4
N = 5

# Function to preprcess input mat[M][N].  
# This function mainly fills aux[M][N] 
# such that aux[i][j] stores sum 
# of elements from (0,0) to (i,j) 
def preProcess(mat, aux): 

    # Copy first row of mat[][] to aux[][] 
    for i in range(0, N, 1): 
        aux[0][i] = mat[0][i] 

    # Do column wise sum 
    for i in range(1, M, 1): 
        for j in range(0, N, 1): 
            aux[i][j] = mat[i][j] + aux[i - 1][j] 

    # Do row wise sum 
    for i in range(0, M, 1): 
        for j in range(1, N, 1): 
            aux[i][j] += aux[i][j - 1] 

# A O(1) time function to compute sum of submatrix 
# between (tli, tlj) and (rbi, rbj) using aux[][] 
# which is built by the preprocess function 
def sumQuery(aux, tli, tlj, rbi, rbj): 

    # result is now sum of elements  
    # between (0, 0) and (rbi, rbj) 
    res = aux[rbi][rbj] 

    # Remove elements between (0, 0) 
    # and (tli-1, rbj) 
    if (tli > 0): 
        res = res - aux[tli - 1][rbj] 

    # Remove elements between (0, 0) 
    # and (rbi, tlj-1) 
    if (tlj > 0): 
        res = res - aux[rbi][tlj - 1] 

    # Add aux[tli-1][tlj-1] as elements 
    # between (0, 0) and (tli-1, tlj-1) 
    # are subtracted twice 
    if (tli > 0 and tlj > 0): 
        res = res + aux[tli - 1][tlj - 1] 

    return res 

# Driver Code 
if __name__ == '__main__': 
    mat = [[1, 2, 3, 4, 6], 
           [5, 3, 8, 1, 2], 
           [4, 6, 7, 5, 5], 
           [2, 4, 8, 9, 4]] 
aux = [[0 for i in range(N)]  
          for j in range(M)] 

preProcess(mat, aux) 

tli = 2
tlj = 2
rbi = 3
rbj = 4
print("Query1:", sumQuery(aux, tli, tlj, rbi, rbj)) 

tli = 0
tlj = 0
rbi = 1
rbj = 1
print("Query2:", sumQuery(aux, tli, tlj, rbi, rbj)) 

tli = 1
tlj = 2
rbi = 3
rbj = 3
print("Query3:", sumQuery(aux, tli, tlj, rbi, rbj)) 

# This code is contributed by 
# Shashank_Sharma 

```

## C# 

```cs

// C# program to compute submatrix  
// query sum in O(1) time 
using System; 

class GFG 
{  
    static int M = 4; 
    static int N = 5; 

    // Function to preprcess input mat[M][N].  
    // This function mainly fills aux[M][N]  
    // such that aux[i][j] stores sum of  
    // elements from (0,0) to (i,j) 
    static int preProcess(int [,]mat, int [,]aux) 
    { 
        // Copy first row of mat[][] to aux[][] 
        for (int i = 0; i < N; i++) 
            aux[0,i] = mat[0,i]; 

        // Do column wise sum 
        for (int i = 1; i < M; i++) 
            for (int j = 0; j < N; j++) 
                aux[i,j] = mat[i,j] + aux[i-1,j]; 

        // Do row wise sum 
        for (int i = 0; i < M; i++) 
            for (int j = 1; j < N; j++) 
                aux[i,j] += aux[i,j-1]; 

        return 0; 
    } 

    // A O(1) time function to compute sum  
    // of submatrix between (tli, tlj) and  
    // (rbi, rbj) using aux[][] which is  
    // built by the preprocess function 
    static int sumQuery(int [,]aux, int tli,  
                        int tlj, int rbi, int rbj) 
    { 
        // result is now sum of elements  
        // between (0, 0) and (rbi, rbj) 
        int res = aux[rbi,rbj]; 

        // Remove elements between (0, 0)  
        // and (tli-1, rbj) 
        if (tli > 0) 
            res = res - aux[tli-1,rbj]; 

        // Remove elements between (0, 0)  
        // and (rbi, tlj-1) 
        if (tlj > 0) 
            res = res - aux[rbi,tlj-1]; 

        // Add aux[tli-1][tlj-1] as elements  
        // between (0, 0) and (tli-1, tlj-1)  
        // are subtracted twice 
        if (tli > 0 && tlj > 0) 
            res = res + aux[tli-1,tlj-1]; 

        return res; 
    } 

    // Driver code 
    public static void Main () 
    { 
        int [,]mat = {{1, 2, 3, 4, 6}, 
                      {5, 3, 8, 1, 2}, 
                      {4, 6, 7, 5, 5}, 
                      {2, 4, 8, 9, 4}}; 

        int [,]aux = new int[M,N]; 

        preProcess(mat, aux); 

        int tli = 2, tlj = 2, rbi = 3, rbj = 4; 

        Console.Write("\nQuery1: " +  
                      sumQuery(aux, tli, tlj, rbi, rbj)); 

        tli = 0; tlj = 0; rbi = 1; rbj = 1; 

        Console.Write("\nQuery2: " + 
                      sumQuery(aux, tli, tlj, rbi, rbj)); 

        tli = 1; tlj = 2; rbi = 3; rbj = 3; 

        Console.Write("\nQuery3: " +  
                      sumQuery(aux, tli, tlj, rbi, rbj)); 
    } 
} 

// This code is contributed by Sam007\. 

```

## PHP

```php

<?php 
// PHP program to compute submatrix  
// query sum in O(1) time 

// Function to preprcess input mat[M][N].  
// This function mainly fills aux[M][N]  
// such that aux[i][j] stores sum 
// of elements from (0,0) to (i,j) 
function preProcess(&$mat, &$aux) 
{ 
    $M = 4; 
    $N = 5; 

    // Copy first row of mat[][] to aux[][] 
    for ($i = 0; $i < $N; $i++) 
        $aux[0][$i] = $mat[0][$i]; 

    // Do column wise sum 
    for ($i = 1; $i < $M; $i++) 
        for ($j = 0; $j < $N; $j++) 
            $aux[$i][$j] = $mat[$i][$j] + 
                           $aux[$i - 1][$j]; 

    // Do row wise sum 
    for ($i = 0; $i < $M; $i++) 
        for ($j = 1; $j < $N; $j++) 
            $aux[$i][$j] += $aux[$i][$j - 1]; 
} 

// A O(1) time function to compute sum of  
// submatrix between (tli, tlj) and  
// (rbi, rbj) using aux[][] which is built  
// by the preprocess function 
function sumQuery(&$aux, $tli, $tlj, $rbi,$rbj) 
{ 
    // result is now sum of elements  
    // between (0, 0) and (rbi, rbj) 
    $res = $aux[$rbi][$rbj]; 

    // Remove elements between (0, 0)  
    // and (tli-1, rbj) 
    if ($tli > 0) 
    $res = $res - $aux[$tli - 1][$rbj]; 

    // Remove elements between (0, 0) 
    // and (rbi, tlj-1) 
    if ($tlj > 0) 
    $res = $res - $aux[$rbi][$tlj - 1]; 

    // Add aux[tli-1][tlj-1] as elements between (0, 0) 
    // and (tli-1, tlj-1) are subtracted twice 
    if ($tli > 0 && $tlj > 0) 
    $res = $res + $aux[$tli - 1][$tlj - 1]; 

    return $res; 
} 

// Driver Code 
$mat = array(array(1, 2, 3, 4, 6), 
             array(5, 3, 8, 1, 2), 
             array(4, 6, 7, 5, 5), 
             array(2, 4, 8, 9, 4)); 

preProcess($mat, $aux); 

$tli = 2; 
$tlj = 2; 
$rbi = 3; 
$rbj = 4; 
echo ("Query1: "); 
echo(sumQuery($aux, $tli, $tlj, $rbi, $rbj)); 

$tli = 0; 
$tlj = 0; 
$rbi = 1; 
$rbj = 1; 
echo ("\nQuery2: "); 
echo(sumQuery($aux, $tli, $tlj, $rbi, $rbj)); 

$tli = 1; 
$tlj = 2; 
$rbi = 3; 
$rbj = 3; 
echo ("\nQuery3: "); 
echo(sumQuery($aux, $tli, $tlj, $rbi, $rbj)); 

// This code is contributed by Shivi_Aggarwal 
?> 

```

**输出**：

```
Query1: 38
Query2: 11
Query3: 38
```

资料来源： [https://www.geeksforgeeks.org/amazon-interview-experience-set-241-1-5-years-experience/](https://www.geeksforgeeks.org/amazon-interview-experience-set-241-1-5-years-experience/)

