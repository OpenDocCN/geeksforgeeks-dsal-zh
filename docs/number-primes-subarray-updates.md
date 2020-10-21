# 子数组中的素数（带有更新）

> 原文： [https://www.geeksforgeeks.org/number-primes-subarray-updates/](https://www.geeksforgeeks.org/number-primes-subarray-updates/)

给定一个由`N`个整数组成的数组，任务是执行以下两个查询：

+   `query(start, end)`：从头到尾打印子数组中的质数数。

+   `update(i, x)`：将索引`i`的值更新为`x`，即`arr[i] = x`。

例子：

```
Input : arr = {1, 2, 3, 5, 7, 9}
        Query 1: query(start = 0, end = 4)
        Query 2: update(i = 3, x = 6)
        Query 3: query(start = 0, end = 4)
Output :4
        3
Explanation
In Query 1, the subarray [0...4]
has 4 primes viz. {2, 3, 5, 7}

In Query 2, the value at index 3 
is updated to 6, the array arr now is, {1, 2, 3, 
6, 7, 9}
In Query 3, the subarray [0...4]
has 4 primes viz. {2, 3, 7}
```



**方法 1（暴力）**：

在这里可以找到类似的问题。 这里没有更新，我们可以对其进行修改以处理更新，但是为此，我们总是在执行更新时需要构建前缀数组，这会使这种方法的时间复杂度为`O(Q * N)`。

**方法 2（高效）**：

由于我们需要处理范围查询和点更新，因此段树最适合此目的。

我们可以使用 [Eratosthenes 筛子](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)预处理所有素数，直到最大值`arr[i]`在`O(MAX log(log(MAX)))`。

**构建段树**：

我们基本上使用段树将问题简化为[子数组和](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。

现在，我们可以构建段树，其中叶节点表示为 0（如果不是素数）或 1（如果是素数）。

段树的内部节点等于其子节点的总和，因此，一个节点表示从`L`到`R`的范围内的总素数，其中`L`到`R`的范围落在该节点下，而在其下方的子树也是如此。

**处理查询和点更新**：

每当我们从头到尾进行查询时，我们都可以查询段树以查找范围开始到结束的节点总数，这又代表了范围开始到结束的素数。

如果需要执行点更新并将索引`i`处的值更新为`x`，则我们检查以下情况：

```

Let the old value of arri be y and the new value be x

Case 1: If x and y both are primes
Count of primes in the subarray does not change so we just update array and donot
modify the segment tree

Case 2: If x and y both are non primes
Count of primes in the subarray does not change so we just update array and donot
modify the segment tree

Case 3: If y is prime but x is non prime
Count of primes in the subarray decreases so we update array and add -1 to every 
range, the index i which is to be updated, is a part of in the segment tree

Case 4: If y is non prime but x is prime
Count of primes in the subarray increases so we update array and add 1 to every 
range, the index i which is to be updated, is a part of in the segment tree

```

## CPP

```

// C++ program to find number of prime numbers in a  
// subarray and performing updates 
#include <bits/stdc++.h> 
using namespace std; 

#define MAX 1000 

void sieveOfEratosthenes(bool isPrime[]) 
{ 
    isPrime[1] = false; 

    for (int p = 2; p * p <= MAX; p++) { 

        // If prime[p] is not changed, then 
        // it is a prime 
        if (isPrime[p] == true) { 

            // Update all multiples of p 
            for (int i = p * 2; i <= MAX; i += p) 
                isPrime[i] = false; 
        } 
    } 
} 

// A utility function to get the middle index from corner indexes. 
int getMid(int s, int e) { return s + (e - s) / 2; } 

/*  A recursive function to get the number of primes in a given range 
     of array indexes. The following are parameters for this function. 

    st    --> Pointer to segment tree 
    index --> Index of current node in the segment tree. Initially 
              0 is passed as root is always at index 0 
    ss & se  --> Starting and ending indexes of the segment represented 
                  by current node, i.e., st[index] 
    qs & qe  --> Starting and ending indexes of query range */
int queryPrimesUtil(int* st, int ss, int se, int qs, int qe, int index) 
{ 
    // If segment of this node is a part of given range, then return 
    // the number of primes in the segment 
    if (qs <= ss && qe >= se) 
        return st[index]; 

    // If segment of this node is outside the given range 
    if (se < qs || ss > qe) 
        return 0; 

    // If a part of this segment overlaps with the given range 
    int mid = getMid(ss, se); 
    return queryPrimesUtil(st, ss, mid, qs, qe, 2 * index + 1) +  
           queryPrimesUtil(st, mid + 1, se, qs, qe, 2 * index + 2); 
} 

/* A recursive function to update the nodes which have the given  
   index in their range. The following are parameters 
    st, si, ss and se are same as getSumUtil() 
    i    --> index of the element to be updated. This index is  
             in input array. 
   diff --> Value to be added to all nodes which have i in range */
void updateValueUtil(int* st, int ss, int se, int i, int diff, int si) 
{ 
    // Base Case: If the input index lies outside the range of 
    // this segment 
    if (i < ss || i > se) 
        return; 

    // If the input index is in range of this node, then update 
    // the value of the node and its children 
    st[si] = st[si] + diff; 
    if (se != ss) { 
        int mid = getMid(ss, se); 
        updateValueUtil(st, ss, mid, i, diff, 2 * si + 1); 
        updateValueUtil(st, mid + 1, se, i, diff, 2 * si + 2); 
    } 
} 

// The function to update a value in input array and segment tree. 
// It uses updateValueUtil() to update the value in segment tree 
void updateValue(int arr[], int* st, int n, int i, int new_val, 
                                               bool isPrime[]) 
{ 
    // Check for erroneous input index 
    if (i < 0 || i > n - 1) { 
        printf("Invalid Input"); 
        return; 
    } 

    int diff, oldValue; 

    oldValue = arr[i]; 

    // Update the value in array 
    arr[i] = new_val; 

    // Case 1: Old and new values both are primes 
    if (isPrime[oldValue] && isPrime[new_val]) 
        return; 

    // Case 2: Old and new values both non primes 
    if ((!isPrime[oldValue]) && (!isPrime[new_val])) 
        return; 

    // Case 3: Old value was prime, new value is non prime 
    if (isPrime[oldValue] && !isPrime[new_val]) { 
        diff = -1; 
    } 

    // Case 4: Old value was non prime, new_val is prime 
    if (!isPrime[oldValue] && isPrime[new_val]) { 
        diff = 1; 
    } 

    // Update the values of nodes in segment tree 
    updateValueUtil(st, 0, n - 1, i, diff, 0); 
} 

// Return number of primes in range from index qs (query start) to 
// qe (query end).  It mainly uses queryPrimesUtil() 
void queryPrimes(int* st, int n, int qs, int qe) 
{ 
    int primesInRange = queryPrimesUtil(st, 0, n - 1, qs, qe, 0); 

    cout << "Number of Primes in subarray from " << qs << " to "
         << qe << " = " << primesInRange << "\n"; 
} 

// A recursive function that constructs Segment Tree  
// for array[ss..se]. 
// si is index of current node in segment tree st 
int constructSTUtil(int arr[], int ss, int se, int* st,  
                                 int si, bool isPrime[]) 
{ 
    // If there is one element in array, check if it 
    // is prime then store 1 in the segment tree else 
    // store 0 and return 
    if (ss == se) { 

        // if arr[ss] is prime 
        if (isPrime[arr[ss]])  
            st[si] = 1;         
        else 
            st[si] = 0; 

        return st[si]; 
    } 

    // If there are more than one elements, then recur  
    // for left and right subtrees and store the sum  
    // of the two values in this node 
    int mid = getMid(ss, se); 
    st[si] = constructSTUtil(arr, ss, mid, st,  
                               si * 2 + 1, isPrime) +  
             constructSTUtil(arr, mid + 1, se, st,  
                              si * 2 + 2, isPrime); 
    return st[si]; 
} 

/* Function to construct segment tree from given array.  
   This function allocates memory for segment tree and 
   calls constructSTUtil() to fill the allocated memory */
int* constructST(int arr[], int n, bool isPrime[]) 
{ 
    // Allocate memory for segment tree 

    // Height of segment tree 
    int x = (int)(ceil(log2(n))); 

    // Maximum size of segment tree 
    int max_size = 2 * (int)pow(2, x) - 1; 

    int* st = new int[max_size]; 

    // Fill the allocated memory st 
    constructSTUtil(arr, 0, n - 1, st, 0, isPrime); 

    // Return the constructed segment tree 
    return st; 
} 

// Driver program to test above functions 
int main() 
{ 

    int arr[] = { 1, 2, 3, 5, 7, 9 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    /* Preprocess all primes till MAX. 
       Create a boolean array "isPrime[0..MAX]". 
       A value in prime[i] will finally be false  
       if i is Not a prime, else true. */

    bool isPrime[MAX + 1]; 
    memset(isPrime, true, sizeof isPrime); 
    sieveOfEratosthenes(isPrime); 

    // Build segment tree from given array 
    int* st = constructST(arr, n, isPrime); 

    // Query 1: Query(start = 0, end = 4) 
    int start = 0; 
    int end = 4; 
    queryPrimes(st, n, start, end); 

    // Query 2: Update(i = 3, x = 6), i.e Update  
    // a[i] to x 
    int i = 3; 
    int x = 6; 
    updateValue(arr, st, n, i, x, isPrime); 

    // uncomment to see array after update 
    // for(int i = 0; i < n; i++) cout << arr[i] << " "; 

    // Query 3: Query(start = 0, end = 4) 
    start = 0; 
    end = 4; 
    queryPrimes(st, n, start, end); 

    return 0; 
} 

```

## Python3

```py

# Python3 program to find number of prime numbers in a 
# subarray and performing updates 
from math import ceil, floor, log 
MAX = 1000

def sieveOfEratosthenes(isPrime): 

    isPrime[1] = False

    for p in range(2, MAX + 1): 
        if p  * p > MAX: 
            break

        # If prime[p] is not changed, then 
        # it is a prime 
        if (isPrime[p] == True): 

            # Update all multiples of p 
            for i in range(2 * p, MAX + 1, p): 
                isPrime[i] = False

# A utility function to get the middle index from corner indexes. 
def getMid(s, e): 
    return s + (e - s) // 2
# 
# /* A recursive function to get the number of primes in a given range 
#     of array indexes. The following are parameters for this function. 
# 
#     st --> Pointer to segment tree 
#     index --> Index of current node in the segment tree. Initially 
#             0 is passed as root is always at index 0 
#     ss & se --> Starting and ending indexes of the segment represented 
#                 by current node, i.e., st[index] 
#     qs & qe --> Starting and ending indexes of query range */ 
def queryPrimesUtil(st, ss, se, qs, qe, index): 

    # If segment of this node is a part of given range, then return 
    # the number of primes in the segment 
    if (qs <= ss and qe >= se): 
        return st[index] 

    # If segment of this node is outside the given range 
    if (se < qs or ss > qe): 
        return 0

    # If a part of this segment overlaps with the given range 
    mid = getMid(ss, se) 
    return queryPrimesUtil(st, ss, mid, qs, qe, 2 * index + 1) + \ 
            queryPrimesUtil(st, mid + 1, se, qs, qe, 2 * index + 2) 

# /* A recursive function to update the nodes which have the given 
# index in their range. The following are parameters 
#     st, si, ss and se are same as getSumUtil() 
#     i --> index of the element to be updated. This index is 
#             in input array. 
# diff --> Value to be added to all nodes which have i in range */ 
def updateValueUtil(st, ss, se, i, diff, si): 

    # Base Case: If the input index lies outside the range of 
    # this segment 
    if (i < ss or i > se): 
        return

    # If the input index is in range of this node, then update 
    # the value of the node and its children 
    st[si] = st[si] + diff 
    if (se != ss): 
        mid = getMid(ss, se) 
        updateValueUtil(st, ss, mid, i, diff, 2 * si + 1) 
        updateValueUtil(st, mid + 1, se, i, diff, 2 * si + 2) 

# The function to update a value in input array and segment tree. 
# It uses updateValueUtil() to update the value in segment tree 
def updateValue(arr,st, n, i, new_val,isPrime): 

    # Check for erroneous input index 
    if (i < 0 or i > n - 1): 
        printf("Invalid Input") 
        return

    diff, oldValue = 0, 0

    oldValue = arr[i] 

    # Update the value in array 
    arr[i] = new_val 

    # Case 1: Old and new values both are primes 
    if (isPrime[oldValue] and isPrime[new_val]): 
        return

    # Case 2: Old and new values both non primes 
    if ((not isPrime[oldValue]) and (not isPrime[new_val])): 
        return

    # Case 3: Old value was prime, new value is non prime 
    if (isPrime[oldValue] and not isPrime[new_val]): 
        diff = -1

    # Case 4: Old value was non prime, new_val is prime 
    if (not isPrime[oldValue] and isPrime[new_val]): 
        diff = 1

    # Update the values of nodes in segment tree 
    updateValueUtil(st, 0, n - 1, i, diff, 0) 

# Return number of primes in range from index qs (query start) to 
# qe (query end). It mainly uses queryPrimesUtil() 
def queryPrimes(st, n, qs, qe): 

    primesInRange = queryPrimesUtil(st, 0, n - 1, qs, qe, 0) 

    print("Number of Primes in subarray from ", qs," to ", qe," = ", primesInRange) 

# A recursive function that constructs Segment Tree 
# for array[ss..se]. 
# si is index of current node in segment tree st 
def constructSTUtil(arr, ss, se, st,si,isPrime): 

    # If there is one element in array, check if it 
    # is prime then store 1 in the segment tree else 
    # store 0 and return 
    if (ss == se): 

        # if arr[ss] is prime 
        if (isPrime[arr[ss]]): 
            st[si] = 1
        else: 
            st[si] = 0

        return st[si] 

    # If there are more than one elements, then recur 
    # for left and right subtrees and store the sum 
    # of the two values in this node 
    mid = getMid(ss, se) 
    st[si] = constructSTUtil(arr, ss, mid, st,si * 2 + 1, isPrime) + \ 
            constructSTUtil(arr, mid + 1, se, st,si * 2 + 2, isPrime) 
    return st[si] 

# /* Function to construct segment tree from given array. 
# This function allocates memory for segment tree and 
# calls constructSTUtil() to fill the allocated memory */ 
def constructST(arr, n, isPrime): 

    # Allocate memory for segment tree 

    # Height of segment tree 
    x = ceil(log(n, 2)) 

    # Maximum size of segment tree 
    max_size = 2 * pow(2, x) - 1

    st = [0]*(max_size) 

    # Fill the allocated memory st 
    constructSTUtil(arr, 0, n - 1, st, 0, isPrime) 

    # Return the constructed segment tree 
    return st 

# Driver code 
if __name__ == '__main__': 

    arr= [ 1, 2, 3, 5, 7, 9] 
    n = len(arr) 

    # /* Preprocess all primes till MAX. 
    # Create a boolean array "isPrime[0..MAX]". 
    # A value in prime[i] will finally be false 
    # if i is Not a prime, else true. */ 

    isPrime = [True]*(MAX + 1) 
    sieveOfEratosthenes(isPrime) 

    # Build segment tree from given array 
    st = constructST(arr, n, isPrime) 

    # Query 1: Query(start = 0, end = 4) 
    start = 0
    end = 4
    queryPrimes(st, n, start, end) 

    # Query 2: Update(i = 3, x = 6), i.e Update 
    # a[i] to x 
    i = 3
    x = 6
    updateValue(arr, st, n, i, x, isPrime) 

    # uncomment to see array after update 
    # for(i = 0 i < n i++) cout << arr[i] << " " 

    # Query 3: Query(start = 0, end = 4) 
    start = 0
    end = 4
    queryPrimes(st, n, start, end) 

# This code is contributed by mohit kumar 29 

```

**输出**：

```
Number of Primes in subarray from 0 to 4 = 4
Number of Primes in subarray from 0 to 4 = 3

```

每个查询和更新的时间复杂度为`O(logn)`，构建段树的时间复杂度为`O(n)`。

**注意**：这里，使用 Eratosthenes 的筛子是`O(MAX log(log(MAX)))`，其中`MAX`是`arr[i]`可以取的最大值。



* * *

* * *



