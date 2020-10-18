# 在给定约束条件下找到矩阵中的最长路径

> 原文： [https://www.geeksforgeeks.org/find-the-longest-path-in-a-matrix-with-given-constraints/](https://www.geeksforgeeks.org/find-the-longest-path-in-a-matrix-with-given-constraints/)

给定一个`n * n`矩阵，其中所有数字都是不同的，请找到最大长度路径（从任何单元格开始），以使该路径上的所有单元格都以递增顺序排列，相差 1。

我们可以从给定的单元格`(i, j)`向 4 个方向移动，即我们可以移动到`(i + 1, j)`或`(i, j + 1)`或`(i - 1, j)`或`(i, j - 1)`，条件是相邻单元格的差为 1。

**示例**：

```
Input:  mat[][] = {{1, 2, 9}
                   {5, 3, 8}
                   {4, 6, 7}}
Output: 4
The longest path is 6-7-8-9\. 

```



这个想法很简单，我们计算从每个单元格开始的最长路径。 一旦计算出所有单元格的最长，就返回所有最长路径的最大值。 这种方法的一个重要发现是许多重叠的子问题。 因此，可以使用动态规划来最佳解决该问题。

以下是基于动态规划的实现，该实现使用查找表`dp[][]`来检查问题是否已解决。

## C/C++ 

```

// C++ program to find the longest path in a matrix 
// with given constraints 
#include <bits/stdc++.h> 
#define n 3 
using namespace std; 

// Returns length of the longest path beginning with mat[i][j]. 
// This function mainly uses lookup table dp[n][n] 
int findLongestFromACell(int i, int j, int mat[n][n], int dp[n][n]) 
{ 
    if (i < 0 || i >= n || j < 0 || j >= n) 
        return 0; 

    // If this subproblem is already solved 
    if (dp[i][j] != -1) 
        return dp[i][j]; 

    // To store the path lengths in all the four directions 
    int x = INT_MIN, y = INT_MIN, z = INT_MIN, w = INT_MIN; 

    // Since all numbers are unique and in range from 1 to n*n, 
    // there is atmost one possible direction from any cell 
    if (j < n - 1 && ((mat[i][j] + 1) == mat[i][j + 1])) 
        x = 1 + findLongestFromACell(i, j + 1, mat, dp); 

    if (j > 0 && (mat[i][j] + 1 == mat[i][j - 1])) 
        y = 1 + findLongestFromACell(i, j - 1, mat, dp); 

    if (i > 0 && (mat[i][j] + 1 == mat[i - 1][j])) 
        z = 1 + findLongestFromACell(i - 1, j, mat, dp); 

    if (i < n - 1 && (mat[i][j] + 1 == mat[i + 1][j])) 
        w = 1 + findLongestFromACell(i + 1, j, mat, dp); 

    // If none of the adjacent fours is one greater we will take 1 
    // otherwise we will pick maximum from all the four directions 
    return dp[i][j] = max(x, max(y, max(z, max(w, 1)))); 
} 

// Returns length of the longest path beginning with any cell 
int finLongestOverAll(int mat[n][n]) 
{ 
    int result = 1; // Initialize result 

    // Create a lookup table and fill all entries in it as -1 
    int dp[n][n]; 
    memset(dp, -1, sizeof dp); 

    // Compute longest path beginning from all cells 
    for (int i = 0; i < n; i++) { 
        for (int j = 0; j < n; j++) { 
            if (dp[i][j] == -1) 
                findLongestFromACell(i, j, mat, dp); 

            // Update result if needed 
            result = max(result, dp[i][j]); 
        } 
    } 

    return result; 
} 

// Driver program 
int main() 
{ 
    int mat[n][n] = { { 1, 2, 9 }, 
                      { 5, 3, 8 }, 
                      { 4, 6, 7 } }; 
    cout << "Length of the longest path is "
         << finLongestOverAll(mat); 
    return 0; 
} 

```

## Java

```java

// Java program to find the longest path in a matrix 
// with given constraints 

class GFG { 
    public static int n = 3; 

    // Function that returns length of the longest path 
    // beginning with mat[i][j] 
    // This function mainly uses lookup table dp[n][n] 
    static int findLongestFromACell(int i, int j, int mat[][], int dp[][]) 
    { 
        // Base case 
        if (i < 0 || i >= n || j < 0 || j >= n) 
            return 0; 

        // If this subproblem is already solved 
        if (dp[i][j] != -1) 
            return dp[i][j]; 

        // To store the path lengths in all the four directions 
        int x = Integer.MIN_VALUE, y = Integer.MIN_VALUE, z = Integer.MIN_VALUE, w = Integer.MIN_VALUE; 
        // Since all numbers are unique and in range from 1 to n*n, 
        // there is atmost one possible direction from any cell 
        if (j < n - 1 && ((mat[i][j] + 1) == mat[i][j + 1])) 
            x = dp[i][j] = 1 + findLongestFromACell(i, j + 1, mat, dp); 

        if (j > 0 && (mat[i][j] + 1 == mat[i][j - 1])) 
            y = dp[i][j] = 1 + findLongestFromACell(i, j - 1, mat, dp); 

        if (i > 0 && (mat[i][j] + 1 == mat[i - 1][j])) 
            z = dp[i][j] = 1 + findLongestFromACell(i - 1, j, mat, dp); 

        if (i < n - 1 && (mat[i][j] + 1 == mat[i + 1][j])) 
            w = dp[i][j] = 1 + findLongestFromACell(i + 1, j, mat, dp); 

        // If none of the adjacent fours is one greater we will take 1 
        // otherwise we will pick maximum from all the four directions 
        return dp[i][j] = Math.max(x, Math.max(y, Math.max(z, Math.max(w, 1)))); 
    } 

    // Function that returns length of the longest path 
    // beginning with any cell 
    static int finLongestOverAll(int mat[][]) 
    { 
        // Initialize result 
        int result = 1; 

        // Create a lookup table and fill all entries in it as -1 
        int[][] dp = new int[n][n]; 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < n; j++) 
                dp[i][j] = -1; 

        // Compute longest path beginning from all cells 
        for (int i = 0; i < n; i++) { 
            for (int j = 0; j < n; j++) { 
                if (dp[i][j] == -1) 
                    findLongestFromACell(i, j, mat, dp); 

                // Update result if needed 
                result = Math.max(result, dp[i][j]); 
            } 
        } 

        return result; 
    } 

    // driver program 
    public static void main(String[] args) 
    { 
        int mat[][] = { { 1, 2, 9 }, 
                        { 5, 3, 8 }, 
                        { 4, 6, 7 } }; 
        System.out.println("Length of the longest path is " + finLongestOverAll(mat)); 
    } 
} 

// Contributed by Pramod Kumar 

```

## Python3

```py

# Python3 program to find the longest path in a matrix 
# with given constraints 

n = 3
# Returns length of the longest path beginning with mat[i][j].  
# This function mainly uses lookup table dp[n][n]  
def findLongestFromACell(i, j, mat, dp): 
    # Base case  
    if (i<0 or i>= n or j<0 or j>= n): 
        return 0

    # If this subproblem is already solved  
    if (dp[i][j] != -1):  
        return dp[i][j] 

    # To store the path lengths in all the four directions 
    x, y, z, w = -1, -1, -1, -1

    # Since all numbers are unique and in range from 1 to n * n,  
    # there is atmost one possible direction from any cell  
    if (j<n-1 and ((mat[i][j] +1) == mat[i][j + 1])): 
        x = 1 + findLongestFromACell(i, j + 1, mat, dp) 

    if (j>0 and (mat[i][j] +1 == mat[i][j-1])):  
        y = 1 + findLongestFromACell(i, j-1, mat, dp) 

    if (i>0 and (mat[i][j] +1 == mat[i-1][j])): 
        z = 1 + findLongestFromACell(i-1, j, mat, dp) 

    if (i<n-1 and (mat[i][j] +1 == mat[i + 1][j])): 
        w = 1 + findLongestFromACell(i + 1, j, mat, dp) 

    # If none of the adjacent fours is one greater we will take 1 
    # otherwise we will pick maximum from all the four directions 
    dp[i][j] = max(x, max(y, max(z, max(w, 1)))) 
    return dp[i][j] 

# Returns length of the longest path beginning with any cell  
def finLongestOverAll(mat): 
    result = 1 # Initialize result  

    # Create a lookup table and fill all entries in it as -1  
    dp =[[-1 for i in range(n)]for i in range(n)] 

    # Compute longest path beginning from all cells  
    for i in range(n): 
        for j in range(n): 
            if (dp[i][j] == -1): 
                findLongestFromACell(i, j, mat, dp) 
            # Update result if needed  
            result = max(result, dp[i][j]);  
    return result 

# Driver program  
mat = [[1, 2, 9],  
    [5, 3, 8], 
    [4, 6, 7]]  
print("Length of the longest path is ", finLongestOverAll(mat)) 

# this code is improved by sahilshelangia 

```

## C# 

```cs

// C# program to find the longest path 
// in a matrix with given constraints 
using System; 

class GFG { 
    public static int n = 3; 

    // Function that returns length of 
    // the longest path beginning with mat[i][j] 
    // This function mainly uses lookup 
    // table dp[n][n] 
    public static int findLongestFromACell(int i, int j, 
                                           int[][] mat, 
                                           int[][] dp) 
    { 
        // Base case 
        if (i < 0 || i >= n || j < 0 || j >= n) { 
            return 0; 
        } 

        // If this subproblem is 
        // already solved 
        if (dp[i][j] != -1) { 
            return dp[i][j]; 
        } 

        // To store the path lengths in all the four directions 
        int x = int.MinValue, y = int.MinValue, z = int.MinValue, w = int.MinValue; 

        // Since all numbers are unique and 
        // in range from 1 to n*n, there is 
        // atmost one possible direction 
        // from any cell 
        if (j < n - 1 && ((mat[i][j] + 1) == mat[i][j + 1])) { 
            x = dp[i][j] = 1 + findLongestFromACell(i, j + 1, mat, dp); 
        } 

        if (j > 0 && (mat[i][j] + 1 == mat[i][j - 1])) { 
            y = dp[i][j] = 1 + findLongestFromACell(i, j - 1, mat, dp); 
        } 

        if (i > 0 && (mat[i][j] + 1 == mat[i - 1][j])) { 
            z = dp[i][j] = 1 + findLongestFromACell(i - 1, j, mat, dp); 
        } 

        if (i < n - 1 && (mat[i][j] + 1 == mat[i + 1][j])) { 
            w = dp[i][j] = 1 + findLongestFromACell(i + 1, j, mat, dp); 
        } 

        // If none of the adjacent fours is one greater we will take 1 
        // otherwise we will pick maximum from all the four directions 
        dp[i][j] = Math.Max(x, Math.Max(y, Math.Max(z, Math.Max(w, 1)))); 
        return dp[i][j]; 
    } 

    // Function that returns length of the 
    // longest path beginning with any cell 
    public static int finLongestOverAll(int[][] mat) 
    { 
        // Initialize result 
        int result = 1; 

        // Create a lookup table and fill 
        // all entries in it as -1 
        int[][] dp = RectangularArrays.ReturnRectangularIntArray(n, n); 
        for (int i = 0; i < n; i++) { 
            for (int j = 0; j < n; j++) { 
                dp[i][j] = -1; 
            } 
        } 

        // Compute longest path beginning 
        // from all cells 
        for (int i = 0; i < n; i++) { 
            for (int j = 0; j < n; j++) { 
                if (dp[i][j] == -1) { 
                    findLongestFromACell(i, j, mat, dp); 
                } 

                // Update result if needed 
                result = Math.Max(result, dp[i][j]); 
            } 
        } 

        return result; 
    } 

    public static class RectangularArrays { 
        public static int[][] ReturnRectangularIntArray(int size1, 
                                                        int size2) 
        { 
            int[][] newArray = new int[size1][]; 
            for (int array1 = 0; 
                 array1 < size1; array1++) { 
                newArray[array1] = new int[size2]; 
            } 

            return newArray; 
        } 
    } 

    // Driver Code 
    public static void Main(string[] args) 
    { 
        int[][] mat = new int[][] { 
            new int[] { 1, 2, 9 }, 
            new int[] { 5, 3, 8 }, 
            new int[] { 4, 6, 7 } 
        }; 
        Console.WriteLine("Length of the longest path is " + finLongestOverAll(mat)); 
    } 
} 

// This code is contributed by Shrikant13 

```

**输出**：

```
Length of the longest path is 4
```

上述解决方案的时间复杂度为 `O(n^2)`。 乍看起来似乎更多。 如果仔细观察，我们会发现`dp[i][j]`的所有值仅计算一次。



