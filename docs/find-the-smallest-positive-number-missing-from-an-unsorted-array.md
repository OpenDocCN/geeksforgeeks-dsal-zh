# 查找未排序数组中缺失的最小正数 | 系列 1

> 原文： [https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/)

您会得到一个包含正负元素的未排序数组。 您必须使用恒定的额外空间在`O(n)`时间内找到数组中丢失的最小正数。 您可以修改原始数组。

例子：

```
 Input:  {2, 3, 7, 6, 8, -1, -10, 15}
 Output: 1

 Input:  { 2, 3, -7, 6, 8, 1, -10, 15 }
 Output: 4

 Input: {1, 1, 0, -1, -2}
 Output: 2 

```



解决此问题的**朴素的方法**是搜索给定数组中从 1 开始的所有正整数。 我们可能必须在给定数组中搜索最多`n + 1`个数字。 因此，在最坏的情况下，此解决方案需要`O(n ^ 2)`。

我们可以使用**排序**来解决，时间复杂度更低。 我们可以在`O(nLogn)`时间对数组进行排序。 数组排序后，我们要做的就是对数组进行线性扫描。 因此，此方法需要`O(nLogn + n)`时间，即`O(nLogn)`。

我们还可以**使用哈希**。 我们可以建立给定数组中所有正元素的哈希表。 一旦建立哈希表。 我们可以在哈希表中查找从 1 开始的所有正整数。一旦我们发现哈希表中不存在的数字，我们就将其返回。 这种方法平均可能需要`O(n)`时间，但需要`O(n)`额外空间。

**`O(n)`时间和`O(1)`额外空间解决方案**：

这个想法类似于这个帖子。 我们使用数组元素作为索引。 要标记元素`x`的存在，我们将索引`x`处的值更改为负。 但是，如果存在非正数（`-ve`和 0），则此方法无效。 因此，我们首先将正数与负数分开，然后应用该方法。

以下是两步算法。

1.  将正数与其他正数分开，即，将所有非正数移到左侧。 在下面的代码中，`segregate()`函数完成了这一部分。

2.  现在我们可以忽略非正元素，而只考虑包含所有正元素的数组部分。 我们遍历包含所有正数的数组，并标记元素`x`的存在，我们将索引`x`处的值符号更改为负数。 我们再次遍历数组，然后打印具有正值的第一个索引。 在下面的代码中，`findMissingPositive()`函数完成了这一部分。 请注意，在`findMissingPositive`中，由于 C 中的索引从 0 开始，所以我们从值中减去了 1。

## C++ 

```cpp

/* C++ program to find the smallest positive missing number */
#include <bits/stdc++.h> 
using namespace std; 

/* Utility to swap to integers */
void swap(int* a, int* b) 
{ 
    int temp; 
    temp = *a; 
    *a = *b; 
    *b = temp; 
} 

/* Utility function that puts all  
non-positive (0 and negative) numbers on left  
side of arr[] and return count of such numbers */
int segregate(int arr[], int size) 
{ 
    int j = 0, i; 
    for (i = 0; i < size; i++) { 
        if (arr[i] <= 0) { 
            swap(&arr[i], &arr[j]); 
            j++; // increment count of non-positive integers 
        } 
    } 

    return j; 
} 

/* Find the smallest positive missing number  
in an array that contains all positive integers */
int findMissingPositive(int arr[], int size) 
{ 
    int i; 

    // Mark arr[i] as visited by making arr[arr[i] - 1] negative. 
    // Note that 1 is subtracted because index start 
    // from 0 and positive numbers start from 1 
    for (i = 0; i < size; i++) { 
        if (abs(arr[i]) - 1 < size && arr[abs(arr[i]) - 1] > 0) 
            arr[abs(arr[i]) - 1] = -arr[abs(arr[i]) - 1]; 
    } 

    // Return the first index value at which is positive 
    for (i = 0; i < size; i++) 
        if (arr[i] > 0) 
            // 1 is added because indexes start from 0 
            return i + 1; 

    return size + 1; 
} 

/* Find the smallest positive missing  
number in an array that contains  
both positive and negative integers */
int findMissing(int arr[], int size) 
{ 
    // First separate positive and negative numbers 
    int shift = segregate(arr, size); 

    // Shift the array and call findMissingPositive for 
    // positive part 
    return findMissingPositive(arr + shift, size - shift); 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 0, 10, 2, -10, -20 }; 
    int arr_size = sizeof(arr) / sizeof(arr[0]); 
    int missing = findMissing(arr, arr_size); 
    cout << "The smallest positive missing number is " << missing; 
    return 0; 
} 

// This is code is contributed by rathbhupendra 

```

