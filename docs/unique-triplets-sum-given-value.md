# 总和为给定值的唯一三元组

> 原文： [https://www.geeksforgeeks.org/unique-triplets-sum-given-value/](https://www.geeksforgeeks.org/unique-triplets-sum-given-value/)

给定一个数组和一个求和值，请在该数组中找到所有总和等于给定和值的唯一三元组。 如果无法从数组中形成这样的三元组，则打印`"No triplets can be formed."`，否则打印所有唯一的三元组。 例如，如果给定数组为`{12, 3, 6, 1, 6, 9}`，给定总和为 24，则唯一三元组为`(3, 9, 12)`和`(6, 6, 12)`，其总和为 24

**示例**：

```
Input : array = {12, 3, 6, 1, 6, 9} sum = 24
Output : [[3, 9, 12], [6, 6, 12]]

Input : array = {-2, 0, 1, 1, 2} sum = 0
Output : [[-2, 0, 2], [-2, 1, 1]]

Input : array = {-2, 0, 1, 1, 2} sum = 10
Output : No triplets can be formed

```



在[上一篇文章](https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/)中，找到一个三元组，其总和为给定值，我们讨论了三元组是否可以由数组形成。

在这里，我们需要打印所有总计为给定值的唯一的三元组。

1\. 对输入数组进行排序。

2\. 从数组`i`，`j`和`k`中找到三个索引，其中`A[i] + A[j] + A[k]`等于给定的总和值。

3\. 将第一个元素固定为`A[i]`，然后将`i`从 0 迭代到数组大小 –2。

4\. 对于`i`的每次迭代，取`j`为其余元素中第一个元素的索引，`k`是最后一个元素的索引。

5\. 检查三元组组合`A[i] + A[j] + A[k]`等于给定的总和值。

6\. 如果获得三元组（即，`A[i] + A[j] + A[k]`等于给定的总和），则：

……6.1 将所有三元组添加到具有`:`分隔值的树集中，以获取唯一的三元组；

……6.2 增加第二个值索引；

……6.3 减少第三个值索引；

……6.4 重复步骤 4 和 5 直到`j < k`。

7\. 否则，如果`A[i] + A[j] + A[k]`小于给定总和值，则增加第二个值索引。

8\. 否则，如果`A[i] + A[j] + A[k]`大于给定总和值，则减少第三值索引。

## C++ 

```cpp

// C++ program to find unique triplets 
// that sum up to a given value. 
#include <bits/stdc++.h> 
using namespace std; 

// Structure to define a triplet. 
struct triplet{ 
    int first, second, third; 
}; 

// Function to find unique triplets that 
// sum up to a given value. 
int findTriplets(int nums[], int n, int sum) 
{ 
    int i, j, k; 

    // Vector to store all unique triplets. 
    vector <triplet> triplets; 

    // Set to store already found triplets 
    // to avoid duplication. 
    unordered_set <string> uniqTriplets; 

    // Variable used to hold triplet  
    // converted to string form. 
    string temp; 

    // Variable used to store current 
    // triplet which is stored in vector 
    // if it is unique. 
    triplet newTriplet; 

    // Sort the input array. 
    sort(nums, nums + n); 

    // Iterate over the array from the 
    // start and consider it as the  
    // first element. 
    for(i = 0; i < n - 2; i++){ 

        // index of the first element in  
        // the remaining elements. 
        j = i + 1; 

        // index of the last element. 
        k = n - 1; 

        while(j < k){ 

            // If sum of triplet is equal to  
            // given value, then check if 
            // this triplet is unique or not. 
            // To check uniqueness, convert  
            // triplet to string form and 
            // then check if this string is  
            // present in set or not. If  
            // triplet is unique, then store 
            // it in vector. 
            if(nums[i] + nums[j] + nums[k] == sum) 
            { 
                temp = to_string(nums[i]) + " : " 
                     + to_string(nums[j]) + " : "
                             + to_string(nums[k]); 
                if(uniqTriplets.find(temp) ==  
                                uniqTriplets.end()) 
                { 
                    uniqTriplets.insert(temp); 
                    newTriplet.first = nums[i]; 
                    newTriplet.second = nums[j]; 
                    newTriplet.third = nums[k]; 
                    triplets.push_back(newTriplet); 
                } 

                // Increment the first index  
                // and decrement the last 
                // index of remaining elements. 
                j++; 
                k--; 
            } 

            // If sum is greater than given  
            // value then to reduce sum  
            // decrement the last index. 
            else if(nums[i] + nums[j] + 
                                 nums[k] > sum) 
                k--; 

            // If sum is less than given value 
            // then to increase sum increment  
            // the first index of remaining 
            // elements. 
            else
                j++; 
        } 
    } 

    // If no unique triplet is found, then 
    // return 0\. 
    if(triplets.size() == 0) 
        return 0; 

    // Print all unique triplets stored in  
    // vector. 
    for(i = 0; i < triplets.size(); i++) 
    { 
        cout << "[" << triplets[i].first  
            << ", " << triplets[i].second 
          << ", " << triplets[i].third <<"], "; 
    } 
} 

// Driver Function. 
int main()  
{ 
    int nums[] = { 12, 3, 6, 1, 6, 9 }; 
    int n = sizeof(nums) / sizeof(nums[0]); 
    int sum = 24; 
    if(!findTriplets(nums, n, sum)) 
        cout << "No triplets can be formed."; 

    return 0; 
} 

// This code is contributed by NIKHIL JINDAL. 

```

## Java

```java

// Java program to find all triplets with given sum 
import java.util.*; 

public class triplets { 

    // returns all triplets whose sum is equal to sum value 
    public static List<List<Integer> > findTriplets(int[] nums, int sum) 
    { 

        /* Sort the elements */
        Arrays.sort(nums); 

        List<List<Integer> > pair = new ArrayList<>(); 
        TreeSet<String> set = new TreeSet<String>(); 
        List<Integer> triplets = new ArrayList<>(); 

        /* Iterate over the array from the start and  
           consider it as the first element*/
        for (int i = 0; i < nums.length - 2; i++) { 

            // index of the first element in the 
            // remaining elements 
            int j = i + 1; 

            // index of the last element 
            int k = nums.length - 1; 

            while (j < k) { 

                if (nums[i] + nums[j] + nums[k] == sum) { 

                    String str = nums[i] + ":" + nums[j] + ":" + nums[k]; 

                    if (!set.contains(str)) { 

                        // To check for the unique triplet 
                        triplets.add(nums[i]); 
                        triplets.add(nums[j]); 
                        triplets.add(nums[k]); 
                        pair.add(triplets); 
                        triplets = new ArrayList<>(); 
                        set.add(str); 
                    } 

                    j++; // increment the second value index 
                    k--; // decrement the third value index 

                } else if (nums[i] + nums[j] + nums[k] < sum) 
                    j++; 

                else // nums[i] + nums[j] + nums[k] > sum 
                    k--; 
            } 
        } 
        return pair; 
    } 

    public static void main(String[] args) 
    { 
        int[] nums = { 12, 3, 6, 1, 6, 9 }; 
        int sum = 24; 

        List<List<Integer> > triplets = findTriplets(nums, sum); 

        if (!triplets.isEmpty()) { 
            System.out.println(triplets); 
        } else { 
            System.out.println("No triplets can be formed"); 
        } 
    } 
} 

```

## C# 

```cs

// C# program to find all triplets with given sum 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

    // returns all triplets whose sum is equal to sum value 
    public static List<List<int>> findTriplets(int[] nums,  
                                               int sum) 
    { 

        /* Sort the elements */
        Array.Sort(nums); 

        List<List<int> > pair = new List<List<int>>(); 
        SortedSet<String> set = new SortedSet<String>(); 
        List<int> triplets = new List<int>(); 

        /* Iterate over the array from the start and  
        consider it as the first element*/
        for (int i = 0; i < nums.Length - 2; i++) 
        { 

            // index of the first element in the 
            // remaining elements 
            int j = i + 1; 

            // index of the last element 
            int k = nums.Length - 1; 

            while (j < k)  
            { 
                if (nums[i] + nums[j] + nums[k] == sum) 
                { 
                    String str = nums[i] + ":" +  
                                 nums[j] + ":" + nums[k]; 

                    if (!set.Contains(str)) 
                    { 

                        // To check for the unique triplet 
                        triplets.Add(nums[i]); 
                        triplets.Add(nums[j]); 
                        triplets.Add(nums[k]); 
                        pair.Add(triplets); 
                        triplets = new List<int>(); 
                        set.Add(str); 
                    } 

                    j++; // increment the second value index 
                    k--; // decrement the third value index 

                }  
                else if (nums[i] + nums[j] + nums[k] < sum) 
                    j++; 

                else // nums[i] + nums[j] + nums[k] > sum 
                    k--; 
            } 
        } 
        return pair; 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        int[] nums = { 12, 3, 6, 1, 6, 9 }; 
        int sum = 24; 

        List<List<int> > triplets = findTriplets(nums, sum); 

        if (triplets.Count != 0) 
        { 
            Console.Write("["); 
            for(int i = 0; i < triplets.Count; i++) 
            { 
                List<int> l = triplets[i]; 
                Console.Write("["); 
                for(int j = 0; j < l.Count; j++) 
                { 
                    Console.Write(l[j]); 
                    if (l.Count != j + 1) 
                        Console.Write(", "); 
                } 
                Console.Write("]"); 
                if (triplets.Count != i + 1) 
                    Console.Write(","); 
            } 
            Console.Write("]"); 
        } 
        else 
        { 
            Console.WriteLine("No triplets can be formed"); 
        } 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
[[3, 9, 12], [6, 6, 12]]

```

**时间复杂度**：`O(n^2)`。

