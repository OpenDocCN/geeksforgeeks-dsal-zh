# 检查矩阵的所有行是否都是彼此的旋转

> 原文： [https://www.geeksforgeeks.org/check-rows-matrix-circular-rotations/](https://www.geeksforgeeks.org/check-rows-matrix-circular-rotations/)

给定`n * n`大小的矩阵，任务是查找所有行是否都是彼此的圆周旋转。

**示例**：

```
Input: mat[][] = 1, 2, 3
                 3, 1, 2
                 2, 3, 1
Output:  Yes
All rows are rotated permutation
of each other.

Input: mat[3][3] = 1, 2, 3
                   3, 2, 1
                   1, 3, 2
Output:  No
Explanation : As 3, 2, 1 is not a rotated or 
circular permutation of 1, 2, 3

```



这个想法是基于下面的文章。

[用于检查字符串是否彼此的旋转的程序](https://www.geeksforgeeks.org/a-program-to-check-if-strings-are-rotations-of-each-other/)

**步骤**：

1.  创建一个由第一行元素组成的字符串，并将其与自身连接在一起，以便可以高效地执行字符串搜索操作。 将此字符串设为`str_cat`。

2.  遍历所有剩余的行。 对于要遍历的每一行，创建一个当前行元素的字符串`str_curr`。 如果`str_curr`不是`str_cat`的子字符串，则返回`false`。

3.  返回`true`。

下面是上述步骤的实现。

## C++ 

```cpp

// C++ program to check if all rows of a matrix 
// are rotations of each other 
#include <bits/stdc++.h> 
using namespace std; 
const int MAX = 1000; 

// Returns true if all rows of mat[0..n-1][0..n-1] 
// are rotations of each other. 
bool isPermutedMatrix( int mat[MAX][MAX], int n) 
{ 
    // Creating a string that contains elements of first 
    // row. 
    string str_cat = ""; 
    for (int i = 0 ; i < n ; i++) 
        str_cat = str_cat + "-" + to_string(mat[0][i]); 

    // Concatenating the string with itself so that 
    // substring search operations can be performed on 
    // this 
    str_cat = str_cat + str_cat; 

    // Start traversing remaining rows 
    for (int i=1; i<n; i++) 
    { 
        // Store the matrix into vector in the form 
        // of strings 
        string curr_str = ""; 
        for (int j = 0 ; j < n ; j++) 
            curr_str = curr_str + "-" + to_string(mat[i][j]); 

        // Check if the current string is present in 
        // the concatenated string or not 
        if (str_cat.find(curr_str) == string::npos) 
            return false; 
    } 

    return true; 
} 

// Drivers code 
int main() 
{ 
    int n = 4 ; 
    int mat[MAX][MAX] = {{1, 2, 3, 4}, 
        {4, 1, 2, 3}, 
        {3, 4, 1, 2}, 
        {2, 3, 4, 1} 
    }; 
    isPermutedMatrix(mat, n)? cout << "Yes" : 
                              cout << "No"; 
    return 0; 
} 

```

## Java

```java
// Java program to check if all rows of a matrix  
// are rotations of each other  
class GFG  
{ 
  
    static int MAX = 1000; 
  
    // Returns true if all rows of mat[0..n-1][0..n-1]  
    // are rotations of each other.  
    static boolean isPermutedMatrix(int mat[][], int n)  
    { 
        // Creating a string that contains 
        // elements of first row.  
        String str_cat = ""; 
        for (int i = 0; i < n; i++)  
        { 
            str_cat = str_cat + "-" + String.valueOf(mat[0][i]); 
        } 
  
        // Concatenating the string with itself  
        // so that substring search operations   
        // can be performed on this  
        str_cat = str_cat + str_cat; 
  
        // Start traversing remaining rows  
        for (int i = 1; i < n; i++) 
        { 
            // Store the matrix into vector in the form  
            // of strings  
            String curr_str = ""; 
            for (int j = 0; j < n; j++)  
            { 
                curr_str = curr_str + "-" + String.valueOf(mat[i][j]); 
            } 
  
            // Check if the current string is present in  
            // the concatenated string or not  
            if (str_cat.contentEquals(curr_str))  
            { 
                return false; 
            } 
        } 
  
        return true; 
    } 
  
    // Drivers code  
    public static void main(String[] args)  
    { 
        int n = 4; 
        int mat[][] = {{1, 2, 3, 4}, 
        {4, 1, 2, 3}, 
        {3, 4, 1, 2}, 
        {2, 3, 4, 1} 
        }; 
        if (isPermutedMatrix(mat, n))  
        { 
            System.out.println("Yes"); 
        } 
        else
        { 
            System.out.println("No"); 
        } 
    } 
} 
  
/* This code contributed by PrinciRaj1992 */
```

## Python3

```py
# Python3 program to check if all rows  
# of a matrix are rotations of each other  
  
MAX = 1000
  
# Returns true if all rows of mat[0..n-1][0..n-1]  
# are rotations of each other.  
def isPermutedMatrix(mat, n) : 
      
    # Creating a string that contains  
    # elements of first row.  
    str_cat = "" 
    for i in range(n) : 
        str_cat = str_cat + "-" + str(mat[0][i]) 
  
    # Concatenating the string with itself  
    # so that substring search operations  
    # can be performed on this  
    str_cat = str_cat + str_cat 
  
    # Start traversing remaining rows  
    for i in range(1, n) : 
          
        # Store the matrix into vector  
        # in the form of strings  
        curr_str = "" 
          
        for j in range(n) : 
            curr_str = curr_str + "-" + str(mat[i][j]) 
  
        # Check if the current string is present  
        # in the concatenated string or not  
        if (str_cat.find(curr_str)) :  
            return True
              
    return False
  
# Driver code  
if __name__ == "__main__" : 
    n = 4
    mat = [[1, 2, 3, 4],  
           [4, 1, 2, 3],  
           [3, 4, 1, 2],  
           [2, 3, 4, 1]]  
      
    if (isPermutedMatrix(mat, n)): 
        print("Yes") 
    else : 
        print("No") 
          
# This code is contributed by Ryuga
```

## C#

```cs
// C# program to check if all rows of a matrix  
// are rotations of each other  
using System; 
  
class GFG  
{ 
  
    //static int MAX = 1000; 
  
    // Returns true if all rows of mat[0..n-1,0..n-1]  
    // are rotations of each other.  
    static bool isPermutedMatrix(int [,]mat, int n)  
    { 
        // Creating a string that contains 
        // elements of first row.  
        string str_cat = ""; 
        for (int i = 0; i < n; i++)  
        { 
            str_cat = str_cat + "-" + mat[0,i].ToString(); 
        } 
  
        // Concatenating the string with itself  
        // so that substring search operations  
        // can be performed on this  
        str_cat = str_cat + str_cat; 
  
        // Start traversing remaining rows  
        for (int i = 1; i < n; i++) 
        { 
            // Store the matrix into vector in the form  
            // of strings  
            string curr_str = ""; 
            for (int j = 0; j < n; j++)  
            { 
                curr_str = curr_str + "-" + mat[i,j].ToString(); 
            } 
  
            // Check if the current string is present in  
            // the concatenated string or not  
            if (str_cat.Equals(curr_str))  
            { 
                return false; 
            } 
        } 
  
        return true; 
    } 
  
    // Driver code  
    static void Main()  
    { 
        int n = 4; 
        int [,]mat = {{1, 2, 3, 4}, 
        {4, 1, 2, 3}, 
        {3, 4, 1, 2}, 
        {2, 3, 4, 1} 
        }; 
          
        if (isPermutedMatrix(mat, n))  
        { 
            Console.WriteLine("Yes"); 
        } 
        else
        { 
            Console.WriteLine("No"); 
        } 
    } 
} 
  
/* This code contributed by mits */
```

## PHP

```php
<?php  
// PHP program to check if all rows of a  
// matrix are rotations of each other 
$MAX = 1000; 
  
// Returns true if all rows of mat[0..n-1][0..n-1] 
// are rotations of each other. 
function isPermutedMatrix( &$mat, $n) 
{ 
    // Creating a string that contains  
    // elements of first row. 
    $str_cat = ""; 
    for ($i = 0 ; $i < $n ; $i++) 
        $str_cat = $str_cat . "-" .  
                   strval($mat[0][$i]); 
  
    // Concatenating the string with itself  
    // so that substring search operations  
    // can be performed on this 
    $str_cat = $str_cat . $str_cat; 
  
    // Start traversing remaining rows 
    for ($i = 1; $i < $n; $i++) 
    { 
        // Store the matrix into vector  
        // in the form of strings 
        $curr_str = ""; 
        for ($j = 0 ; $j < $n ; $j++) 
            $curr_str = $curr_str . "-" . 
                        strval($mat[$i][$j]); 
  
        // Check if the current string is present  
        // in the concatenated string or not 
        if (strpos($str_cat, $curr_str)) 
            return true; 
    } 
  
    return false; 
} 
  
// Driver Code 
$n = 4; 
$mat = array(array(1, 2, 3, 4), 
             array(4, 1, 2, 3), 
             array(3, 4, 1, 2), 
             array(2, 3, 4, 1)); 
if (isPermutedMatrix($mat, $n)) 
    echo "Yes"; 
else
    echo "No"; 
  
// This code is contributed by ita_c 
?>
```

输出：

```
Yes
```