## C

```c

/* C program to find the smallest positive missing number */
#include <stdio.h> 
#include <stdlib.h> 

/* Utility to swap to integers */
void swap(int* a, int* b) 
{ 
    int temp; 
    temp = *a; 
    *a = *b; 
    *b = temp; 
} 

/* Utility function that puts all 
non-positive (0 and negative) numbers on left  
side of arr[] and return count of such numbers */
int segregate(int arr[], int size) 
{ 
    int j = 0, i; 
    for (i = 0; i < size; i++) { 
        if (arr[i] <= 0) { 
            swap(&arr[i], &arr[j]); 
            j++; // increment count of non-positive integers 
        } 
    } 

    return j; 
} 

/* Find the smallest positive missing number  
in an array that contains all positive integers */
int findMissingPositive(int arr[], int size) 
{ 
    int i; 

    // Mark arr[i] as visited by making arr[arr[i] - 1] negative. 
    // Note that 1 is subtracted because index start 
    // from 0 and positive numbers start from 1 
    for (i = 0; i < size; i++) { 
        if (abs(arr[i]) - 1 < size && arr[abs(arr[i]) - 1] > 0) 
            arr[abs(arr[i]) - 1] = -arr[abs(arr[i]) - 1]; 
    } 

    // Return the first index value at which is positive 
    for (i = 0; i < size; i++) 
        if (arr[i] > 0) 
            // 1 is added because indexes start from 0 
            return i + 1; 

    return size + 1; 
} 

/* Find the smallest positive missing  
number in an array that contains 
both positive and negative integers */
int findMissing(int arr[], int size) 
{ 
    // First separate positive and negative numbers 
    int shift = segregate(arr, size); 

    // Shift the array and call findMissingPositive for 
    // positive part 
    return findMissingPositive(arr + shift, size - shift); 
} 

int main() 
{ 
    int arr[] = { 0, 10, 2, -10, -20 }; 
    int arr_size = sizeof(arr) / sizeof(arr[0]); 
    int missing = findMissing(arr, arr_size); 
    printf("The smallest positive missing number is %d ", missing); 
    getchar(); 
    return 0; 
} 

```

## Java

```java

// Java program to find the smallest 
// positive missing number 
import java.util.*; 

class Main { 

    /* Utility function that puts all non-positive  
       (0 and negative) numbers on left side of  
       arr[] and return count of such numbers */
    static int segregate(int arr[], int size) 
    { 
        int j = 0, i; 
        for (i = 0; i < size; i++) { 
            if (arr[i] <= 0) { 
                int temp; 
                temp = arr[i]; 
                arr[i] = arr[j]; 
                arr[j] = temp; 
                // increment count of non-positive 
                // integers 
                j++; 
            } 
        } 

        return j; 
    } 

    /* Find the smallest positive missing  
       number in an array that contains 
       all positive integers */
    static int findMissingPositive(int arr[], int size) 
    { 
        int i; 

        // Mark arr[i] as visited by making 
        // arr[arr[i] - 1] negative. Note that 
        // 1 is subtracted because index start 
        // from 0 and positive numbers start from 1 
        for (i = 0; i < size; i++) { 
            int x = Math.abs(arr[i]); 
            if (x - 1 < size && arr[x - 1] > 0) 
                arr[x - 1] = -arr[x - 1]; 
        } 

        // Return the first index value at which 
        // is positive 
        for (i = 0; i < size; i++) 
            if (arr[i] > 0) 
                return i + 1; // 1 is added becuase indexes 
        // start from 0 

        return size + 1; 
    } 

    /* Find the smallest positive missing  
       number in an array that contains 
       both positive and negative integers */
    static int findMissing(int arr[], int size) 
    { 
        // First separate positive and 
        // negative numbers 
        int shift = segregate(arr, size); 
        int arr2[] = new int[size - shift]; 
        int j = 0; 
        for (int i = shift; i < size; i++) { 
            arr2[j] = arr[i]; 
            j++; 
        } 
        // Shift the array and call 
        // findMissingPositive for 
        // positive part 
        return findMissingPositive(arr2, j); 
    } 
    // main function 
    public static void main(String[] args) 
    { 
        int arr[] = { 0, 10, 2, -10, -20 }; 
        int arr_size = arr.length; 
        int missing = findMissing(arr, arr_size); 
        System.out.println("The smallest positive missing number is " + missing); 
    } 
} 

```

