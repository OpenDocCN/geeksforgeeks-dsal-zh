# 从两个给定排序数组的交替元素生成所有可能的排序数组

> 原文： [https://www.geeksforgeeks.org/generate-all-possible-sorted-arrays-from-alternate-elements-of-two-given-arrays/](https://www.geeksforgeeks.org/generate-all-possible-sorted-arrays-from-alternate-elements-of-two-given-arrays/)

给定两个已排序的数组`A`和`B`，生成所有可能的数组，以使第一个元素从`A`中取出，然后从`B`中取出，然后从`A`中取出，依此类推，以递增的顺序直到数组用尽。 生成的数组应以`B`中的元素结尾。

例如：

```

A = {10, 15, 25}
B = {1, 5, 20, 30}

The resulting arrays are:
  10 20
  10 20 25 30
  10 30
  15 20
  15 20 25 30
  15 30
  25 30
```

**我们强烈建议您最小化浏览器，然后自己尝试。**

这个想法是使用递归。 在递归函数中，传递一个标志以指示输出中的当前元素应取自`A`还是`B`。 下面是 C++ 的实现。

## C++ 

```cpp

#include<bits/stdc++.h> 
using namespace std; 

void printArr(int arr[], int n); 

/* Function to generates and prints all sorted arrays from alternate elements of 
   'A[i..m-1]' and 'B[j..n-1]' 
   If 'flag' is true, then current element is to be included from A otherwise 
   from B. 
   'len' is the index in output array C[]. We print output  array  each time 
   before including a character from A only if length of output array is 
   greater than 0\. We try than all possible combinations */
void generateUtil(int A[], int B[], int C[], int i, int j, int m, int n, 
                  int len, bool flag) 
{ 
    if (flag) // Include valid element from A 
    { 
        // Print output if there is at least one 'B' in output array 'C' 
        if (len) 
            printArr(C, len+1); 

        // Recur for all elements of A after current index 
        for (int k = i; k < m; k++) 
        { 
            if (!len) 
            { 
                /* this block works for the very first call to include 
                     the first element in the output array */
                C[len] = A[k]; 

                // don't increment lem as B is included yet 
                generateUtil(A, B, C, k+1, j, m, n, len, !flag); 
            } 
            else      /* include valid element from A and recur */
            { 
                if (A[k] > C[len]) 
                { 
                    C[len+1] = A[k]; 
                    generateUtil(A, B, C, k+1, j, m, n, len+1, !flag); 
                } 
            } 
        } 
    } 
    else   /* Include valid element from B and recur */
    { 
        for (int l = j; l < n; l++) 
        { 
            if (B[l] > C[len]) 
            { 
                C[len+1] = B[l]; 
                generateUtil(A, B, C, i, l+1, m, n, len+1, !flag); 
            } 
        } 
    } 
} 

/* Wrapper function */
void generate(int A[], int B[], int m, int n) 
{ 
    int C[m+n];    /* output array */
    generateUtil(A, B, C, 0, 0, m, n, 0, true); 
} 

// A utility function to print an array 
void printArr(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
    cout << endl; 
} 

// Driver program 
int main() 
{ 
    int A[] = {10, 15, 25}; 
    int B[] = {5, 20, 30}; 
    int n = sizeof(A)/sizeof(A[0]); 
    int m = sizeof(B)/sizeof(B[0]); 
    generate(A, B, n, m); 
    return 0; 
} 

```

## Java

```java

class GenerateArrays { 

    /* Function to generates and prints all sorted arrays from alternate 
       elements of 'A[i..m-1]' and 'B[j..n-1]' 
       If 'flag' is true, then current element is to be included from A  
       otherwise from B. 
       'len' is the index in output array C[]. We print output array   
       each time before including a character from A only if length of  
       output array is greater than 0\. We try than all possible  
       combinations */
    void generateUtil(int A[], int B[], int C[], int i, int j, int m, int n, 
            int len, boolean flag)  
    { 
        if (flag) // Include valid element from A 
        { 
            // Print output if there is at least one 'B' in output array 'C' 
            if (len != 0)  
                printArr(C, len + 1); 

            // Recur for all elements of A after current index 
            for (int k = i; k < m; k++)  
            { 
                if (len == 0)  
                { 
                    /* this block works for the very first call to include 
                    the first element in the output array */
                    C[len] = A[k]; 

                    // don't increment lem as B is included yet 
                    generateUtil(A, B, C, k + 1, j, m, n, len, !flag); 
                }  

                /* include valid element from A and recur */
                else if (A[k] > C[len])  
                { 
                        C[len + 1] = A[k]; 
                        generateUtil(A, B, C, k + 1, j, m, n, len + 1, !flag); 
                } 
            } 
        }  

        /* Include valid element from B and recur */
        else
        { 
            for (int l = j; l < n; l++)  
            { 
                if (B[l] > C[len])  
                { 
                    C[len + 1] = B[l]; 
                    generateUtil(A, B, C, i, l + 1, m, n, len + 1, !flag); 
                } 
            } 
        } 
    } 

    /* Wrapper function */
    void generate(int A[], int B[], int m, int n)  
    { 
        int C[] = new int[m + n]; 

        /* output array */
        generateUtil(A, B, C, 0, 0, m, n, 0, true); 
    } 

    // A utility function to print an array 
    void printArr(int arr[], int n)  
    { 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
        System.out.println(""); 
    } 

    public static void main(String[] args)  
    { 
        GenerateArrays generate = new GenerateArrays(); 
        int A[] = {10, 15, 25}; 
        int B[] = {5, 20, 30}; 
        int n = A.length; 
        int m = B.length; 
        generate.generate(A, B, n, m); 
    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

## Python3

```py

# A utility function to print an array 
def printArr(arr,n): 

    for i in range(n): 
        print(arr[i] , " ",end="") 
    print() 

''' Function to generates and prints all 
    sorted arrays from alternate elements of 
   'A[i..m-1]' and 'B[j..n-1]' 
   If 'flag' is true, then current element 
   is to be included from A otherwise 
   from B. 
   'len' is the index in output array C[]. 
    We print output  array  each time 
   before including a character from A 
   only if length of output array is 
   greater than 0\. We try than all possible combinations '''
def generateUtil(A,B,C,i,j,m,n,len,flag): 

    if (flag): # Include valid element from A 

        # Print output if there is at 
        # least one 'B' in output array 'C' 
        if (len): 
            printArr(C, len+1) 

        # Recur for all elements of 
        # A after current index 
        for k in range(i,m): 

            if ( not len): 

                ''' this block works for the 
                    very first call to include 
                    the first element in the output array '''
                C[len] = A[k] 

                # don't increment lem 
                # as B is included yet 
                generateUtil(A, B, C, k+1, j, m, n, len,  not flag) 

            else:   

                # include valid element from A and recur  
                if (A[k] > C[len]): 

                    C[len+1] = A[k] 
                    generateUtil(A, B, C, k+1, j, m, n, len+1, not flag) 

    else:   

        # Include valid element from B and recur 
        for l in range(j,n): 

            if (B[l] > C[len]): 

                C[len+1] = B[l] 
                generateUtil(A, B, C, i, l+1, m, n, len+1, not flag) 

# Wrapper function  
def generate(A,B,m,n): 

    C=[]    #output array  
    for i in range(m+n+1): 
        C.append(0) 
    generateUtil(A, B, C, 0, 0, m, n, 0, True) 

# Driver program 

A = [10, 15, 25] 
B = [5, 20, 30] 
n = len(A) 
m = len(B) 

generate(A, B, n, m) 

# This code is contributed 
# by Anant Agarwal. 

```

## C# 

```cs

// C# Program to generate all possible 
// sorted arrays from alternate elements 
// of two given sorted arrays 
using System; 

class GenerateArrays { 

/* Function to generates and prints 
   all sorted arrays from alternate  
   elements of 'A[i..m-1]' and 'B[j..n-1]'  
   If 'flag' is true, then current element 
   is to be included from A otherwise 
   from B.  
   'len' is the index in output array  
   C[]. We print output array each  
   time before including a character  
   from A only if length of output array  
   is greater than 0\. We try than all  
   possible combinations */
   public virtual void generateUtil(int[] A, int[] B, 
                                    int[] C, int i,  
                                    int j, int m, int n, 
                                    int len, bool flag) { 

    // Include valid  
    // element from A                                    
    if (flag)  
    { 

        // Print output if there is 
        // at least one 'B' in  
        // output array 'C'  
        if (len != 0) { 

            printArr(C, len + 1); 
        } 

        // Recur for all elements 
        // of A after current index  
        for (int k = i; k < m; k++) { 

            if (len == 0) { 

                /* this block works for the  
                   very first call to include  
                   the first element in the  
                   output array */
                C[len] = A[k]; 

                // don't increment lem  
                // as B is included yet  
                generateUtil(A, B, C, k + 1, j, 
                             m, n, len, !flag); 
            } 

            // include valid element 
            // from A and recur  
            else if (A[k] > C[len]) { 

                C[len + 1] = A[k]; 
                generateUtil(A, B, C, k + 1, j, 
                         m, n, len + 1, !flag); 
            } 
        } 
    } 

    // Include valid element 
    // from B and recur  
    else { 
        for (int l = j; l < n; l++) { 
            if (B[l] > C[len]) { 
                C[len + 1] = B[l]; 
                generateUtil(A, B, C, i, l + 1, 
                         m, n, len + 1, !flag); 
            } 
        } 
    } 
} 

// Wrapper function  
public virtual void generate(int[] A, int[] B, 
                               int m, int n) { 
    int[] C = new int[m + n]; 

    // output array  
    generateUtil(A, B, C, 0, 0, m, n, 0, true); 
} 

// A utility function to print an array  
public virtual void printArr(int[] arr, int n) { 

    for (int i = 0; i < n; i++) { 
        Console.Write(arr[i] + " "); 
    } 
    Console.WriteLine(""); 
} 

// Driver Code 
public static void Main(string[] args) { 

    GenerateArrays generate = new GenerateArrays(); 

    int[] A = new int[] {10, 15, 25}; 
    int[] B = new int[] {5, 20, 30}; 

    int n = A.Length; 
    int m = B.Length; 
    generate.generate(A, B, n, m); 
} 
} 

// This code is contributed by Shrikant13 

```

## PHP

```php

<?php  

/* Function to generates and prints all  
sorted arrays from alternate elements of 
'A[i..m-1]' and 'B[j..n-1]' 
If 'flag' is true, then current element 
is to be included from A otherwise from B. 
'len' is the index in output array C[].  
We print output array each time before 
including a character from A only if length  
of output array is greater than 0\. We try 
than all possible combinations */
function generateUtil(&$A, &$B, &$C, $i, $j, 
                       $m, $n, $len, $flag) 
{ 
    if ($flag) // Include valid element from A 
    { 
        // Print output if there is at least 
        // one 'B' in output array 'C' 
        if ($len) 
            printArr($C, $len + 1); 

        // Recur for all elements of A  
        // after current index 
        for ($k = $i; $k < $m; $k++) 
        { 
            if (!$len) 
            { 
                /* this block works for the very  
                first call to include the first  
                element in the output array */
                $C[$len] = $A[$k]; 

                // don't increment lem as B 
                // is included yet 
                generateUtil($A, $B, $C, $k + 1, 
                             $j, $m, $n, $len, !$flag); 
            } 
            else     /* include valid element 
                        from A and recur */
            { 
                if ($A[$k] > $C[$len]) 
                { 
                    $C[$len + 1] = $A[$k]; 
                    generateUtil($A, $B, $C, $k + 1, $j,  
                                 $m, $n, $len + 1, !$flag); 
                } 
            } 
        } 
    } 
    else /* Include valid element  
            from B and recur */
    { 
        for ($l = $j; $l < $n; $l++) 
        { 
            if ($B[$l] > $C[$len]) 
            { 
                $C[$len + 1] = $B[$l]; 
                generateUtil($A, $B, $C, $i, $l + 1, 
                             $m, $n, $len + 1, !$flag); 
            } 
        } 
    } 
} 

/* Wrapper function */
function generate(&$A, &$B, $m, $n) 
{ 
    $C = array_fill(0, ($m + $n), NULL); /* output array */
    generateUtil($A, $B, $C, 0, 0, $m, $n, 0, true); 
} 

// A utility function to print an array 
function printArr(&$arr, $n) 
{ 
    for ($i = 0; $i < $n; $i++) 
        echo $arr[$i] . " "; 
    echo "\n"; 
} 

// Driver Code 
$A = array(10, 15, 25); 
$B = array(5, 20, 30); 
$n = sizeof($A); 
$m = sizeof($B); 
generate($A, $B, $n, $m); 

// This code is contributed by ChitraNayal 
?> 

```

**输出**：

```
10 20
10 20 25 30
10 30
15 20
15 20 25 30
15 30
25 30

```



