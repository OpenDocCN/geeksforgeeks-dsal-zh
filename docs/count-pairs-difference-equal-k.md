算所有等于`k`的不同对的数量

> 原文： [https://www.geeksforgeeks.org/count-pairs-difference-equal-k/](https://www.geeksforgeeks.org/count-pairs-difference-equal-k/)

给定一个整数数组和一个正整数`k`，对所有不同的对进行计数，其差等于`k`。

**示例**：

```
Input: arr[] = {1, 5, 3, 4, 2}, k = 3
Output: 2
There are 2 pairs with difference 3, the pairs are {1, 4} and {5, 2} 

Input: arr[] = {8, 12, 16, 4, 0, 20}, k = 4
Output: 5
There are 5 pairs with difference 4, the pairs are {0, 4}, {4, 8}, 
{8, 12}, {12, 16} and {16, 20} 

```



**方法 1（简单）**：

一个简单的解决方案是逐一考虑所有对，并检查每对之间的差异。 以下程序实现简单的解决方案。 我们运行两个循环：外部循环选择对的第一个元素，内部循环寻找另一个元素。 如果数组中有重复项，则此解决方案将不起作用，因为要求仅计算不重复的对。

## C++ 

```cpp

/* A simple program to count pairs with difference k*/
#include<iostream> 
using namespace std; 

int countPairsWithDiffK(int arr[], int n, int k) 
{ 
    int count = 0; 

    // Pick all elements one by one 
    for (int i = 0; i < n; i++) 
    {        
        // See if there is a pair of this picked element 
        for (int j = i+1; j < n; j++) 
            if (arr[i] - arr[j] == k || arr[j] - arr[i] == k ) 
                  count++; 
    } 
    return count; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] =  {1, 5, 3, 4, 2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int k = 3; 
    cout << "Count of pairs with given diff is "
         << countPairsWithDiffK(arr, n, k); 
    return 0; 
} 

```

## Java

```java

// A simple Java program to  
//count pairs with difference k 
import java.util.*; 
import java.io.*; 

class GFG { 

    static int countPairsWithDiffK(int arr[],  
                                    int n, int k) 
    { 
        int count = 0; 

        // Pick all elements one by one 
        for (int i = 0; i < n; i++)  
        { 
            // See if there is a pair 
            // of this picked element 
            for (int j = i + 1; j < n; j++) 
                if (arr[i] - arr[j] == k || 
                    arr[j] - arr[i] == k) 
                    count++; 
        } 
        return count; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 5, 3, 4, 2 }; 
        int n = arr.length; 
        int k = 3; 
        System.out.println("Count of pairs with given diff is "
                        + countPairsWithDiffK(arr, n, k)); 
    } 
} 

// This code is contributed  
// by Sahil_Bansall 

```

## Python3

```py

# A simple program to count pairs with difference k 

def countPairsWithDiffK(arr, n, k): 
    count = 0

    # Pick all elements one by one 
    for i in range(0, n): 

        # See if there is a pair of this picked element 
        for j in range(i+1, n) : 

            if arr[i] - arr[j] == k or arr[j] - arr[i] == k: 
                count += 1

    return count 

# Driver program 
arr = [1, 5, 3, 4, 2] 

n = len(arr) 
k = 3
print ("Count of pairs with given diff is ", 
                countPairsWithDiffK(arr, n, k)) 

```

## C# 

```cs

// A simple C# program to count pairs with  
// difference k 
using System; 

class GFG { 

    static int countPairsWithDiffK(int []arr,  
                                int n, int k) 
    { 
        int count = 0; 

        // Pick all elements one by one 
        for (int i = 0; i < n; i++)  
        { 

            // See if there is a pair 
            // of this picked element 
            for (int j = i + 1; j < n; j++) 
                if (arr[i] - arr[j] == k || 
                      arr[j] - arr[i] == k) 
                    count++; 
        } 

        return count; 
    } 

    // Driver code 
    public static void Main() 
    { 
        int []arr = { 1, 5, 3, 4, 2 }; 
        int n = arr.Length; 
        int k = 3; 

        Console.WriteLine("Count of pairs with "
                             + " given diff is "
               + countPairsWithDiffK(arr, n, k)); 
    } 
} 

// This code is contributed by Sam007\. 

```

## PHP

```php

<?php 
// A simple PHP program to count  
// pairs with difference k 

function countPairsWithDiffK($arr, $n, 
                                   $k) 
{ 
    $count = 0; 

    // Pick all elements one by one 
    for($i = 0; $i < $n; $i++) 
    {  

        // See if there is a pair of 
        // this picked element 
        for($j = $i + 1; $j < $n; $j++) 
            if ($arr[$i] - $arr[$j] == $k or
                $arr[$j] - $arr[$i] == $k) 
                $count++; 
    } 
    return $count; 
} 

    // Driver Code 
    $arr = array(1, 5, 3, 4, 2); 
    $n = count($arr); 
    $k = 3; 
    echo "Count of pairs with given diff is "
        , countPairsWithDiffK($arr, $n, $k); 

// This code is contributed by anuj_67\. 
?> 

```

Output :

```
Count of pairs with given diff is 2
```

`O(n^2)`的时间复杂度。

**方法 2（使用排序）**：

我们可以使用`O(nLogn)`排序算法（例如[归并排序](http://geeksquiz.com/merge-sort/)，[堆排序(http://geeksquiz.com/heap-sort/)等）。以下是详细步骤。

```
1) Initialize count as 0
2) Sort all numbers in increasing order.
3) Remove duplicates from array.
4) Do following for each element arr[i]
   a) Binary Search for arr[i] + k in subarray from i+1 to n-1.
   b) If arr[i] + k found, increment count. 
5) Return count. 
```

## C++

```cpp

/* A sorting based program to count pairs with difference k*/
#include <iostream> 
#include <algorithm> 
using namespace std; 

/* Standard binary search function */
int binarySearch(int arr[], int low, int high, int x) 
{ 
    if (high >= low) 
    { 
        int mid = low + (high - low)/2; 
        if (x == arr[mid]) 
            return mid; 
        if (x > arr[mid]) 
            return binarySearch(arr, (mid + 1), high, x); 
        else
            return binarySearch(arr, low, (mid -1), x); 
    } 
    return -1; 
} 

/* Returns count of pairs with difference k in arr[] of size n. */
int countPairsWithDiffK(int arr[], int n, int k) 
{ 
    int count = 0, i; 
    sort(arr, arr+n);  // Sort array elements 

    /* code to remove duplicates from arr[] */

    // Pick a first element point 
    for (i = 0; i < n-1; i++) 
        if (binarySearch(arr, i+1, n-1, arr[i] + k) != -1) 
            count++; 

    return count; 
} 

// Driver program  
int main() 
{ 
    int arr[] = {1, 5, 3, 4, 2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int k = 3; 
    cout << "Count of pairs with given diff is "
        << countPairsWithDiffK(arr, n, k); 
    return 0; 
} 

```

## Java

```java

// A sorting base java program to  
// count pairs with difference k 
import java.util.*; 
import java.io.*; 

class GFG { 

    // Standard binary search function // 
    static int binarySearch(int arr[], int low,  
                               int high, int x) 
    { 
        if (high >= low)  
        { 
            int mid = low + (high - low) / 2; 
            if (x == arr[mid]) 
                return mid; 
            if (x > arr[mid]) 
                return binarySearch(arr, (mid + 1), 
                                          high, x); 
            else
                return binarySearch(arr, low,  
                                    (mid - 1), x); 
        } 
        return -1; 
    } 

    // Returns count of pairs with  
    // difference k in arr[] of size n.  
    static int countPairsWithDiffK(int arr[], int n, int k) 
    { 
        int count = 0, i; 

        // Sort array elements 
        Arrays.sort(arr); 

        // code to remove duplicates from arr[]  

        // Pick a first element point 
        for (i = 0; i < n - 1; i++) 
            if (binarySearch(arr, i + 1, n - 1, 
                             arr[i] + k) != -1) 
                count++; 

        return count; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 5, 3, 4, 2 }; 
        int n = arr.length; 
        int k = 3; 
        System.out.println("Count of pairs with given diff is "
                            + countPairsWithDiffK(arr, n, k)); 
    } 
} 

// This code is contributed by Sahil_Bansall 

```

## Python

```py

# A sorting based program to  
# count pairs with difference k 

# Standard binary search function  
def binarySearch(arr, low, high, x): 

    if (high >= low): 

        mid = low + (high - low)//2
        if x == arr[mid]: 
            return (mid) 
        elif(x > arr[mid]): 
            return binarySearch(arr, (mid + 1), high, x) 
        else: 
            return binarySearch(arr, low, (mid -1), x) 

    return -1

# Returns count of pairs with  
# difference k in arr[] of size n.  
def countPairsWithDiffK(arr, n, k): 

    count = 0
    arr.sort() # Sort array elements 

    # code to remove  
    # duplicates from arr[]  

    # Pick a first element point 
    for i in range (0, n - 2): 
        if (binarySearch(arr, i + 1, n - 1,  
                         arr[i] + k) != -1): 
            count += 1

    return count 

# Driver Code  
arr= [1, 5, 3, 4, 2] 
n = len(arr) 
k = 3
print ("Count of pairs with given diff is ", 
             countPairsWithDiffK(arr, n, k))  

# This code is contributed 
# by Shivi_Aggarwal 

```

## C#

```cs

// A sorting base C# program to  
// count pairs with difference k 
using System; 

class GFG { 

    // Standard binary search function  
    static int binarySearch(int []arr, int low,  
                            int high, int x) 
    { 
        if (high >= low)  
        { 
            int mid = low + (high - low) / 2; 
            if (x == arr[mid]) 
                return mid; 
            if (x > arr[mid]) 
                return binarySearch(arr, (mid + 1), 
                                          high, x); 
            else
                return binarySearch(arr, low,  
                                     (mid - 1), x); 
        } 

        return -1; 
    } 

    // Returns count of pairs with  
    // difference k in arr[] of size n.  
    static int countPairsWithDiffK(int []arr,  
                                   int n, int k) 
    { 

        int count = 0, i; 

        // Sort array elements 
        Array.Sort(arr); 

        // code to remove duplicates from arr[]  

        // Pick a first element point 
        for (i = 0; i < n - 1; i++) 
            if (binarySearch(arr, i + 1, n - 1, 
                            arr[i] + k) != -1) 
                count++; 

        return count; 
    } 

    // Driver code 
    public static void Main() 
    { 
        int []arr = { 1, 5, 3, 4, 2 }; 
        int n = arr.Length; 
        int k = 3; 

        Console.WriteLine("Count of pairs with"
                            + " given diff is "
              + countPairsWithDiffK(arr, n, k)); 
    } 
} 

// This code is contributed by Sam007\. 

```

## PHP

```php

<?php 
// A sorting based PHP program to 
// count pairs with difference k 

// Standard binary search function 
function binarySearch($arr, $low, 
                      $high, $x) 
{ 
    if ($high >= $low) 
    { 
        $mid = $low + ($high - $low)/2; 
        if ($x == $arr[$mid]) 
            return $mid; 

        if ($x > $arr[$mid]) 
            return binarySearch($arr, ($mid + 1),  
                                      $high, $x); 
        else
            return binarySearch($arr, $low, 
                               ($mid -1), $x); 
    } 
    return -1; 
} 

/* Returns count of pairs with 
   difference k in arr[] of size n. */
function countPairsWithDiffK($arr, $n, $k) 
{ 
    $count = 0; 
    $i; 

    // Sort array elements 
    sort($arr);  

    // Code to remove duplicates  
    // from arr[] 

    // Pick a first element point 
    for ($i = 0; $i < $n - 1; $i++) 
        if (binarySearch($arr, $i + 1, $n - 1,  
                         $arr[$i] + $k) != -1) 
            $count++; 

    return $count; 
} 

    // Driver Code 
    $arr = array(1, 5, 3, 4, 2); 
    $n = count($arr); 
    $k = 3; 
    echo "Count of pairs with given diff is "
         , countPairsWithDiffK($arr, $n, $k); 

// This code is contributed by anuj-67\. 
?> 

```

**输出**：

```
Count of pairs with given diff is 2
```

时间复杂度：第一步（排序）需要`O(nLogn)`时间。 第二步运行二分搜索`n`次，因此第二步的时间复杂度也是`O(nLogn)`。 因此，总体时间复杂度为`O(nLogn)`。 第二步可以优化为`O(n)`，请参见。

**方法 3（使用自平衡 BST）**：

我们也可以使用自平衡 BST（例如 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)或红黑树）来解决此问题。 以下是详细的算法。

```
1) Initialize count as 0.
2) Insert all elements of arr[] in an AVL tree. While inserting, 
   ignore an element if already present in AVL tree.
3) Do following for each element arr[i].
   a) Search for arr[i] + k in AVL tree, if found then increment count.
   b) Search for arr[i] - k in AVL tree, if found then increment count.
   c) Remove arr[i] from AVL tree. 
```

上述解决方案的时间复杂度也是`O(nLogn)`，因为自平衡二叉树的搜索和删除操作花费`O(Logn)`时间。

**方法 4（使用散列）**：

在许多情况下，我们也可以使用散列来实现平均时间复杂度为`O(n)`。

```
1) Initialize count as 0.
2) Insert all distinct elements of arr[] in a hash map.  While inserting, 
   ignore an element if already present in the hash map.
3) Do following for each element arr[i].
   a) Look for arr[i] + k in the hash map, if found then increment count.
   b) Look for arr[i] - k in the hash map, if found then increment count.
   c) Remove arr[i] from hash table. 
```

哈希在`O(n)`时间内起作用的非常简单的情况是值范围很小的情况。 例如，在以下实现中，数字范围假定为 0 到 99999。可以使用将值用作索引的简单哈希技术。

```

/* An efficient program to count pairs with difference k when the range 
   numbers is small */
#define MAX 100000 
int countPairsWithDiffK(int arr[], int n, int k) 
{ 
    int count = 0;  // Initialize count 

    // Initialize empty hashmap. 
    bool hashmap[MAX] = {false}; 

    // Insert array elements to hashmap 
    for (int i = 0; i < n; i++) 
        hashmap[arr[i]] = true; 

    for (int i = 0; i < n; i++) 
    { 
        int x = arr[i]; 
        if (x - k >= 0 && hashmap[x - k]) 
            count++; 
        if (x + k < MAX && hashmap[x + k]) 
            count++; 
        hashmap[x] = false; 
    } 
    return count; 
}

```

**方法 5（使用排序）**：

*   排序数组`arr`

*   取两个指针`l`和`r`，都指向第一个元素

*   取差`arr[r] – arr[l]`

*   如果`diff`值为`K`，则递增计数并将两个指针都移至下一个元素

*   如果值`diff > k`，则将`l`移至下一个元素

*   如果值`diff < k`，则将`r`移至下一个元素

*   返回计数

## C++

```cpp

/* A sorting based program to count pairs with difference k*/
#include <iostream> 
#include <algorithm> 
using namespace std; 

/* Returns count of pairs with difference k in arr[] of size n. */
int countPairsWithDiffK(int arr[], int n, int k) 
{ 
    int count = 0; 
    sort(arr, arr+n);  // Sort array elements 

    int l = 0; 
    int r = 0; 
    while(r < n) 
    { 
         if(arr[r] - arr[l] == k) 
        { 
              count++; 
              l++; 
              r++; 
        } 
         else if(arr[r] - arr[l] > k) 
              l++; 
         else // arr[r] - arr[l] < sum 
              r++; 
    }    
    return count; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] =  {1, 5, 3, 4, 2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int k = 3; 
    cout << "Count of pairs with given diff is "
         << countPairsWithDiffK(arr, n, k); 
    return 0; 
} 

```

## Java

```java

// A sorting based Java program to  
// count pairs with difference k 
import java.util.*; 

class GFG { 

/* Returns count of pairs with 
difference k in arr[] of size n. */
static int countPairsWithDiffK(int arr[], int n, 
                                          int k) 
{ 
    int count = 0; 
    Arrays.sort(arr); // Sort array elements 

    int l = 0; 
    int r = 0; 
    while(r < n) 
    { 
        if(arr[r] - arr[l] == k) 
        { 
            count++; 
            l++; 
            r++; 
        } 
        else if(arr[r] - arr[l] > k) 
            l++; 
        else // arr[r] - arr[l] < sum 
            r++; 
    }  
    return count; 
} 

// Driver program to test above function 
public static void main(String[] args) 
{ 
    int arr[] = {1, 5, 3, 4, 2}; 
    int n = arr.length; 
    int k = 3; 
    System.out.println("Count of pairs with given diff is " + 
                        countPairsWithDiffK(arr, n, k)); 
} 
} 

// This code is contributed by Prerna Saini 

```

## Python3

```py

# A sorting based program to  
# count pairs with difference k 
def countPairsWithDiffK(arr,n,k): 

    count =0

    # Sort array elements 
    arr.sort()  

    l =0
    r=0

    while r<n: 
        if arr[r]-arr[l]==k: 
            count+=1
            l+=1
            r+=1

        # arr[r] - arr[l] < sum 
        elif arr[r]-arr[l]>k:  
            l+=1
        else: 
            r+=1
    return count 

# Driver code 
if __name__=='__main__': 
    arr = [1, 5, 3, 4, 2] 
    n = len(arr) 
    k = 3
    print("Count of pairs with given diff is ", 
          countPairsWithDiffK(arr, n, k)) 

# This code is contributed by  
# Shrikant13 

```

## C#

```cs

// A sorting based C# program to count  
// pairs with difference k 
using System; 

class GFG { 

    /* Returns count of pairs with 
    difference k in arr[] of size n. */
    static int countPairsWithDiffK(int []arr,  
                                int n, int k) 
    { 
        int count = 0; 

        // Sort array elements 
        Array.Sort(arr); 

        int l = 0; 
        int r = 0; 
        while(r < n) 
        { 
            if(arr[r] - arr[l] == k) 
            { 
                count++; 
                l++; 
                r++; 
            } 
            else if(arr[r] - arr[l] > k) 
                l++; 
            else // arr[r] - arr[l] < sum 
                r++; 
        }  
        return count; 
    } 

    // Driver program to test above function 
    public static void Main() 
    { 
        int []arr = {1, 5, 3, 4, 2}; 
        int n = arr.Length; 
        int k = 3; 
        Console.Write("Count of pairs with "
                        + "given diff is " + 
            countPairsWithDiffK(arr, n, k)); 
    } 
} 

// This code is contributed by nitin mittal. 

```

## PHP

```php

<?php 
// A sorting based program to count 
// pairs with difference k 

// Returns count of pairs with  
// difference k in arr[] of size n. 
function countPairsWithDiffK( $arr, $n, $k) 
{ 
    $count = 0; 

    // Sort array elements 
    sort($arr);  

    $l = 0; 
    $r = 0; 
    while($r < $n) 
    { 
        if($arr[$r] - $arr[$l] == $k) 
        { 
            $count++; 
            $l++; 
            $r++; 
        } 
        else if($arr[$r] - $arr[$l] > $k) 
            $l++; 

        // arr[r] - arr[l] < k 
        else 
            $r++; 
    }  
    return $count; 
} 

    // Driver Code 
    $arr = array(1, 5, 3, 4, 2); 
    $n =count($arr); 
    $k = 3; 
    echo "Count of pairs with given diff is "
        , countPairsWithDiffK($arr, $n, $k); 

// This code is contributed by anuj_67, 
?> 

```

**输出**：

```
Count of pairs with given diff is 2
```

时间复杂度：`O(nLogn)`