## Python

```

''' Python program to find the  
smallest positive missing number '''

''' Utility function that puts all  
non-positive (0 and negative) numbers on left  
side of arr[] and return count of such numbers '''
def segregate(arr, size): 
    j = 0
    for i in range(size): 
        if (arr[i] <= 0): 
            arr[i], arr[j] = arr[j], arr[i] 
            j += 1 # increment count of non-positive integers  
    return j  

''' Find the smallest positive missing number  
in an array that contains all positive integers '''
def findMissingPositive(arr, size): 

    # Mark arr[i] as visited by making arr[arr[i] - 1] negative.  
    # Note that 1 is subtracted because index start  
    # from 0 and positive numbers start from 1  
    for i in range(size): 
        if (abs(arr[i]) - 1 < size and arr[abs(arr[i]) - 1] > 0): 
            arr[abs(arr[i]) - 1] = -arr[abs(arr[i]) - 1] 

    # Return the first index value at which is positive  
    for i in range(size): 
        if (arr[i] > 0): 

            # 1 is added because indexes start from 0  
            return i + 1
    return size + 1

''' Find the smallest positive missing  
number in an array that contains  
both positive and negative integers '''
def findMissing(arr, size): 

    # First separate positive and negative numbers  
    shift = segregate(arr, size) 

    # Shift the array and call findMissingPositive for  
    # positive part  
    return findMissingPositive(arr[shift:], size - shift)  

# Driver code  
arr = [ 0, 10, 2, -10, -20 ] 
arr_size = len(arr)  
missing = findMissing(arr, arr_size)  
print("The smallest positive missing number is ", missing) 

# This code is contributed by Shubhamsingh10 

```

## C# 

