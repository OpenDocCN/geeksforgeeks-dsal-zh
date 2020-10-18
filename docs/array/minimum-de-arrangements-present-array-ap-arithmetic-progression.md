# AP 数组中存在的最小解排列（算术级数）

> 原文： [https://www.geeksforgeeks.org/minimum-de-arrangements-present-array-ap-arithmetic-progression/](https://www.geeksforgeeks.org/minimum-de-arrangements-present-array-ap-arithmetic-progression/)

给定一个`n`元素数组。 给定数组是某些算术级数的置换。 找到该数组中存在的最小解排列数，以使该数组成为算术级数。

**示例**：

```
Input : arr[] = [8, 6, 10 ,4, 2]
Output : Minimum De-arrangement = 3
Explanation : arr[] = [10, 8, 6, 4, 2] is permutation 
which forms an AP and has minimum de-arrangements.

Input : arr[] = [5, 10, 15, 25, 20]
Output : Minimum De-arrangement = 2
Explanation : arr[] = [5, 10, 15, 20, 25] is permutation
which forms an AP and has minimum de-arrangements.

```



根据算术级数的性质，我们的序列将以递增或递减的方式排列。 同样，我们知道，任何算术级数的倒数也将形成另一个算术级数。 因此，我们创建了一个原始数组的副本，然后按升序对给定的数组进行排序，然后再次找到不匹配的总数，之后我们将反转排序后的数组并找到新的不匹配数。 比较两个不匹配的计数，我们可以找到最小的失序数。 时间复杂度=`O(nLogn)`。

## C++ 

```cpp

// CPP for counting minimum de-arrangements present 
// in an array. 
#include<bits/stdc++.h> 
using namespace std; 

// function to count Dearrangement 
int countDe (int arr[], int n) 
{ 
    // create a copy of original array 
    vector <int> v (arr, arr+n); 

    // sort the array 
    sort(arr, arr+n); 

    // traverse sorted array for counting mismatches 
    int count1 = 0; 
    for (int i=0; i<n; i++)    
        if (arr[i] != v[i]) 
            count1++;         

    // reverse the sorted array 
    reverse(arr,arr+n);     

    // traverse reverse sorted array for counting  
    // mismatches 
    int count2 = 0; 
    for (int i=0; i<n; i++) 
        if (arr[i] != v[i])        
            count2++; 

    // return minimum mismatch count 
    return (min (count1, count2)); 
} 

// driver program 
int main() 
{ 
    int arr[] = {5, 9, 21, 17, 13}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << "Minimum Dearrangement = " << countDe(arr, n); 
    return 0; 
}  

```

## Java

```java

// Java code for counting minimum  
// de-arrangements present in an array. 
import java.util.*; 
import java.lang.*; 
import java.util.Arrays; 

public class GeeksforGeeks{ 

    // function to count Dearrangement 
    public static int countDe(int arr[], int n){ 
        int v[] = new int[n]; 

        // create a copy of original array 
        for(int i = 0; i < n; i++) 
            v[i] = arr[i];  

        // sort the array 
        Arrays.sort(arr); 

        // traverse sorted array for  
        // counting mismatches 
        int count1 = 0; 
        for (int i = 0; i < n; i++)  
            if (arr[i] != v[i]) 
            count1++;      

        // reverse the sorted array 
        Collections.reverse(Arrays.asList(arr)); 

        // traverse reverse sorted array  
        // for counting mismatches 
        int count2 = 0; 
        for (int i = 0; i < n; i++) 
            if (arr[i] != v[i])      
                count2++; 

        // return minimum mismatch count 
        return (Math.min (count1, count2)); 
    } 

    // driver code 
    public static void main(String argc[]){ 
        int arr[] = {5, 9, 21, 17, 13}; 
        int n = 5; 
        System.out.println("Minimum Dearrangement = "+ 
                            countDe(arr, n)); 
    } 
} 

/*This code is contributed by Sagar Shukla.*/

```

## Python3

```py

# Python3 code for counting minimum  
# de-arrangements present in an array. 

# function to count Dearrangement 
def countDe(arr, n): 

        i = 0

        # create a copy of  
        # original array 
        v = arr.copy() 

        # sort the array 
        arr.sort() 

        # traverse sorted array for  
        # counting mismatches 
        count1 = 0
        i = 0
        while( i < n ):  
            if (arr[i] != v[i]): 
                count1 = count1 + 1
            i = i + 1

        # reverse the sorted array 
        arr.sort(reverse=True) 

        # traverse reverse sorted array  
        # for counting mismatches 
        count2 = 0
        i = 0
        while( i < n ): 
            if (arr[i] != v[i]):      
                count2 = count2 + 1
            i = i + 1

        # return minimum mismatch count 
        return (min (count1, count2)) 

# Driven code 
arr = [5, 9, 21, 17, 13] 
n = 5
print ("Minimum Dearrangement =",countDe(arr, n)) 

# This code is contributed by "rishabh_jain". 

```

## C# 

```cs

// C# code for counting  
// minimum de-arrangements  
// present in an array. 
using System; 

class GFG 
{ 

// function to count 
// Dearrangement 
public static int countDe(int[] arr,  
                          int n) 
{ 
    int[] v = new int[n]; 

    // create a copy 
    // of original array 
    for(int i = 0; i < n; i++) 
        v[i] = arr[i];  

    // sort the array 
    Array.Sort(arr); 

    // traverse sorted array for  
    // counting mismatches 
    int count1 = 0; 
    for (int i = 0; i < n; i++)  
        if (arr[i] != v[i]) 
        count1++;  

    // reverse the sorted array 
    Array.Reverse(arr); 

    // traverse reverse sorted array  
    // for counting mismatches 
    int count2 = 0; 
    for (int i = 0; i < n; i++) 
        if (arr[i] != v[i])  
            count2++; 

    // return minimum  
    // mismatch count 
    return (Math.Min (count1, count2)); 
} 

// Driver code 
public static void Main() 
{ 
    int[] arr = new int[]{5, 9, 21, 17, 13}; 
    int n = 5; 
    Console.WriteLine("Minimum Dearrangement = " +  
                                 countDe(arr, n)); 
} 
} 

// This code is contributed by mits 

```

## PHP

```php

<?php 
// PHP for counting minimum de-arrangements  
// present in an array. 

// function to count Dearrangement 
function countDe ($arr, $n) 
{ 
    // create a copy of original array 
    $v = $arr; 

    // sort the array 
    sort($arr); 

    // traverse sorted array for  
    // counting mismatches 
    $count1 = 0; 
    for ($i = 0; $i < $n; $i++)  
        if ($arr[$i] != $v[$i]) 
            $count1++;  

    // reverse the sorted array 
    rsort($arr);  

    // traverse reverse sorted array  
    // for counting mismatches 
    $count2 = 0; 
    for ($i = 0; $i < $n; $i++) 
        if ($arr[$i] != $v[$i])  
            $count2++; 

    // return minimum mismatch count 
    return (min($count1, $count2)); 
} 

// Driver Code 
$arr = array(5, 9, 21, 17, 13); 
$n = count($arr); 
echo "Minimum Dearrangement = " .  
               countDe($arr, $n); 

// This code is contributed by mits 
?> 

```

**输出**：

```
Minimum Dearrangement = 2

```



* * *

* * *



