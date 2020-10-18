# 矩阵秩程序

> 原文： [https://www.geeksforgeeks.org/program-for-rank-of-matrix/](https://www.geeksforgeeks.org/program-for-rank-of-matrix/)

**矩阵的秩是多少？**

大小为`M x N`的矩阵`A`的秩定义为：

1.  矩阵中线性独立列向量的最大数量。

2.  矩阵中线性独立行向量的最大数量。

示例：

```
Input:  mat[][] = {{10,   20,   10},
                   {20,   40,   20},
                   {30,   50,   0}}
Output: Rank is 2
Explanation: Ist and IInd rows are linearly dependent.
             But Ist and  3rd or IInd and IIIrd  are
             independent.   

Input:  mat[][] = {{10,   20,   10},
                   {-20, -30,   10},
                   {30,   50,   0}}
Output: Rank is 2
Explanation: Ist and IInd rows are linearly independent.
             So rank must be atleast 2\. But all three rows
             are linearly dependent (the first is equal to
             the sum of the second and third) so the rank 
             must be less than 3\. 

```

换句话说，`A`的秩是`A`中任何非零未成年人的最大阶，其中次幂的阶次是确定它的平方子矩阵的边长。

因此，如果`M < N`，则`A`的最大秩可以为`M`，否则可以为`N`，通常矩阵的秩不能大于`min(M, N)`。

仅当矩阵不包含非零元素时，矩阵的秩才会为零。 如果矩阵甚至具有一个非零元素，则其最小秩为 1。

**如何找到秩？**

这个想法是基于转换为[行梯形形式](https://en.wikipedia.org/wiki/Row_echelon_form)。

```
1) Let the input matrix be mat[][].  Initialize rank equals
   to number of columns

// Before we visit row 'row',  traversal of previous 
// rows make sure that mat[row][0],....mat[row][row-1]
// are 0.
2) Do following for row = 0 to rank-1.

  a) If mat[row][row] is not zero, make all elements of
     current column as 0 except the element mat[row][row]
     by finding appropriate multiplier and adding a the 
     multiple of row 'row'

  b) Else (mat[row][row] is zero). Two cases arise:
       (i) If there is a row below it with non-zero entry in 
           same column, then swap current 'row' and that row.
       (ii) If all elements in current column below mat[r][row] 
            are 0, then remove this column by swapping it with
            last column and  reducing number of rank by 1.
     Reduce row by 1 so that this row is processed again.

3) Number of remaining columns is rank of matrix.

```

例：

```
Input:  mat[][] = {{10,   20,   10},
                   {-20, -30,   10},
                   {30,   50,   0}}

row = 0:
Since mat[0][0] is not 0, we are in case 2.a of above algorithm.
We set all entries of 0'th column as 0 (except entry mat[0][0]).
To do this, we subtract R1*(-2) from R2, i.e., R2 --> R2 - R1*(-2)
         mat[][] = {{10,   20,   10},
                   { 0,    10,   30},
                    {30,   50,   0}}
            And subtract R1*3 from R3, i.e., R3   --> R3 - R1*3  
         mat[][] = {{10,   20,   10},
                    { 0,   10,   30},
                    { 0,  -10,  -30}}

row = 1:
Since mat[1][1] is not 0, we are in case 2.a of above algorithm.
We set all entries of 1st column as 0 (except entry mat[1][1]).
To do this, we subtract R2*2 from R1, i.e., R1 --> R1 - R2*2
         mat[][] = {{10,    0,  -50},
                    { 0,   10,   30},
                    { 0,  -10,  -30}}
           And subtract R2*(-1) from R3, i.e., R3   --> R3 - R2*(-1)
         mat[][] = {{10,   0,   -50},
                    { 0,   10,   30},
                    { 0,   0,     0}}

row = 2:
Since Since mat[2][2] is 0, we are in case 2.b of above algorithm.
Since there is no row below it swap. We reduce the rank by 1 and 
keep row as 2\. 

The loop doesn't iterate next time because loop termination condition
row <= rank-1 returns false.

```

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to find rank of a matrix 
#include <bits/stdc++.h> 
using namespace std; 
#define R 3 
#define C 3 

/* function for exchanging two rows of 
   a matrix */
void swap(int mat[R][C], int row1, int row2, 
          int col) 
{ 
    for (int i = 0; i < col; i++) 
    { 
        int temp = mat[row1][i]; 
        mat[row1][i] = mat[row2][i]; 
        mat[row2][i] = temp; 
    } 
} 

// Function to display a matrix 
void display(int mat[R][C], int row, int col); 

/* function for finding rank of matrix */
int rankOfMatrix(int mat[R][C]) 
{ 
    int rank = C; 

    for (int row = 0; row < rank; row++) 
    { 
        // Before we visit current row 'row', we make 
        // sure that mat[row][0],....mat[row][row-1] 
        // are 0\. 

        // Diagonal element is not zero 
        if (mat[row][row]) 
        { 
           for (int col = 0; col < R; col++) 
           { 
               if (col != row) 
               { 
                 // This makes all entries of current 
                 // column as 0 except entry 'mat[row][row]' 
                 double mult = (double)mat[col][row] / 
                                       mat[row][row]; 
                 for (int i = 0; i < rank; i++) 
                   mat[col][i] -= mult * mat[row][i]; 
              } 
           } 
        } 

        // Diagonal element is already zero. Two cases 
        // arise: 
        // 1) If there is a row below it with non-zero 
        //    entry, then swap this row with that row 
        //    and process that row 
        // 2) If all elements in current column below 
        //    mat[r][row] are 0, then remvoe this column 
        //    by swapping it with last column and 
        //    reducing number of columns by 1\. 
        else
        { 
            bool reduce = true; 

            /* Find the non-zero element in current 
                column  */
            for (int i = row + 1; i < R;  i++) 
            { 
                // Swap the row with non-zero element 
                // with this row. 
                if (mat[i][row]) 
                { 
                    swap(mat, row, i, rank); 
                    reduce = false; 
                    break ; 
                } 
            } 

            // If we did not find any row with non-zero 
            // element in current columnm, then all 
            // values in this column are 0\. 
            if (reduce) 
            { 
                // Reduce number of columns 
                rank--; 

                // Copy the last column here 
                for (int i = 0; i < R; i ++) 
                    mat[i][row] = mat[i][rank]; 
            } 

            // Process this row again 
            row--; 
        } 

       // Uncomment these lines to see intermediate results 
       // display(mat, R, C); 
       // printf("\n"); 
    } 
    return rank; 
} 

/* function for displaying the matrix */
void display(int mat[R][C], int row, int col) 
{ 
    for (int i = 0; i < row; i++) 
    { 
        for (int j = 0; j < col; j++) 
            printf("  %d", mat[i][j]); 
        printf("\n"); 
    } 
} 

// Driver program to test above functions 
int main() 
{ 
   int mat[][3] = {{10,   20,   10}, 
                  {-20,  -30,   10}, 
                   {30,   50,   0}}; 
    printf("Rank of the matrix is : %d", 
         rankOfMatrix(mat)); 
    return 0; 
} 

```

## Java

```java

// Java program to find rank of a matrix 
class GFG { 

    static final int R = 3; 
    static final int C = 3; 

    // function for exchanging two rows 
    // of a matrix  
    static void swap(int mat[][],  
          int row1, int row2, int col) 
    { 
        for (int i = 0; i < col; i++) 
        { 
            int temp = mat[row1][i]; 
            mat[row1][i] = mat[row2][i]; 
            mat[row2][i] = temp; 
        } 
    } 

    // Function to display a matrix 
    static void display(int mat[][],  
                     int row, int col) 
    { 
        for (int i = 0; i < row; i++) 
        { 

            for (int j = 0; j < col; j++) 

                System.out.print(" "
                          + mat[i][j]); 

            System.out.print("\n"); 
        } 
    }  

    // function for finding rank of matrix  
    static int rankOfMatrix(int mat[][]) 
    { 

        int rank = C; 

        for (int row = 0; row < rank; row++) 
        { 

            // Before we visit current row  
            // 'row', we make sure that  
            // mat[row][0],....mat[row][row-1] 
            // are 0\. 

            // Diagonal element is not zero 
            if (mat[row][row] != 0) 
            { 
                for (int col = 0; col < R; col++) 
                { 
                    if (col != row) 
                    { 
                        // This makes all entries  
                        // of current column  
                        // as 0 except entry  
                        // 'mat[row][row]' 
                        double mult =  
                           (double)mat[col][row] / 
                                    mat[row][row]; 

                        for (int i = 0; i < rank; i++) 

                            mat[col][i] -= mult  
                                       * mat[row][i]; 
                    } 
                } 
            } 

            // Diagonal element is already zero.  
            // Two cases arise: 
            // 1) If there is a row below it  
            // with non-zero entry, then swap  
            // this row with that row and process  
            // that row 
            // 2) If all elements in current  
            // column below mat[r][row] are 0,  
            // then remvoe this column by  
            // swapping it with last column and 
            // reducing number of columns by 1\. 
            else
            { 
                boolean reduce = true; 

                // Find the non-zero element  
                // in current column  
                for (int i = row + 1; i < R; i++) 
                { 
                    // Swap the row with non-zero  
                    // element with this row. 
                    if (mat[i][row] != 0) 
                    { 
                        swap(mat, row, i, rank); 
                        reduce = false; 
                        break ; 
                    } 
                } 

                // If we did not find any row with  
                // non-zero element in current  
                // columnm, then all values in  
                // this column are 0\. 
                if (reduce) 
                { 
                    // Reduce number of columns 
                    rank--; 

                    // Copy the last column here 
                    for (int i = 0; i < R; i ++) 
                        mat[i][row] = mat[i][rank]; 
                } 

                // Process this row again 
                row--; 
            } 

        // Uncomment these lines to see  
        // intermediate results display(mat, R, C); 
        // printf("\n"); 
        } 

        return rank; 
    } 

    // Driver code 
    public static void main (String[] args) 
    { 
        int mat[][] = {{10, 20, 10}, 
                       {-20, -30, 10}, 
                       {30, 50, 0}}; 

        System.out.print("Rank of the matrix is : " 
                               + rankOfMatrix(mat)); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python 3 program to find rank of a matrix 
class rankMatrix(object): 
    def __init__(self, Matrix): 
        self.R = len(Matrix) 
        self.C = len(Matrix[0]) 

    # Function for exchanging two rows of a matrix 
    def swap(self, Matrix, row1, row2, col): 
        for i in range(col): 
            temp = Matrix[row1][i] 
            Matrix[row1][i] = Matrix[row2][i] 
            Matrix[row2][i] = temp 

    # Function to Display a matrix 
    def Display(self, Matrix, row, col): 
        for i in range(row): 
            for j in range(col): 
                print (" " + str(Matrix[i][j])) 
            print ('\n') 

    # Find rank of a matrix 
    def rankOfMatrix(self, Matrix): 
        rank = self.C 
        for row in range(0, rank, 1): 

            # Before we visit current row  
            # 'row', we make sure that  
            # mat[row][0],....mat[row][row-1]  
            # are 0.  

            # Diagonal element is not zero 
            if Matrix[row][row] != 0: 
                for col in range(0, self.R, 1): 
                    if col != row: 

                        # This makes all entries of current  
                        # column as 0 except entry 'mat[row][row]'  
                        multiplier = (Matrix[col][row] /
                                      Matrix[row][row]) 
                        for i in range(rank): 
                            Matrix[col][i] -= (multiplier *
                                               Matrix[row][i]) 

            # Diagonal element is already zero.  
            # Two cases arise:  
            # 1) If there is a row below it  
            # with non-zero entry, then swap  
            # this row with that row and process  
            # that row  
            # 2) If all elements in current  
            # column below mat[r][row] are 0,  
            # then remvoe this column by  
            # swapping it with last column and  
            # reducing number of columns by 1.  
            else: 
                reduce = True

                # Find the non-zero element  
                # in current column  
                for i in range(row + 1, self.R, 1): 

                    # Swap the row with non-zero  
                    # element with this row. 
                    if Matrix[i][row] != 0: 
                        self.swap(Matrix, row, i, rank) 
                        reduce = False
                        break

                # If we did not find any row with  
                # non-zero element in current  
                # columnm, then all values in  
                # this column are 0\. 
                if reduce: 

                    # Reduce number of columns  
                    rank -= 1

                    # copy the last column here 
                    for i in range(0, self.R, 1): 
                        Matrix[i][row] = Matrix[i][rank] 

                # process this row again 
                row -= 1

        # self.Display(Matrix, self.R,self.C)  
        return (rank) 

# Driver Code 
if __name__ == '__main__': 
    Matrix = [[10, 20, 10], 
              [-20, -30, 10], 
              [30, 50, 0]] 
    RankMatrix = rankMatrix(Matrix) 
    print ("Rank of the Matrix is:",  
           (RankMatrix.rankOfMatrix(Matrix))) 

# This code is contributed by Vikas Chitturi  

```

## C# 

```cs

// C# program to find rank of a matrix 
using System; 
class GFG { 

    static  int R = 3; 
    static  int C = 3; 

    // function for exchanging two rows 
    // of a matrix  
    static void swap(int [,]mat,  
          int row1, int row2, int col) 
    { 
        for (int i = 0; i < col; i++) 
        { 
            int temp = mat[row1,i]; 
            mat[row1,i] = mat[row2,i]; 
            mat[row2,i] = temp; 
        } 
    } 

    // Function to display a matrix 
    static void display(int [,]mat,  
                     int row, int col) 
    { 
        for (int i = 0; i < row; i++) 
        { 

            for (int j = 0; j < col; j++) 

                Console.Write(" "
                          + mat[i,j]); 

            Console.Write("\n"); 
        } 
    }  

    // function for finding rank of matrix  
    static int rankOfMatrix(int [,]mat) 
    { 

        int rank = C; 

        for (int row = 0; row < rank; row++) 
        { 

            // Before we visit current row  
            // 'row', we make sure that  
            // mat[row][0],....mat[row][row-1] 
            // are 0\. 

            // Diagonal element is not zero 
            if (mat[row,row] != 0) 
            { 
                for (int col = 0; col < R; col++) 
                { 
                    if (col != row) 
                    { 
                        // This makes all entries  
                        // of current column  
                        // as 0 except entry  
                        // 'mat[row][row]' 
                        double mult =  
                           (double)mat[col,row] / 
                                    mat[row,row]; 

                        for (int i = 0; i < rank; i++) 

                            mat[col,i] -= (int) mult 
                                     * mat[row,i]; 
                    } 
                } 
            } 

            // Diagonal element is already zero.  
            // Two cases arise: 
            // 1) If there is a row below it  
            // with non-zero entry, then swap  
            // this row with that row and process  
            // that row 
            // 2) If all elements in current  
            // column below mat[r][row] are 0,  
            // then remvoe this column by  
            // swapping it with last column and 
            // reducing number of columns by 1\. 
            else
            { 
                bool reduce = true; 

                // Find the non-zero element  
                // in current column  
                for (int i = row + 1; i < R; i++) 
                { 
                    // Swap the row with non-zero  
                    // element with this row. 
                    if (mat[i,row] != 0) 
                    { 
                        swap(mat, row, i, rank); 
                        reduce = false; 
                        break ; 
                    } 
                } 

                // If we did not find any row with  
                // non-zero element in current  
                // columnm, then all values in  
                // this column are 0\. 
                if (reduce) 
                { 
                    // Reduce number of columns 
                    rank--; 

                    // Copy the last column here 
                    for (int i = 0; i < R; i ++) 
                        mat[i,row] = mat[i,rank]; 
                } 

                // Process this row again 
                row--; 
            } 

        // Uncomment these lines to see  
        // intermediate results display(mat, R, C); 
        // printf("\n"); 
        } 

        return rank; 
    } 

    // Driver code 
    public static void Main () 
    { 
        int [,]mat = {{10, 20, 10}, 
                       {-20, -30, 10}, 
                       {30, 50, 0}}; 

        Console.Write("Rank of the matrix is : "
                          + rankOfMatrix(mat)); 
    } 
} 

// This code is contributed by nitin mittal 

```

## PHP

```php

<?php 
// PHP program to find rank of a matrix 

$R = 3; 
$C = 3; 

/* function for exchanging two rows of 
a matrix */
function swap(&$mat, $row1, $row2, $col) 
{ 
    for ($i = 0; $i < $col; $i++) 
    { 
        $temp = $mat[$row1][$i]; 
        $mat[$row1][$i] = $mat[$row2][$i]; 
        $mat[$row2][$i] = $temp; 
    } 
} 

/* function for finding rank of matrix */
function rankOfMatrix($mat) 
{ 
    global $R, $C; 
    $rank = $C; 

    for ($row = 0; $row < $rank; $row++) 
    { 
        // Before we visit current row 'row', we make 
        // sure that mat[row][0],....mat[row][row-1] 
        // are 0\. 

        // Diagonal element is not zero 
        if ($mat[$row][$row]) 
        { 
            for ($col = 0; $col < $R; $col++) 
            { 
                if ($col != $row) 
                { 
                    // This makes all entries of current 
                    // column as 0 except entry 'mat[row][row]' 
                    $mult = $mat[$col][$row] / $mat[$row][$row]; 
                    for ($i = 0; $i < $rank; $i++) 
                        $mat[$col][$i] -= $mult * $mat[$row][$i]; 
                } 
            } 
        } 

        // Diagonal element is already zero. Two cases 
        // arise: 
        // 1) If there is a row below it with non-zero 
        // entry, then swap this row with that row 
        // and process that row 
        // 2) If all elements in current column below 
        // mat[r][row] are 0, then remvoe this column 
        // by swapping it with last column and 
        // reducing number of columns by 1\. 
        else
        { 
            $reduce = true; 

            /* Find the non-zero element in current 
                column */
            for ($i = $row + 1; $i < $R; $i++) 
            { 
                // Swap the row with non-zero element 
                // with this row. 
                if ($mat[$i][$row]) 
                { 
                    swap($mat, $row, $i, $rank); 
                    $reduce = false; 
                    break ; 
                } 
            } 

            // If we did not find any row with non-zero 
            // element in current columnm, then all 
            // values in this column are 0\. 
            if ($reduce) 
            { 
                // Reduce number of columns 
                $rank--; 

                // Copy the last column here 
                for ($i = 0; $i < $R; $i++) 
                    $mat[$i][$row] = $mat[$i][$rank]; 
            } 

            // Process this row again 
            $row--; 
        } 

    // Uncomment these lines to see intermediate results 
    // display(mat, R, C); 
    // printf("\n"); 
    } 
    return $rank; 
} 

/* function for displaying the matrix */
function display($mat, $row, $col) 
{ 
    for ($i = 0; $i < $row; $i++) 
    { 
        for ($j = 0; $j < $col; $j++) 
            print(" $mat[$i][$j]"); 
        print("\n"); 
    } 
} 

// Driver code 
$mat = array(array(10, 20, 10), 
                array(-20, -30, 10), 
                array(30, 50, 0)); 
print("Rank of the matrix is : ".rankOfMatrix($mat)); 

// This code is contributed by mits 
?> 

```

**输出**：

```
Rank of the matrix is : 2
```

由于以上等级计算方法涉及浮点运算，因此如果除法超出精度，可能会产生错误的结果。 还有其他方法可以处理

**参考**：

[https://en.wikipedia.org/wiki/Rank_%28linear_algebra%29](https://en.wikipedia.org/wiki/Rank_%28linear_algebra%29)

