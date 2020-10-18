# 给定数组范围的 XOR 之和最大的数字

> 原文： [https://www.geeksforgeeks.org/number-whose-sum-of-xor-with-given-array-range-is-maximum/](https://www.geeksforgeeks.org/number-whose-sum-of-xor-with-given-array-range-is-maximum/)

系统会为您提供`N`个整数和`Q`个查询的序列。 在每个查询中，给您两个参数`L`和`R`。您必须找到最小的整数`X`，使得`0 <= X < 2 ^ 31`，并且`x`与范围`[L,  R]`的所有元素的 XOR 之和是最大可能的。

**示例**：

```
Input  : A = {20, 11, 18, 2, 13}
         Three queries as (L, R) pairs
         1 3
         3 5
         2 4
Output : 2147483629
         2147483645
         2147483645

```



**方法**：每个元素和`x`的二进制表示，我们可以观察到每个位都是独立的，并且可以通过迭代每个位来解决问题。 现在基本上，对于每个位，我们都需要计算给定范围内的 1 和 0 的数量，如果 1 的数量更多，则必须将`x`的该位设置为 0，以便在`x`或`x`之后用`x`取最大，否则 0 的数量更多，那么您必须将`x`的该位设置为 1。如果 1 和 0 的数量相等，那么我们可以将`x`的该位设置为 1 或 0 中的任何一个，因为这不会影响总和，但是 我们必须最小化`x`的值，因此我们将使用该位 0。

现在，为了优化解决方案，我们可以通过创建前缀数组来预先计算数字的每个位位置上的 1 的计数，这将花费`O(n)`时间。 现在，对于每个查询，从 1 到第`R`个位置的数字都是 1，由 1 到第`L - 1`位置的数字。

## C++ 

```cpp

// CPP program to find smallest integer X 
// such that sum of its XOR with range is 
// maximum. 
#include <bits/stdc++.h> 
using namespace std; 

#define MAX 2147483647 
int one[100001][32]; 

// Function to make prefix array which  
// counts 1's of each bit up to that number 
void make_prefix(int A[], int n) 
{ 
    for (int j = 0; j < 32; j++) 
        one[0][j] = 0; 

    // Making a prefix array which sums 
    // number of 1's up to that position 
    for (int i = 1; i <= n; i++)  
    { 
        int a = A[i - 1]; 
        for (int j = 0; j < 32; j++)  
        { 
            int x = pow(2, j); 

            // If j-th bit of a number is set then 
            // add one to previously counted 1's 
            if (a & x) 
                one[i][j] = 1 + one[i - 1][j]; 
            else
                one[i][j] = one[i - 1][j]; 
        } 
    } 
} 

// Function to find X 
int Solve(int L, int R) 
{ 
    int l = L, r = R; 
    int tot_bits = r - l + 1; 

    // Initially taking maximum value all bits 1 
    int X = MAX; 

    // Iterating over each bit 
    for (int i = 0; i < 31; i++)  
    { 

        // get 1's at ith bit between the  
        // range L-R by subtracting 1's till 
        // Rth number - 1's till L-1th number 
        int x = one[r][i] - one[l - 1][i]; 

        // If 1's are more than or equal to 0's 
        // then unset the ith bit from answer 
        if (x >= tot_bits - x)  
        { 
            int ith_bit = pow(2, i); 

            // Set ith bit to 0 by doing 
            // Xor with 1 
            X = X ^ ith_bit; 
        } 
    } 
    return X; 
} 

// Driver program 
int main() 
{ 
    // Taking inputs 
    int n = 5, q = 3; 
    int A[] = { 210, 11, 48, 22, 133 }; 
    int L[] = { 1, 4, 2 }, R[] = { 3, 14, 4 }; 

    make_prefix(A, n); 

    for (int j = 0; j < q; j++) 
        cout << Solve(L[j], R[j]) << endl; 

    return 0; 
} 

```

## Java

```java

// Java program to find smallest integer X 
// such that sum of its XOR with range is 
// maximum. 
import java.lang.Math; 

class GFG { 

    private static final int MAX = 2147483647; 
    static int[][] one = new int[100001][32]; 

    // Function to make prefix array which counts 
    // 1's of each bit up to that number 
    static void make_prefix(int A[], int n) 
    { 
        for (int j = 0; j < 32; j++) 
            one[0][j] = 0; 

        // Making a prefix array which sums 
        // number of 1's up to that position 
        for (int i = 1; i <= n; i++)  
        { 
            int a = A[i - 1]; 
            for (int j = 0; j < 32; j++)  
            { 
                int x = (int)Math.pow(2, j); 

                // If j-th bit of a number is set then 
                // add one to previously counted 1's 
                if ((a & x) != 0) 
                    one[i][j] = 1 + one[i - 1][j]; 
                else
                    one[i][j] = one[i - 1][j]; 
            } 
        } 
    } 

    // Function to find X 
    static int Solve(int L, int R) 
    { 
        int l = L, r = R; 
        int tot_bits = r - l + 1; 

        // Initially taking maximum  
        // value all bits 1 
        int X = MAX; 

        // Iterating over each bit 
        for (int i = 0; i < 31; i++)  
        { 

            // get 1's at ith bit between the range 
            // L-R by subtracting 1's till 
            // Rth number - 1's till L-1th number 
            int x = one[r][i] - one[l - 1][i]; 

            // If 1's are more than or equal to 0's 
            // then unset the ith bit from answer 
            if (x >= tot_bits - x)  
            { 
                int ith_bit = (int)Math.pow(2, i); 

                // Set ith bit to 0 by  
                // doing Xor with 1 
                X = X ^ ith_bit; 
            } 
        } 
        return X; 
    } 

    // Driver program 
    public static void main(String[] args) 
    { 
        // Taking inputs 
        int n = 5, q = 3; 
        int A[] = { 210, 11, 48, 22, 133 }; 
        int L[] = { 1, 4, 2 }, R[] = { 3, 14, 4 }; 

        make_prefix(A, n); 

        for (int j = 0; j < q; j++) 
            System.out.println(Solve(L[j], R[j])); 
    } 
} 

// This code is contributed by Smitha 

```

## Python3

```py

# Python3 program to find smallest integer X 
# such that sum of its XOR with range is 
# maximum. 
import math 

one = [[0 for x in range(32)]  
      for y in range(100001)]  
MAX = 2147483647

# Function to make prefix array  
# which counts 1's of each bit  
# up to that number 
def make_prefix(A, n) : 
    global one, MAX

    for j in range(0 , 32) : 
        one[0][j] = 0

    # Making a prefix array which  
    # sums number of 1's up to  
    # that position 
    for i in range(1, n+1) :  
        a = A[i - 1] 
        for j in range(0 , 32) : 

            x = int(math.pow(2, j)) 

            # If j-th bit of a number  
            # is set then add one to 
            # previously counted 1's 
            if (a & x) : 
                one[i][j] = 1 + one[i - 1][j] 
            else : 
                one[i][j] = one[i - 1][j] 

# Function to find X 
def Solve(L, R) : 

    global one, MAX
    l = L  
    r = R 
    tot_bits = r - l + 1

    # Initially taking maximum 
    # value all bits 1 
    X = MAX

    # Iterating over each bit 
    for i in range(0, 31) : 

        # get 1's at ith bit between the  
        # range L-R by subtracting 1's till 
        # Rth number - 1's till L-1th number 

        x = one[r][i] - one[l - 1][i] 

        # If 1's are more than or equal  
        # to 0's then unset the ith bit 
        # from answer 
        if (x >= (tot_bits - x)) : 

            ith_bit = pow(2, i) 

            # Set ith bit to 0 by 
            # doing Xor with 1 
            X = X ^ ith_bit 
    return X 

# Driver Code 
n = 5
q = 3
A = [ 210, 11, 48, 22, 133 ] 
L = [ 1, 4, 2 ]  
R = [ 3, 14, 4 ] 

make_prefix(A, n) 

for j in range(0, q) : 
    print (Solve(L[j], R[j]),end="\n") 

# This code is contributed by  
# Manish Shaw(manishshaw1) 

```

## C# 

```cs

// C# program to find smallest integer X 
// such that sum of its XOR with range is 
// maximum. 
using System; 
using System.Collections.Generic; 

class GFG{ 
    static int MAX = 2147483647; 
    static int [,]one = new int[100001,32]; 

    // Function to make prefix  
    // array which counts 1's  
    // of each bit up to that number 
    static void make_prefix(int []A, int n) 
    { 
        for (int j = 0; j < 32; j++) 
            one[0,j] = 0; 

        // Making a prefix array which sums 
        // number of 1's up to that position 
        for (int i = 1; i <= n; i++)  
        { 
            int a = A[i - 1]; 
            for (int j = 0; j < 32; j++)  
            { 
                int x = (int)Math.Pow(2, j); 

                // If j-th bit of a number is set then 
                // add one to previously counted 1's 
                if ((a & x) != 0) 
                    one[i, j] = 1 + one[i - 1, j]; 
                else
                    one[i,j] = one[i - 1, j]; 
            } 
        } 
    } 

    // Function to find X 
    static int Solve(int L, int R) 
    { 
        int l = L, r = R; 
        int tot_bits = r - l + 1; 

        // Initially taking maximum 
        // value all bits 1 
        int X = MAX; 

        // Iterating over each bit 
        for (int i = 0; i < 31; i++)  
        { 

            // get 1's at ith bit between the  
            // range L-R by subtracting 1's till 
            // Rth number - 1's till L-1th number 
            int x = one[r, i] - one[l - 1, i]; 

            // If 1's are more than or  
            // equal to 0's then unset 
            // the ith bit from answer 
            if (x >= tot_bits - x)  
            { 
                int ith_bit = (int)Math.Pow(2, i); 

                // Set ith bit to 0 by doing 
                // Xor with 1 
                X = X ^ ith_bit; 
            } 
        } 
        return X; 
    } 

    // Driver Code 
    public static void Main() 
    { 

        // Taking inputs 
        int n = 5, q = 3; 
        int []A = {210, 11, 48, 22, 133}; 
        int []L = {1, 4, 2}; 
        int []R = {3, 14, 4}; 

        make_prefix(A, n); 

        for (int j = 0; j < q; j++) 
            Console.WriteLine(Solve(L[j], R[j])); 
    } 
} 

// This code is contributed by  
// Manish Shaw (manishshaw1) 

```

## PHP

```php

<?php 
error_reporting(0); 
// PHP program to find smallest integer X 
// such that sum of its XOR with range is 
// maximum. 

$one = array(); 
$MAX = 2147483647; 

// Function to make prefix array  
// which counts 1's of each bit  
// up to that number 
function make_prefix($A, $n) 
{ 
    global $one, $MAX; 

    for ($j = 0; $j < 32; $j++) 
        $one[0][$j] = 0; 

    // Making a prefix array which  
    // sums number of 1's up to  
    // that position 
    for ($i = 1; $i <= $n; $i++)  
    { 
        $a = $A[$i - 1]; 
        for ($j = 0; $j < 32; $j++)  
        { 
            $x = pow(2, $j); 

            // If j-th bit of a number  
            // is set then add one to 
            // previously counted 1's 
            if ($a & $x) 
                $one[$i][$j] = 1 + $one[$i - 1][$j]; 
            else
                $one[$i][$j] = $one[$i - 1][$j]; 
        } 
    } 
} 

// Function to find X 
function Solve($L, $R) 
{ 
    global $one, $MAX; 
    $l = $L; $r = $R; 
    $tot_bits = $r - $l + 1; 

    // Initially taking maximum 
    // value all bits 1 
    $X = $MAX; 

    // Iterating over each bit 
    for ($i = 0; $i < 31; $i++)  
    { 
        // get 1's at ith bit between the  
        // range L-R by subtracting 1's till 
        // Rth number - 1's till L-1th number 

        $x = $one[$r][$i] - $one[$l - 1][$i]; 

        // If 1's are more than or equal  
        // to 0's then unset the ith bit 
        // from answer 
        if ($x >= ($tot_bits - $x))  
        { 
            $ith_bit = pow(2, $i); 

            // Set ith bit to 0 by 
            // doing Xor with 1 
            $X = $X ^ $ith_bit; 
        } 
    } 
    return $X; 
} 

// Driver Code 
$n = 5; $q = 3; 
$A = [ 210, 11, 48, 22, 133 ]; 
$L = [ 1, 4, 2 ];  
$R = [ 3, 14, 4 ]; 

make_prefix($A, $n); 

for ($j = 0; $j < $q; $j++) 
    echo (Solve($L[$j], $R[$j]). "\n"); 

// This code is contributed by  
// Manish Shaw(manishshaw1) 
?> 

```

**输出**：

```
2147483629
2147483647
2147483629

```



* * *

* * *



