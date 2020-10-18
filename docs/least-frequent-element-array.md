# 数组中最少的元素

> 原文： [https://www.geeksforgeeks.org/least-frequent-element-array/](https://www.geeksforgeeks.org/least-frequent-element-array/)

给定一个数组，在其中找到最不频繁的元素。 如果有多个元素出现的次数最少，请打印其中的任何一个。

**示例**：

```
Input : arr[] = {1, 3, 2, 1, 2, 2, 3, 1}
Output : 3
3 appears minimum number of times in given
array.

Input : arr[] = {10, 20, 30}
Output : 10 or 20 or 30

```



一个简单的**解决方案**是运行两个循环。 外循环一一挑选所有元素。 内循环找到所拾取元素的频率，并与到目前为止的最小值进行比较。 该解决方案的时间复杂度为`O(n^2)`。

更好的**解决方案**是进行排序。 我们首先对数组进行排序，然后线性遍历数组。

## C++ 

```cpp

// CPP program to find the least frequent element 
// in an array. 
#include <bits/stdc++.h> 
using namespace std; 

int leastFrequent(int arr[], int n) 
{ 
    // Sort the array 
    sort(arr, arr + n); 

    // find the min frequency using linear traversal 
    int min_count = n+1, res = -1, curr_count = 1; 
    for (int i = 1; i < n; i++) { 
        if (arr[i] == arr[i - 1]) 
            curr_count++; 
        else { 
            if (curr_count < min_count) { 
                min_count = curr_count; 
                res = arr[i - 1]; 
            } 
            curr_count = 1; 
        } 
    } 

    // If last element is least frequent 
    if (curr_count < min_count) 
    { 
        min_count = curr_count; 
        res = arr[n - 1]; 
    } 

    return res; 
} 

// driver program 
int main() 
{ 
    int arr[] = {1, 3, 2, 1, 2, 2, 3, 1}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << leastFrequent(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find the least frequent element 
// in an array. 
import java.io.*; 
import java.util.*; 

class GFG { 

    static int leastFrequent(int arr[], int n) 
    { 

        // Sort the array 
        Arrays.sort(arr); 

        // find the min frequency using  
        // linear traversal 
        int min_count = n+1, res = -1; 
        int curr_count = 1; 

        for (int i = 1; i < n; i++) { 
            if (arr[i] == arr[i - 1]) 
                curr_count++; 
            else { 
                if (curr_count < min_count) { 
                    min_count = curr_count; 
                    res = arr[i - 1]; 
                } 

                curr_count = 1; 
            } 
        } 

        // If last element is least frequent 
        if (curr_count < min_count) 
        { 
            min_count = curr_count; 
            res = arr[n - 1]; 
        } 

        return res; 
    } 

    // driver program 
    public static void main(String args[]) 
    { 
        int arr[] = {1, 3, 2, 1, 2, 2, 3, 1}; 
        int n = arr.length; 
        System.out.print(leastFrequent(arr, n)); 

    } 
} 

/*This code is contributed by Nikita Tiwari.*/

```

## Python3

```py

# Python 3 program to find the least 
# frequent element in an array. 

def leastFrequent(arr, n) : 

    # Sort the array 
    arr.sort() 

    # find the min frequency using 
    # linear traversal 
    min_count = n + 1
    res = -1
    curr_count = 1
    for i in range(1, n) : 
        if (arr[i] == arr[i - 1]) : 
            curr_count = curr_count + 1
        else : 
            if (curr_count < min_count) : 
                min_count = curr_count 
                res = arr[i - 1] 

            curr_count = 1

    # If last element is least frequent 
    if (curr_count < min_count) : 
        min_count = curr_count 
        res = arr[n - 1] 

    return res 

# Driver program 
arr = [1, 3, 2, 1, 2, 2, 3, 1] 
n = len(arr) 
print(leastFrequent(arr, n)) 

# This code is contributed 
# by Nikita Tiwari. 

```

## C# 

```cs

// C# program to find the least  
// frequent element in an array. 
using System; 

class GFG { 

    static int leastFrequent(int[] arr, int n) 
    { 
        // Sort the array 
        Array.Sort(arr); 

        // find the min frequency  
        // using linear traversal 
        int min_count = n + 1, res = -1; 
        int curr_count = 1; 

        for (int i = 1; i < n; i++)  
        { 
            if (arr[i] == arr[i - 1]) 
                curr_count++; 
            else 
            { 
                if (curr_count < min_count) 
                { 
                    min_count = curr_count; 
                    res = arr[i - 1]; 
                } 

                curr_count = 1; 
            } 
        } 

        // If last element is least frequent 
        if (curr_count < min_count) 
        { 
            min_count = curr_count; 
            res = arr[n - 1]; 
        } 

        return res; 
    } 

    // Driver code 
    static public void Main () 
    { 
        int[] arr = {1, 3, 2, 1, 2, 2, 3, 1}; 
        int n = arr.Length;  

        // Function calling 
        Console.Write(leastFrequent(arr, n)); 
    } 
} 

// This code is contributed by Shrikant13 

```

## PHP

```php

<?php 
// PHP program to find the  
// least frequent element 
// in an array. 

function leastFrequent($arr, $n) 
{ 

    // Sort the array 
    sort($arr);  
    sort($arr , $n); 

    // find the min frequency  
    // using linear traversal 
    $min_count = $n + 1;  
    $res = -1; 
    $curr_count = 1; 
    for($i = 1; $i < $n; $i++) 
    { 
        if ($arr[$i] == $arr[$i - 1]) 
            $curr_count++; 
        else 
        { 
            if ($curr_count < $min_count) 
            { 
                $min_count = $curr_count; 
                $res = $arr[$i - 1]; 
            } 
            $curr_count = 1; 
        } 
    } 

    // If last element is  
    // least frequent 
    if ($curr_count < $min_count) 
    { 
        $min_count = $curr_count; 
        $res = $arr[$n - 1]; 
    } 

    return $res; 
} 

// Driver Code 
{ 
    $arr = array(1, 3, 2, 1, 2, 2, 3, 1); 
    $n = sizeof($arr) / sizeof($arr[0]); 
    echo leastFrequent($arr, $n); 
    return 0; 
} 

// This code is contributed by nitin mittal  
?> 

```

**输出**：

```
3

```

**时间复杂度**：`O(N log N)`。

**辅助空间**：`O(1)`。

**有效解决方案**是使用哈希。 我们创建一个哈希表，并将元素及其频率计数存储为键值对。 最后，我们遍历哈希表并打印具有最小值的键。

## C++

```

// CPP program to find the least frequent element 
// in an array. 
#include <bits/stdc++.h> 
using namespace std; 

int leastFrequent(int arr[], int n) 
{ 
    // Insert all elements in hash. 
    unordered_map<int, int> hash; 
    for (int i = 0; i < n; i++) 
        hash[arr[i]]++; 

    // find the min frequency 
    int min_count = n+1, res = -1; 
    for (auto i : hash) { 
        if (min_count >= i.second) { 
            res = i.first; 
            min_count = i.second; 
        } 
    } 

    return res; 
} 

// driver program 
int main() 
{ 
    int arr[] = {1, 3, 2, 1, 2, 2, 3, 1}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << leastFrequent(arr, n); 
    return 0; 
} 

```

## Java

```java

//Java program to find the least frequent element 
//in an array 
import java.util.HashMap; 
import java.util.Map; 
import java.util.Map.Entry; 

class GFG { 

    static int leastFrequent(int arr[],int n) 
    { 

        // Insert all elements in hash. 
        Map<Integer,Integer> count =  
                   new HashMap<Integer,Integer>(); 

        for(int i = 0; i < n; i++) 
        { 
            int key = arr[i]; 
            if(count.containsKey(key)) 
            { 
                int freq = count.get(key); 
                freq++; 
                count.put(key,freq); 
            } 
            else
                count.put(key,1); 
        } 

        // find min frequency. 
        int min_count = n+1, res = -1; 
        for(Entry<Integer,Integer> val : count.entrySet()) 
        { 
            if (min_count >= val.getValue()) 
            { 
                res = val.getKey(); 
                min_count = val.getValue(); 
            } 
        } 

        return res; 
    } 

    // driver program 
    public static void main (String[] args) { 

        int arr[] = {1, 3, 2, 1, 2, 2, 3, 1}; 
        int n = arr.length; 

        System.out.println(leastFrequent(arr,n)); 
    } 
} 

// This code is contributed by Akash Singh. 

```

## Python3

```py

# Python3 program to find the most  
# frequent element in an array. 
import math as mt 

def leastFrequent(arr, n): 

    # Insert all elements in Hash. 
    Hash = dict() 
    for i in range(n): 
        if arr[i] in Hash.keys(): 
            Hash[arr[i]] += 1
        else: 
            Hash[arr[i]] = 1

    # find the max frequency 
    min_count = n + 1
    res = -1
    for i in Hash:  
        if (min_count >= Hash[i]):  
            res = i 
            min_count = Hash[i] 

    return res 

# Driver Code 
arr = [1, 3, 2, 1, 2, 2, 3, 1]  
n = len(arr) 
print(leastFrequent(arr, n)) 

# This code is contributed by 
# mohit kumar 29 

```

## C#

```

// C# program to find the  
// least frequent element  
// in an array. 
using System; 
using System.Collections.Generic; 

class GFG 
{ 
    static int leastFrequent(int []arr,  
                             int n) 
    { 
        // Insert all elements in hash. 
        Dictionary<int, int> count =  
                        new Dictionary<int,  
                                       int>(); 
        for (int i = 0; i < n; i++) 
        { 
            int key = arr[i]; 
            if(count.ContainsKey(key)) 
            { 
                int freq = count[key]; 
                freq++; 
                count[key] = freq; 
            } 
            else
                count.Add(key, 1); 
        } 

        // find the min frequency 
        int min_count = n + 1, res = -1; 
        foreach (KeyValuePair<int,  
                    int> pair in count) 
        { 
            if (min_count >= pair.Value) 
            { 
                res = pair.Key; 
                min_count = pair.Value; 
            } 
        }  
        return res; 
    } 

    // Driver Code 
    static void Main() 
    { 
        int []arr = new int[]{1, 3, 2, 1, 
                              2, 2, 3, 1}; 
        int n = arr.Length; 
        Console.Write(leastFrequent(arr, n)); 
    } 
} 

// This code is contributed by  
// Manish Shaw(manishshaw1) 

```

**输出**：

```
3

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。



* * *

* * *



