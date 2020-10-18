# 计算范围内的素数

> 原文： [https://www.geeksforgeeks.org/count-primes-ranges/](https://www.geeksforgeeks.org/count-primes-ranges/)

给定范围`[L, R]`，我们需要找到范围为`[L, R]`的素数总数，其中`0 <= L <= R < 10000`。 针对不同范围的大量查询。

**示例**：

```
Input : Query 1 : L = 1, R = 10
        Query 2 : L = 5, R = 10
Output : 4
         2
Explanation
Primes in the range L = 1 to R = 10 are 
{2, 3, 5, 7}. Therefore for query, answer 
is 4 {2, 3, 5, 7}.
For the second query, answer is 2 {5, 7}.

```



一个**简单解决方案**是为每个查询`[L, R]`执行以下操作。 从`L`遍历到`R`，[检查当前数字是否为素数](https://www.geeksforgeeks.org/prime-numbers/)。 如果是，则增加计数。 最后返回计数。

一种有效的**解决方案**是使用 [Eratosthenes 筛子](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)查找达到给定极限的所有素数。 然后，我们计算一个前缀数组来存储计数，直到每个值超出限制为止。 一旦有了前缀数组，就可以在`O(1)`时间内回答查询。 我们只需要返回`prefix[R] – prefix[L-1]`。

## C++ 

```cpp

// CPP program to answer queries for count of 
// primes in given range. 
#include <bits/stdc++.h> 
using namespace std; 

const int MAX = 10000; 

// prefix[i] is going to store count of primes 
// till i (including i). 
int prefix[MAX + 1]; 

void buildPrefix() 
{ 
    // Create a boolean array "prime[0..n]". A  
    // value in prime[i] will finally be false  
    // if i is Not a prime, else true. 
    bool prime[MAX + 1]; 
    memset(prime, true, sizeof(prime)); 

    for (int p = 2; p * p <= MAX; p++) { 

        // If prime[p] is not changed, then  
        // it is a prime 
        if (prime[p] == true) { 

            // Update all multiples of p 
            for (int i = p * 2; i <= MAX; i += p) 
                prime[i] = false; 
        } 
    } 

    // Build prefix array 
    prefix[0] = prefix[1] = 0; 
    for (int p = 2; p <= MAX; p++) { 
        prefix[p] = prefix[p - 1]; 
        if (prime[p]) 
            prefix[p]++; 
    } 
} 

// Returns count of primes in range from L to 
// R (both inclusive). 
int query(int L, int R) 
{ 
    return prefix[R] - prefix[L - 1]; 
} 

// Driver code 
int main() 
{ 
    buildPrefix(); 

    int L = 5, R = 10; 
    cout << query(L, R) << endl; 

    L = 1, R = 10; 
    cout << query(L, R) << endl; 

    return 0; 
} 

```