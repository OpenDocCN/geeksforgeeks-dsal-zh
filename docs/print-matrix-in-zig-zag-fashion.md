# 之字形打印矩阵

> 原文:[https://www . geesforgeks . org/print-matrix-in-zig-zag-fashion/](https://www.geeksforgeeks.org/print-matrix-in-zig-zag-fashion/)

给定 n 行 m 列的 2D 矩阵。如图所示，以 ZIG-ZIG 方式打印该矩阵。

![matrix_zag-zag](img/e7235d8f5a8d5cc0fb6c141fd6d523d1.png)

**例:**

```
Input: 
1 2 3
4 5 6
7 8 9
Output: 
1 2 4 7 5 3 6 8 9
```

**c++代码的方法**
方法很简单。只需一次迭代一个对角元素，并根据之前的匹配改变方向。
**蟒蛇 3 的方法代码**
这个方法很简单。当以通常的方式在矩阵中行进时，基于元素的索引的和的奇偶性，如果 I 和 j 的和分别是偶数或奇数，则将该特定元素添加到列表的开头或结尾。按原样打印解决方案列表。

## C++

```
/* C++ Program to print matrix in Zig-zag pattern*/
#include <iostream>
using namespace std;
#define C 3

// Utility function to print matrix
// in zig-zag form
void zigZagMatrix(int arr[][C], int n, int m)
{
    int row = 0, col = 0;

    // Boolean variable that will true if we
    // need to increment 'row' value otherwise
    // false- if increment 'col' value
    bool row_inc = 0;

    // Print matrix of lower half zig-zag pattern
    int mn = min(m, n);
    for (int len = 1; len <= mn; ++len) {
        for (int i = 0; i < len; ++i) {
            cout << arr[row][col] << " ";

            if (i + 1 == len)
                break;
            // If row_increment value is true
            // increment row and decrement col
            // else decrement row and increment
            // col
            if (row_inc)
                ++row, --col;
            else
                --row, ++col;
        }

        if (len == mn)
            break;

        // Update row or col value according
        // to the last increment
        if (row_inc)
            ++row, row_inc = false;
        else
            ++col, row_inc = true;
    }

    // Update the indexes of row and col variable
    if (row == 0) {
        if (col == m - 1)
            ++row;
        else
            ++col;
        row_inc = 1;
    }
    else {
        if (row == n - 1)
            ++col;
        else
            ++row;
        row_inc = 0;
    }

    // Print the next half zig-zag pattern
    int MAX = max(m, n) - 1;
    for (int len, diag = MAX; diag > 0; --diag) {

        if (diag > mn)
            len = mn;
        else
            len = diag;

        for (int i = 0; i < len; ++i) {
            cout << arr[row][col] << " ";

            if (i + 1 == len)
                break;

            // Update row or col value according
            // to the last increment
            if (row_inc)
                ++row, --col;
            else
                ++col, --row;
        }

        // Update the indexes of row and col variable
        if (row == 0 || col == m - 1) {
            if (col == m - 1)
                ++row;
            else
                ++col;

            row_inc = true;
        }

        else if (col == 0 || row == n - 1) {
            if (row == n - 1)
                ++col;
            else
                ++row;

            row_inc = false;
        }
    }
}

// Driver code
int main()
{
    int matrix[][3] = { { 1, 2, 3 },
                        { 4, 5, 6 },
                        { 7, 8, 9 } };
    zigZagMatrix(matrix, 3, 3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java Program to print matrix in Zig-zag pattern*/
class GFG {
  static final int C = 3;

  // Utility function to print matrix
  // in zig-zag form
  static void zigZagMatrix(int arr[][], int n, int m) {
    int row = 0, col = 0;

    // Boolean variable that will true if we
    // need to increment 'row' value otherwise
    // false- if increment 'col' value
    boolean row_inc = false;

    // Print matrix of lower half zig-zag pattern
    int mn = Math.min(m, n);
    for (int len = 1; len <= mn; ++len) {
      for (int i = 0; i < len; ++i) {
        System.out.print(arr[row][col] + " ");

        if (i + 1 == len)
          break;
        // If row_increment value is true
        // increment row and decrement col
        // else decrement row and increment
        // col
        if (row_inc) {
          ++row;
          --col;
        } else {
          --row;
          ++col;
        }
      }

      if (len == mn)
        break;

      // Update row or col value according
      // to the last increment
      if (row_inc) {
        ++row;
        row_inc = false;
      } else {
        ++col;
        row_inc = true;
      }
    }

    // Update the indexes of row and col variable
    if (row == 0) {
      if (col == m - 1)
        ++row;
      else
        ++col;
      row_inc = true;
    } else {
      if (row == n - 1)
        ++col;
      else
        ++row;
      row_inc = false;
    }

    // Print the next half zig-zag pattern
    int MAX = Math.max(m, n) - 1;
    for (int len, diag = MAX; diag > 0; --diag) {

      if (diag > mn)
        len = mn;
      else
        len = diag;

      for (int i = 0; i < len; ++i) {
        System.out.print(arr[row][col] + " ");

        if (i + 1 == len)
          break;

        // Update row or col value according
        // to the last increment
        if (row_inc) {
          ++row;
          --col;
        } else {
          ++col;
          --row;
        }
      }

      // Update the indexes of row and col variable
      if (row == 0 || col == m - 1) {
        if (col == m - 1)
          ++row;
        else
          ++col;

        row_inc = true;
      }

      else if (col == 0 || row == n - 1) {
        if (row == n - 1)
          ++col;
        else
          ++row;

        row_inc = false;
      }
    }
  }
  // Driver code
  public static void main(String[] args) {
    int matrix[][] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    zigZagMatrix(matrix, 3, 3);
  }
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Program to print matrix in Zig-zag pattern

matrix =[
            [ 1, 2, 3,],
            [ 4, 5, 6 ],
            [ 7, 8, 9 ],
        ]
rows=3
columns=3

solution=[[] for i in range(rows+columns-1)]

for i in range(rows):
    for j in range(columns):
        sum=i+j
        if(sum%2 ==0):

            #add at beginning
            solution[sum].insert(0,matrix[i][j])
        else:

            #add at end of the list
            solution[sum].append(matrix[i][j])

# print the solution as it as
for i in solution:
    for j in i:
        print(j,end=" ")

```

## C#

```
// C# Program to print matrix
// in Zig-zag pattern
using System;

class GFG {
    static int C = 3;

    // Utility function to print
    // matrix in zig-zag form
    static void zigZagMatrix(int[, ] arr, int n, int m)
    {
        int row = 0, col = 0;

        // Boolean variable that will
        // true if we need to increment
        // 'row' valueotherwise false-
        // if increment 'col' value
        bool row_inc = false;

        // Print matrix of lower half
        // zig-zag pattern
        int mn = Math.Min(m, n);
        for (int len = 1; len <= mn; ++len) {
                for (int i = 0; i < len; ++i) {

                Console.Write(arr[row, col] + " ");

                if (i + 1 == len)
                    break;

                // If row_increment value is true
                // increment row and decrement col
                // else decrement row and increment
                // col
                if (row_inc) {
                    ++row;
                    --col;
                }
                else {
                    --row;
                    ++col;
                }
            }

            if (len == mn)
                break;

            // Update row or col value
            // according to the last
            // increment
            if (row_inc) {
                    ++row;
                    row_inc = false;
            }
            else {
                ++col;
                row_inc = true;
            }
        }

        // Update the indexes of row
        // and col variable
        if (row == 0) {
            if (col == m - 1)
                ++row;
            else
                ++col;
            row_inc = true;
        }
        else {
            if (row == n - 1)
                ++col;
            else
                ++row;
            row_inc = false;
        }

        // Print the next half
        // zig-zag pattern
        int MAX = Math.Max(m, n) - 1;
        for (int len, diag = MAX; diag > 0; --diag) {

            if (diag > mn)
                    len = mn;
            else
                len = diag;

            for (int i = 0; i < len; ++i) {
                    Console.Write(arr[row, col] + " ");

                if (i + 1 == len)
                    break;

                // Update row or col value
                // according to the last
                // increment
                if (row_inc) {
                        ++row;
                        --col;
                }
                else {
                    ++col;
                    --row;
                }
            }

            // Update the indexes of
            // row and col variable
            if (row == 0 || col == m - 1) {
                if (col == m - 1)
                    ++row;
                else
                    ++col;

                row_inc = true;
            }

            else if (col == 0 || row == n - 1) {
                if (row == n - 1)
                    ++col;
                else
                    ++row;

                row_inc = false;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int[, ] matrix = { { 1, 2, 3 },
                        { 4, 5, 6 },
                        { 7, 8, 9 } };
        zigZagMatrix(matrix, 3, 3);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print
// matrix in Zig-zag pattern
$C = 3;

// Utility function
// to print matrix
// in zig-zag form
function zigZagMatrix($arr,
                      $n, $m)
{
    $row = 0; $col = 0;

    // Boolean variable that
    // will true if we need
    // to increment 'row'
    // value otherwise false-
    // if increment 'col' value
    $row_inc = false;

    // Print matrix of lower
    // half zig-zag pattern
    $mn = min($m, $n);
    for ($len = 1;
         $len <= $mn; $len++)
    {
        for ($i = 0;
             $i < $len; $i++)
        {
            echo ($arr[$row][$col]." ");

            if ($i + 1 == $len)
                break;

            // If row_increment value
            // is true increment row
            // and decrement col else
            // decrement row and
            // increment col
            if ($row_inc)
            {
                $row++; $col--;
            }
            else
            {
                $row--; $col++;
            }
        }

        if ($len == $mn)
            break;

        // Update row or col
        // value according
        // to the last increment
        if ($row_inc)
        {
            ++$row; $row_inc = false;
        }
        else
        {
            ++$col; $row_inc = true;
        }
    }

    // Update the indexes of
    // row and col variable
    if ($row == 0)
    {
        if ($col == $m - 1)
            ++$row;
        else
            ++$col;
        $row_inc = 1;
    }
    else
    {
        if ($row == $n - 1)
            ++$col;
        else
            ++$row;
        $row_inc = 0;
    }

    // Print the next half
    // zig-zag pattern
    $MAX = max($m, $n) - 1;
    for ($len, $diag = $MAX;
         $diag > 0; --$diag)
    {
        if ($diag > $mn)
            $len = $mn;
        else
            $len = $diag;

        for ($i = 0;
             $i < $len; ++$i)
        {
            echo($arr[$row][$col] . " ");

            if ($i + 1 == $len)
                break;

            // Update row or col
            // value according to
            // the last increment
            if ($row_inc)
            {
                ++$row; --$col;
            }
            else
            {
                ++$col; --$row;
            }
        }

        // Update the indexes of
        // row and col variable
        if ($row == 0 ||
            $col == $m - 1)
        {
            if ($col == $m - 1)
                ++$row;
            else
                ++$col;

            $row_inc = true;
        }

        else if ($col == 0 ||
                 $row == $n - 1)
        {
            if ($row == $n - 1)
                ++$col;
            else
                ++$row;

            $row_inc = false;
        }
    }
}

// Driver code
$matrix = array(array(1, 2, 3),
                array(4, 5, 6),
                array(7, 8, 9));

zigZagMatrix($matrix, 3, 3);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

**输出:**

```
1 2 4 7 5 3 6 8 9 
```

**时间复杂度:**O(n * m)
T3】辅助空间: O(1)