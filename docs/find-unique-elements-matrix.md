# 在矩阵中查找唯一元素

> 原文： [https://www.geeksforgeeks.org/find-unique-elements-matrix/](https://www.geeksforgeeks.org/find-unique-elements-matrix/)

给定具有`n`行和`m`列的矩阵`mat[][]`。 我们需要在矩阵中找到唯一元素，即矩阵中未重复的元素或频率为 1 的元素。

**示例**：

```
Input :  20  15  30  2
         2   3   5   30
         6   7   6   8
Output : 3  20  5  7  8  15 

Input :  1  2  3  
         5  6  2
         1  3  5
         6  2  2
Output : No unique element in the matrix

```



请按照以下步骤查找唯一元素：

1.  创建一个空的哈希表或字典。

2.  遍历矩阵的所有元素。

3.  如果字典中存在元素，则增加其计数。

4.  否则使用值 1 插入元素。

## C++ 

```cpp

// C++ program to find unique 
// element in matrix 
#include<bits/stdc++.h> 
using namespace std; 
#define R 4 
#define C 4 

// function that calculate unique element 
int unique(int mat[R][C], int n, int m) 
{ 
    int maximum = 0, flag = 0; 
    for(int i = 0; i < n; i++)  
        for(int j = 0; j < m; j++) 
            // Find maximum element in 
            // a matrix 
            if(maximum < mat[i][j]) 
                    maximum = mat[i][j]; 

    // Take 1-D array of (maximum + 1) 
    // size 
    int b[maximum + 1] = {0}; 
    for(int i = 0 ; i < n; i++) 
        for(int j = 0; j < m; j++) 
            b[mat[i][j]]++; 

    //print unique element 
    for(int i = 1; i <= maximum; i++) 
        if(b[i] == 1) 
            cout << i << " "; 
            flag = 1; 

    if(!flag){ 
        cout << "No unique element in the matrix"; 
    } 
} 

// Driver program 
int main() 
{ 
    int mat[R][C] = {{ 1, 2, 3, 20}, 
                     {5, 6, 20, 25}, 
                     {1, 3, 5, 6}, 
                     {6, 7, 8, 15}}; 

    // function that calculate unique element 
    unique(mat, R, C); 
    return 0; 
} 

// This code is contributed by Naman_Garg. 

```

## Java

```java

// Java program to find unique 
// element in matrix 
class GFG 
{ 
static int R = 4, C = 4; 

// function that calculate  
// unique element 
static void unique(int mat[][],  
                   int n, int m) 
{ 
    int maximum = 0, flag = 0; 
    for(int i = 0; i < n; i++)  
        for(int j = 0; j < m; j++) 

            // Find maximum element  
            // in a matrix 
            if(maximum < mat[i][j]) 
                    maximum = mat[i][j]; 

    // Take 1-D array of  
    // (maximum + 1) size 
    int b[] = new int [maximum + 1]; 
    for(int i = 0 ; i < n; i++) 
        for(int j = 0; j < m; j++) 
            b[mat[i][j]]++; 

    //print unique element 
    for(int i = 1; i <= maximum; i++) 
        if(b[i] == 1) 
            System.out.print(i + " "); 
            flag = 1; 

    if(flag == 0) 
    { 
        System.out.println("No unique element " +  
                                "in the matrix"); 
    } 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    int mat[][] = {{1, 2, 3, 20}, 
                   {5, 6, 20, 25}, 
                   {1, 3, 5, 6}, 
                   {6, 7, 8, 15}}; 

    // function that calculate  
    // unique element 
    unique(mat, R, C); 
} 
} 

// This code is contributed 
// by Arnab Kundu 

```

## Python3

```py

# Python 3 program to find unique 
# element in matrix 
def unique(mat, n, m): 

    maximum = 0; flag = 0

    for i in range(0, n): 
        for j in range(0, m): 

            # Find maximum element in 
            # a matrix 
            if(maximum < mat[i][j]): 
                maximum = mat[i][j]; 

    uniqueElementDict = [0] * (maximum + 1) 

    # loops to traverse through the matrix  
    for i in range(0, n): 
        for j in range(0, m): 
                uniqueElementDict[mat[i][j]] += 1

    # Print all those keys whose count is 1 
    for key in range(maximum + 1): 
        if uniqueElementDict[key] == 1: 
            print (key, end = " ") 
            flag = 1

    if(flag == 0): 
        print("No unique element in the matrix") 

# Driver Code 
mat = [[1, 2, 3, 20],  
       [5, 6, 20, 25], 
       [1, 3, 5, 6], 
       [6, 7, 8, 15]] 
n = 4
m = 4
unique(mat, n, m) 

```

## C# 

```cs

// C# program to find unique  
// element in matrix 
using System; 

class GFG  
{  
static int R = 4, C = 4;  

// function that calculate  
// unique element  
static void unique(int [,]mat,  
                   int n, int m)  
{  
    int maximum = 0, flag = 0;  
    for(int i = 0; i < n; i++)  
        for(int j = 0; j < m; j++)  

            // Find maximum element  
            // in a matrix  
            if(maximum < mat[i, j])  
                    maximum = mat[i, j];  

    // Take 1-D array of  
    // (maximum + 1) size  
    int []b = new int [maximum + 1];  
    for(int i = 0 ; i < n; i++)  
        for(int j = 0; j < m; j++)  
            b[mat[i, j]]++;  

    // print unique element  
    for(int i = 1; i <= maximum; i++)  
        if(b[i] == 1)  
            Console.Write(i + " ");  
            flag = 1;  

    if(flag == 0)  
    {  
        Console.WriteLine("No unique element " +  
                               "in the matrix");  
    }  
}  

// Driver Code  
public static void Main()  
{  
    int [,]mat = {{1, 2, 3, 20},  
                  {5, 6, 20, 25},  
                  {1, 3, 5, 6},  
                  {6, 7, 8, 15}};  

    // function that calculate  
    // unique element  
    unique(mat, R, C);  
}  
}  

// This code is contributed  
// by Subhadeep 

```

## PHP

```php

<?php 
// PHP program to find unique 
// element in matrix 

$R = 4; 
$C = 4; 

// function that calculate unique element 
function unique($mat, $n, $m) 
{ 
    $maximum = 0; 
    $flag = 0; 
    for($i = 0; $i < $n; $i++)  
        for($j = 0; $j < $m; $j++) 

            // Find maximum element in 
            // a matrix 
            if($maximum < $mat[$i][$j]) 
                    $maximum = $mat[$i][$j]; 

    // Take 1-D array of (maximum + 1) 
    // size 
    $b = array(); 
    for($j = 0; $j < $maximum + 1; $j++) 
        $b[$j] = 0; 

    for($i = 0 ; $i < $n; $i++) 
        for($j = 0; $j < $m; $j++) 
            $b[$mat[$i][$j]]++; 

    // print unique element 
    for($i = 1; $i <= $maximum; $i++) 
        if($b[$i] == 1) 
            echo "$i "; 
            $flag = 1; 

    if(!$flag) 
    { 
        echo "No unique element in the matrix"; 
    } 
} 

// Driver Code 
$mat = array(array(1, 2, 3, 20), 
             array(5, 6, 20, 25), 
             array(1, 3, 5, 6), 
             array(6, 7, 8, 15)); 

// function that calculate unique element 
unique($mat, $R, $C); 

// This code is contributed by iAyushRaj 
?> 

```

**输出**：

```
2 7 8 25 15 

```



* * *

* * *



