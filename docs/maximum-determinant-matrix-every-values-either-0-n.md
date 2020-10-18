# 每个值为 0 或`n`的矩阵的最大行列式

> 原文： [https://www.geeksforgeeks.org/maximum-determinant-matrix-every-values-either-0-n/](https://www.geeksforgeeks.org/maximum-determinant-matrix-every-values-either-0-n/)

我们给定一个正数`n`，我们必须找到一个`x3 * 3`矩阵，该矩阵可以由 0 或`n`的组合形成，并且具有最大的行列式。

**示例**：

```
Input : n = 3 
Output : Maximum determinant = 54
Resultant Matrix :
3 3 0
0 3 3
3 0 3

Input : n = 13 
Output : Maximum determinant = 4394
Resultant Matrix :
13 13  0
0  13 13
13  0 13

```

**解释**：

对于元素为 0 或`n`的任何`3 * 3`矩阵，最大可能行列式为`2 * (n ^ 3)`。 具有最大行列式的矩阵的形式也为：

```
n n 0
0 n n
n 0 0
```


## C++ 

```cpp

// C++ program to find  maximum possible determinant 
// of 0/n matrix. 
#include <bits/stdc++.h> 
using namespace std; 

// Function for maximum determinant 
int maxDet(int n) 
{ 
    return (2*n*n*n); 
} 

// Function to print resulatant matrix 
void resMatrix ( int n) 
{ 
    for (int i = 0; i < 3; i++) 
    { 
        for (int j = 0; j < 3; j++) 
        { 
            // three position where 0 appears 
            if (i == 0 && j == 2) 
                cout << "0 "; 
            else if (i == 1 && j == 0) 
                cout << "0 "; 
            else if (i == 2 && j == 1) 
                cout << "0 "; 

            // position where n appears 
            else
                cout << n << " "; 
        } 
        cout << "\n"; 
    } 
}  

// Driver code 
int main() 
{ 
    int n = 15; 
    cout << "Maximum Determinant = " << maxDet(n); 

    cout << "\nResultant Matrix :\n"; 
    resMatrix(n);  

    return 0; 
} 

```

## Java

```java

// Java program to find maximum possible 
// determinant of 0/n matrix. 
import java.io.*; 

public class GFG 
{ 

// Function for maximum determinant 
static int maxDet(int n) 
{ 
    return (2 * n * n * n); 
} 

// Function to print resulatant matrix 
void resMatrix(int n) 
{ 
    for (int i = 0; i < 3; i++) 
    { 
        for (int j = 0; j < 3; j++) 
        { 
            // three position where 0 appears 
            if (i == 0 && j == 2) 
                System.out.print("0 "); 
            else if (i == 1 && j == 0) 
                System.out.print("0 "); 
            else if (i == 2 && j == 1) 
                System.out.print("0 "); 

            // position where n appears 
            else
                System.out.print(n +" "); 
        } 
        System.out.println(""); 
    } 
}  

    // Driver code 
    static public void main (String[] args) 
    { 
            int n = 15; 
            GFG geeks=new GFG(); 
            System.out.println("Maximum Determinant = "
                                + maxDet(n)); 

            System.out.println("Resultant Matrix :");  
            geeks.resMatrix(n);  

    } 
} 

// This code is contributed by vt_m. 

```

## Python3

```py

# Python 3 program to find maximum 
# possible determinant of 0/n matrix.  
# Function for maximum determinant 
def maxDet(n): 
    return 2 * n * n * n 

# Function to print resulatant matrix  
def resMatrix(n): 
    for i in range(3): 
        for j in range(3): 

            # three position where 0 appears 
            if i == 0 and j == 2: 
                print("0", end = " ") 
            elif i == 1 and j == 0: 
                print("0", end = " ") 
            elif i == 2 and j == 1: 
                print("0", end = " ") 

            # position where n appears 
            else: 
                print(n, end = " ") 
        print("\n") 

# Driver code 
n = 15
print("Maximum Detrminat=", maxDet(n)) 
print("Resultant Matrix:") 
resMatrix(n) 

# This code is contributed by Shrikant13 

```

## C# 

```cs

// C# program to find maximum possible 
// determinant of 0/n matrix. 
using System; 

public class GFG 
{ 

// Function for maximum determinant 
static int maxDet(int n) 
{ 
    return (2 * n * n * n); 
} 

// Function to print resulatant matrix 
void resMatrix(int n) 
{ 
    for (int i = 0; i < 3; i++) 
    { 
        for (int j = 0; j < 3; j++) 
        { 
            // three position where 0 appears 
            if (i == 0 && j == 2) 
                Console.Write("0 "); 
            else if (i == 1 && j == 0) 
                Console.Write("0 "); 
            else if (i == 2 && j == 1) 
                Console.Write("0 "); 

            // position where n appears 
            else
                Console.Write(n +" "); 
        } 
        Console.WriteLine(""); 
    } 
}  

    // Driver code 
    static public void Main (String []args) 
    { 
            int n = 15; 
            GFG geeks=new GFG(); 
            Console.WriteLine("Maximum Determinant = "
                                + maxDet(n)); 

            Console.WriteLine("Resultant Matrix :");  
            geeks.resMatrix(n);  

    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to find maximum  
// possible determinant of 0/n matrix. 

// Function for maximum determinant 
function maxDet($n) 
{ 
    return (2 * $n * $n * $n); 
} 

// Function to print  
// resulatant matrix 
function resMatrix ( $n) 
{ 
    for ($i = 0; $i < 3; $i++) 
    { 
        for ($j = 0; $j < 3; $j++) 
        { 
            // three position  
            // where 0 appears 
            if ($i == 0 && $j == 2) 
                echo "0 "; 
            else if ($i == 1 && $j == 0) 
                echo "0 "; 
            else if ($i == 2 && $j == 1) 
                echo "0 "; 

            // position where n appears 
            else
                echo $n , " "; 
        } 
    echo "\n"; 
    } 
}  

// Driver code 
$n = 15; 
echo "Maximum Determinant = " ,  
                    maxDet($n); 

echo "\nResultant Matrix :\n"; 
resMatrix($n);  

// This code is contributed 
// by nitin mittal.  
?> 

```

**输出**：

```
Maximum Determinant = 6750
Resultant Matrix :
15 15  0
0  15 15
15 0  15

```

**练习**：将上述解扩展为广义的`k x k`矩阵。



