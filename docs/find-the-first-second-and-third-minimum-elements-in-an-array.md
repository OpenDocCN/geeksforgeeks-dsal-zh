# 在数组中找到第一个，第二个和第三小元素

> 原文： [https://www.geeksforgeeks.org/find-the-first-second-and-third-minimum-elements-in-an-array/](https://www.geeksforgeeks.org/find-the-first-second-and-third-minimum-elements-in-an-array/)

在`O(n)`中找到数组中的第一，第二和第三最小元素。

例子：

```
Input : 9 4 12 6
Output : First min = 4
         Second min = 6
         Third min = 9

Input : 4 9 1 32 12
Output : First min = 1
         Second min = 4
         Third min = 9

```



**第一种方法**：首先，我们可以使用常规方法对数组进行排序，然后打印数组的第一，第二和第三元素。 该解决方案的时间复杂度为`O(N log N)`。

**第二种方法**：此解决方案的时间复杂度为`O(n)`。

算法-

```
First take an element
then if array[index] < Firstelement
        Thirdelement = Secondelement
        Secondelement = Firstelement
        Firstelement = array[index]
     else if array[index] < Secondelement
        Thirdelement = Secondelement
        Secondelement = array[index]
     else if array[index] < Thirdelement
        Thirdelement = array[index]

then print all the element 

```

## C++ 

```cpp

// CPP program to find the first, second 
// and third minimum element in an array 
#include<bits/stdc++.h> 
#define MAX 100000 
using namespace std; 

int Print3Smallest(int array[], int n) 
{ 
    int firstmin = MAX, secmin = MAX, thirdmin = MAX; 
    for (int i = 0; i < n; i++) 
    { 
        /* Check if current element is less than 
           firstmin, then update first, second and 
           third */
        if (array[i] < firstmin) 
        { 
            thirdmin = secmin; 
            secmin = firstmin; 
            firstmin = array[i]; 
        } 

        /* Check if current element is less than 
        secmin then update second and third */
        else if (array[i] < secmin) 
        { 
            thirdmin = secmin; 
            secmin = array[i]; 
        } 

        /* Check if current element is less than 
        then update third */
        else if (array[i] < thirdmin) 
            thirdmin = array[i]; 
    } 

    cout << "First min = " << firstmin << "\n"; 
    cout << "Second min = " << secmin << "\n"; 
    cout << "Third min = " << thirdmin << "\n"; 
} 

// Driver code 
int main() 
{ 
    int array[] = {4, 9, 1, 32, 12}; 
    int n = sizeof(array) / sizeof(array[0]); 
    Print3Smallest(array, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find the first, second 
// and third minimum element in an array 
import java.util.*; 

public class GFG 
{ 
    static void Print3Smallest(int array[], int n) 
    { 
            int firstmin = Integer.MAX_VALUE; 
            int secmin = Integer.MAX_VALUE;  
            int thirdmin = Integer.MAX_VALUE; 
            for (int i = 0; i < n; i++) 
            { 
                /* Check if current element is less than 
                firstmin, then update first, second and 
                third */
                if (array[i] < firstmin) 
                { 
                    thirdmin = secmin; 
                    secmin = firstmin; 
                    firstmin = array[i]; 
                } 

                /* Check if current element is less than 
                secmin then update second and third */
                else if (array[i] < secmin) 
                { 
                    thirdmin = secmin; 
                    secmin = array[i]; 
                } 

                /* Check if current element is less than 
                then update third */
                else if (array[i] < thirdmin) 
                    thirdmin = array[i]; 
            } 

            System.out.println("First min = " + firstmin ); 
            System.out.println("Second min = " + secmin ); 
            System.out.println("Third min = " + thirdmin ); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
            int array[] = {4, 9, 1, 32, 12}; 
            int n = array.length; 
            Print3Smallest(array, n); 
    } 

} 

// This code is contributed by  
// Sam007 

```

## Python3

```py

# A Python program to find the first, 
# second and third minimum element  
# in an array 

MAX = 100000

def Print3Smallest(arr, n): 
    firstmin = MAX
    secmin = MAX
    thirdmin = MAX

    for i in range(0, n): 

        # Check if current element 
        # is less than firstmin,  
        # then update first,second 
        # and third 

        if arr[i] < firstmin: 
            thirdmin = secmin 
            secmin = firstmin 
            firstmin = arr[i] 

        # Check if current element is 
        # less than secmin then update 
        # second and third 
        elif arr[i] < secmin: 
            thirdmin = secmin 
            secmin = arr[i] 

        # Check if current element is 
        # less than,then upadte third 
        elif arr[i] < thirdmin: 
            thirdmin = arr[i] 

    print("First min = ", firstmin) 
    print("Second min = ", secmin) 
    print("Third min = ", thirdmin) 

# driver program 
arr = [4, 9, 1, 32, 12] 
n = len(arr) 
Print3Smallest(arr, n) 

# This code is contributed by Shrikant13\. 

```

## C# 

```cs

// C# program to find the first, second 
// and third minimum element in an array 
using System; 

class GFG 
{ 
static void Print3Smallest(int []array, int n) 
    { 
            int firstmin = int.MaxValue; 
            int secmin = int.MaxValue;  
            int thirdmin = int.MaxValue; 

            for (int i = 0; i < n; i++) 
            { 
                /* Check if current element is less than 
                firstmin, then update first, second and 
                third */
                if (array[i] < firstmin) 
                { 
                    thirdmin = secmin; 
                    secmin = firstmin; 
                    firstmin = array[i]; 
                } 

                /* Check if current element is less than 
                secmin then update second and third */
                else if (array[i] < secmin) 
                { 
                    thirdmin = secmin; 
                    secmin = array[i]; 
                } 

                /* Check if current element is less than 
                then update third */
                else if (array[i] < thirdmin) 
                    thirdmin = array[i]; 
            } 

            Console.WriteLine("First min = " + firstmin ); 
            Console.WriteLine("Second min = " + secmin ); 
            Console.WriteLine("Third min = " + thirdmin ); 
    } 

    // Driver code 
    static void Main() 
    { 
    int []array = new int[]{4, 9, 1, 32, 12}; 
    int n = array.Length; 
    Print3Smallest(array, n); 

    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php 
// php program to find the first, second 
// and third minimum element in an array 

function Print3Smallest($array, $n) 
{ 
    $MAX = 100000; 
    $firstmin = $MAX; 
    $secmin = $MAX; 
    $thirdmin = $MAX; 
    for ($i = 0; $i < $n; $i++) 
    { 

        /* Check if current element is less than 
        firstmin, then update first, second and 
        third */
        if ($array[$i] < $firstmin) 
        { 
            $thirdmin = $secmin; 
            $secmin = $firstmin; 
            $firstmin = $array[$i]; 
        } 

        /* Check if current element is less than 
        secmin then update second and third */
        else if ($array[$i] < $secmin) 
        { 
            $thirdmin = $secmin; 
            $secmin = $array[$i]; 
        } 

        /* Check if current element is less than 
        then update third */
        else if ($array[$i] < $thirdmin) 
            $thirdmin = $array[$i]; 
    } 

    echo "First min = ".$firstmin."\n"; 
    echo "Second min = ".$secmin."\n"; 
    echo "Third min = ".$thirdmin."\n"; 
} 

// Driver code 
    $array= array(4, 9, 1, 32, 12); 
    $n = sizeof($array) / sizeof($array[0]); 
    Print3Smallest($array, $n); 

// This code is contributed by mits 
?> 

```

Output:

```
First min = 1
Second min = 4
Third min = 9

```



* * *

* * *