```cs

// C# program to find the smallest 
// positive missing number 
using System; 

class main { 

    // Utility function that puts all 
    // non-positive (0 and negative) 
    // numbers on left side of arr[] 
    // and return count of such numbers 
    static int segregate(int[] arr, int size) 
    { 
        int j = 0, i; 
        for (i = 0; i < size; i++) { 
            if (arr[i] <= 0) { 
                int temp; 
                temp = arr[i]; 
                arr[i] = arr[j]; 
                arr[j] = temp; 

                // increment count of non-positive 
                // integers 
                j++; 
            } 
        } 

        return j; 
    } 

    // Find the smallest positive missing 
    // number in an array that contains 
    // all positive integers 
    static int findMissingPositive(int[] arr, int size) 
    { 
        int i; 

        // Mark arr[i] as visited by making 
        // arr[arr[i] - 1] negative. Note that 
        // 1 is subtracted as index start from 
        // 0 and positive numbers start from 1 
        for (i = 0; i < size; i++) { 
            if (Math.Abs(arr[i]) - 1 < size && arr[ Math.Abs(arr[i]) - 1] > 0) 
                arr[ Math.Abs(arr[i]) - 1] = -arr[ Math.Abs(arr[i]) - 1]; 
        } 

        // Return the first index value at 
        // which is positive 
        for (i = 0; i < size; i++) 
            if (arr[i] > 0) 
                return i + 1; 

        // 1 is added becuase indexes 
        // start from 0 
        return size + 1; 
    } 

    // Find the smallest positive 
    // missing number in array that 
    // contains both positive and 
    // negative integers 
    static int findMissing(int[] arr, int size) 
    { 

        // First separate positive and 
        // negative numbers 
        int shift = segregate(arr, size); 
        int[] arr2 = new int[size - shift]; 
        int j = 0; 

        for (int i = shift; i < size; i++) { 
            arr2[j] = arr[i]; 
            j++; 
        } 

        // Shift the array and call 
        // findMissingPositive for 
        // positive part 
        return findMissingPositive(arr2, j); 
    } 

    // main function 
    public static void Main() 
    { 
        int[] arr = { 0, 10, 2, -10, -20 }; 
        int arr_size = arr.Length; 
        int missing = findMissing(arr, arr_size); 
        Console.WriteLine("The smallest positive missing number is " + missing); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

**输出**：

```
The smallest positive missing number is 1 
```

请注意，此方法会修改原始数组。 我们可以更改分隔数组中元素的符号，以获取相同的元素集。 但是我们仍然放开元素的顺序。 如果我们想保持原始数组不变，则可以创建该数组的副本，然后在`temp`数组上运行此方法。

**另一种方法**：在此问题中，我们创建了一个全为 0 的列表，其大小为给定数组的`max()`值。 现在，只要我们在原始数组中遇到任何正值，就将列表的索引值更改为 1。因此，完成后，我们简单地遍历修改后的列表，即遇到的第一个 0，即（索引值`+1`）应该是我们的答案，因为 python 中的索引从 0 开始。

下面是上述方法的实现：

## C++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the first missing positive 
// number from the given unsorted array 
int firstMissingPos(int A[], int n) 
{ 

    // To mark the occurrence of elements 
    bool present[n + 1] = { false }; 

    // Mark the occurrences 
    for (int i = 0; i < n; i++) { 

        // Only mark the required elements 
        // All non-positive elements and 
        // the elements greater n + 1 will never 
        // be the answer 
        // For example, the array will be {1, 2, 3} 
        // in the worst case and the result 
        // will be 4 which is n + 1 
        if (A[i] > 0 && A[i] <= n) 
            present[A[i]] = true; 
    } 

    // Find the first element which didn't 
    // appear in the original array 
    for (int i = 1; i <= n; i++) 
        if (!present[i]) 
            return i; 

    // If the original array was of the 
    // type {1, 2, 3} in its sorted form 
    return n + 1; 
} 

// Driver code 
int main() 
{ 

    int A[] = { 0, 10, 2, -10, -20 }; 
    int size = sizeof(A) / sizeof(A[0]); 
    cout << firstMissingPos(A, size); 
} 

// This code is contributed by gp6 

```

## C++

```
// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 
  
// Function to return the first missing positive 
// number from the given unsorted array 
int firstMissingPos(int A[], int n) 
{ 
  
    // To mark the occurrence of elements 
    bool present[n + 1] = { false }; 
  
    // Mark the occurrences 
    for (int i = 0; i < n; i++) { 
  
        // Only mark the required elements 
        // All non-positive elements and 
        // the elements greater n + 1 will never 
        // be the answer 
        // For example, the array will be {1, 2, 3} 
        // in the worst case and the result 
        // will be 4 which is n + 1 
        if (A[i] > 0 && A[i] <= n) 
            present[A[i]] = true; 
    } 
  
    // Find the first element which didn't 
    // appear in the original array 
    for (int i = 1; i <= n; i++) 
        if (!present[i]) 
            return i; 
  
    // If the original array was of the 
    // type {1, 2, 3} in its sorted form 
    return n + 1; 
} 
  
// Driver code 
int main() 
{ 
  
    int A[] = { 0, 10, 2, -10, -20 }; 
    int size = sizeof(A) / sizeof(A[0]); 
    cout << firstMissingPos(A, size); 
} 
  
// This code is contributed by gp6
```

## Java

```
// Java Program to find the smallest 
// positive missing number 
import java.util.Arrays; 
public class GFG { 
  
    static int solution(int[] A) 
    { 
        int n = A.length; 
  
        // To mark the occurrence of elements 
        boolean[] present = new boolean[n + 1]; 
  
        // Mark the occurrences 
        for (int i = 0; i < n; i++) { 
  
            // Only mark the required elements 
            // All non-positive elements and 
            // the elements greater n + 1 will never 
            // be the answer 
            // For example, the array will be {1, 2, 3} 
            // in the worst case and the result 
            // will be 4 which is n + 1 
            if (A[i] > 0 && A[i] <= n) 
                present[A[i]] = true; 
        } 
  
        // Find the first element which didn't 
        // appear in the original array 
        for (int i = 1; i <= n; i++) 
            if (!present[i]) 
                return i; 
  
        // If the original array was of the 
        // type {1, 2, 3} in its sorted form 
        return n + 1; 
    } 
  
    public static void main(String[] args) 
    { 
  
        int A[] = { 0, 10, 2, -10, -20 }; 
        System.out.println(solution(A)); 
    } 
} 
// This code is contributed by 29AjayKumar
```

## Python 3

```
# Python Program to find the smallest 
# positive missing number 
  
def solution(A):# Our original array 
  
    m = max(A) # Storing maximum value 
    if m < 1: 
          
        # In case all values in our array are negative 
        return 1 
    if len(A) == 1: 
          
        # If it contains only one element 
        return 2 if A[0] == 1 else 1     
    l = [0] * m 
    for i in range(len(A)): 
        if A[i] > 0: 
            if l[A[i] - 1] != 1: 
                  
                # Changing the value status at the index of our list 
                l[A[i] - 1] = 1 
    for i in range(len(l)): 
          
        # Encountering first 0, i.e, the element with least value 
        if l[i] == 0:  
            return i + 1
            # In case all values are filled between 1 and m 
    return i + 2     
  
A = [0, 10, 2, -10, -20] 
print(solution(A))
```

## C#

```
// C# Program to find the smallest 
// positive missing number 
using System; 
using System.Linq; 
  
class GFG { 
    static int solution(int[] A) 
    { 
        // Our original array 
  
        int m = A.Max(); // Storing maximum value 
  
        // In case all values in our array are negative 
        if (m < 1) { 
            return 1; 
        } 
        if (A.Length == 1) { 
  
            // If it contains only one element 
            if (A[0] == 1) { 
                return 2; 
            } 
            else { 
                return 1; 
            } 
        } 
        int i = 0; 
        int[] l = new int[m]; 
        for (i = 0; i < A.Length; i++) { 
            if (A[i] > 0) { 
                // Changing the value status at the index of our list 
                if (l[A[i] - 1] != 1) { 
                    l[A[i] - 1] = 1; 
                } 
            } 
        } 
  
        // Encountering first 0, i.e, the element with least value 
        for (i = 0; i < l.Length; i++) { 
            if (l[i] == 0) { 
                return i + 1; 
            } 
        } 
  
        // In case all values are filled between 1 and m 
        return i + 2; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] A = { 0, 10, 2, -10, -20 }; 
        Console.WriteLine(solution(A)); 
    } 
} 
  
// This code is contributed by PrinciRaj1992
```

## PHP

```
<?php  
// PHP Program to find the smallest 
// positive missing number 
   
function solution($A){//Our original array 
   
    $m = max($A); //Storing maximum value 
    if ($m < 1) 
    {          
        // In case all values in our array are negative 
        return 1; 
    } 
    if (sizeof($A) == 1) 
    {   
        //If it contains only one element 
        if ($A[0] == 1) 
            return 2 ; 
        else 
            return 1 ; 
    }         
    $l = array_fill(0, $m, NULL); 
    for($i = 0; $i < sizeof($A); $i++) 
    {         
        if( $A[$i] > 0) 
        { 
            if ($l[$A[$i] - 1] != 1) 
            { 
                  
                //Changing the value status at the index of our list 
                $l[$A[$i] - 1] = 1; 
            } 
        } 
    } 
    for ($i = 0;$i < sizeof($l); $i++) 
    { 
           
        //Encountering first 0, i.e, the element with least value 
        if ($l[$i] == 0)  
            return $i+1; 
    } 
            //In case all values are filled between 1 and m 
    return $i+2;     
} 
  
$A = array(0, 10, 2, -10, -20); 
echo solution($A); 
return 0; 
?>
```

输出：

```
 1 
```

