# 求与 X 加权和异或最大的子树的根

> 原文:[https://www . geeksforgeeks . org/find-子树的根-其加权和-xor-with-x-是最大值/](https://www.geeksforgeeks.org/find-the-root-of-the-sub-tree-whose-weighted-sum-xor-with-x-is-maximum/)

给定一棵树，以及所有节点的权重，任务是找到与给定整数 **X** 加权和异或最大的子树的根。
**例:**

> **输入:**
> 
> ![](img/580b17fbe752fb3a04789f3c327eef8f.png)
> 
> X = 15
> **输出:** 4
> 父 1 的子树权重=(-1)+(5)+(-2)+(-1)+(3))XOR 15 = 4 XOR 15 = 11
> 父 2 的子树权重= ((5) + (-1) + (3)) XOR 15 = 7 XOR 15 = 8
> 父 3 的子树权重= -1 XOR 15 = -16
> 父 4 的子树权重= 3 XOR 15 = 12
> 父 5 的子树权重= -2 XOR 15 = -15
> 节点 4 给出最大子树加权和 XOR X.

**方法:**对树执行 [dfs](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，对于每个节点，计算以当前节点为根的子树加权和，然后找到一个节点的最大值(和异或 X)。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int ans = 0, maxi = INT_MIN;

vector<int> graph[100];
vector<int> weight(100);

// Function to perform dfs and update the tree
// such that every node's weight is the sum of
// the weights of all the nodes in the sub-tree
// of the current node including itself
void dfs(int node, int parent)
{
    for (int to : graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node);

        // Calculating the weighted
        // sum of the subtree
        weight[node] += weight[to];
    }
}

// Function to find the node
// having maximum sub-tree sum XOR x
void findMaxX(int n, int x)
{

    // For every node
    for (int i = 1; i <= n; i++) {

        // If current node's weight XOR x
        // is maximum so far
        if (maxi < (weight[i] ^ x)) {
            maxi = (weight[i] ^ x);
            ans = i;
        }
    }
}

// Driver code
int main()
{
    int x = 15;
    int n = 5;

    // Weights of the node
    weight[1] = -1;
    weight[2] = 5;
    weight[3] = -1;
    weight[4] = 3;
    weight[5] = -2;

    // Edges of the tree
    graph[1].push_back(2);
    graph[2].push_back(3);
    graph[2].push_back(4);
    graph[1].push_back(5);

    dfs(1, 1);
    findMaxX(n, x);

    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    static int ans = 0, maxi = Integer.MIN_VALUE;

    static Vector<Integer>[] graph = new Vector[100];
    static Integer[] weight = new Integer[100];

    // Function to perform dfs and update the tree
    // such that every node's weight is the sum of
    // the weights of all the nodes in the sub-tree
    // of the current node including itself
    static void dfs(int node, int parent)
    {
        for (int to : graph[node])
        {
            if (to == parent)
                continue;
            dfs(to, node);

            // Calculating the weighted
            // sum of the subtree
            weight[node] += weight[to];
        }
    }

    // Function to find the node
    // having maximum sub-tree sum XOR x
    static void findMaxX(int n, int x)
    {

        // For every node
        for (int i = 1; i <= n; i++)
        {

            // If current node's weight XOR x
            // is maximum so far
            if (maxi < (weight[i] ^ x))
            {
                maxi = (weight[i] ^ x);
                ans = i;
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 15;
        int n = 5;
        for (int i = 0; i < 100; i++)
            graph[i] = new Vector<Integer>();

        // Weights of the node
        weight[1] = -1;
        weight[2] = 5;
        weight[3] = -1;
        weight[4] = 3;
        weight[5] = -2;

        // Edges of the tree
        graph[1].add(2);
        graph[2].add(3);
        graph[2].add(4);
        graph[1].add(5);

        dfs(1, 1);
        findMaxX(n, x);

        System.out.print(ans);
    }
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python implementation of the approach
from sys import maxsize

# Function to perform dfs and update the tree
# such that every node's weight is the sum of
# the weights of all the nodes in the sub-tree
# of the current node including itself
def dfs(node, parent):
    global maxi, graph, weight, x, ans
    for to in graph[node]:
        if (to == parent):
            continue
        dfs(to, node)

        # Calculating the weighted
        # sum of the subtree
        weight[node] += weight[to]

# Function to find the node
# having maximum sub-tree sum XOR x
def findMaxX(n, x):
    global maxi, graph, weight, ans

    # For every node
    for i in range(1, n + 1):

        # If current node's weight XOR x
        # is maximum so far
        if (maxi < (weight[i] ^ x)):
            maxi = (weight[i] ^ x)
            ans = i

# Driver code
ans = 0
maxi = -maxsize

graph = [[] for i in range(100)]
weight = [0]*100
x = 15
n = 5

# Weights of the node
weight[1] = -1
weight[2] = 5
weight[3] = -1
weight[4] = 3
weight[5] = -2

# Edges of the tree
graph[1].append(2)
graph[2].append(3)
graph[2].append(4)
graph[1].append(5)

dfs(1, 1)
findMaxX(n, x)

print(ans)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```

// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    static int ans = 0, maxi = int.MinValue;

    static List<int>[] graph = new List<int>[100];
    static int[] weight = new int[100];

    // Function to perform dfs and update the tree
    // such that every node's weight is the sum of
    // the weights of all the nodes in the sub-tree
    // of the current node including itself
    static void dfs(int node, int parent)
    {
        foreach (int to in graph[node])
        {
            if (to == parent)
                continue;
            dfs(to, node);

            // Calculating the weighted
            // sum of the subtree
            weight[node] += weight[to];
        }
    }

    // Function to find the node
    // having maximum sub-tree sum XOR x
    static void findMaxX(int n, int x)
    {

        // For every node
        for (int i = 1; i <= n; i++)
        {

            // If current node's weight XOR x
            // is maximum so far
            if (maxi < (weight[i] ^ x))
            {
                maxi = (weight[i] ^ x);
                ans = i;
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int x = 15;
        int n = 5;
        for (int i = 0; i < 100; i++)
            graph[i] = new List<int>();

        // Weights of the node
        weight[1] = -1;
        weight[2] = 5;
        weight[3] = -1;
        weight[4] = 3;
        weight[5] = -2;

        // Edges of the tree
        graph[1].Add(2);
        graph[2].Add(3);
        graph[2].Add(4);
        graph[1].Add(5);

        dfs(1, 1);
        findMaxX(n, x);

        Console.Write(ans);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
    let maxi = Number.MIN_VALUE, x, ans;
    let graph = new Array(100);
    let weight = new Array(100);
    for(let i = 0; i < 100; i++)
    {
        graph[i] = [];
        weight[i] = 0;
    }

    // Function to perform dfs and update the tree
    // such that every node's weight is the sum of
    // the weights of all the nodes in the sub-tree
    // of the current node including itself
    function  dfs(node, parent)
    {
        for(let to in graph[node])
        {
            if (to == parent)
                continue;
            dfs(to, node);

            // Calculating the weighted
            // sum of the subtree
            weight[node] += weight[to];
        }
    }

    // Function to find the node
    // having maximum sub-tree sum XOR x
    function findMaxX(n, x)
    {

        // For every node
        for (let i = 1; i <= n; i++)
        {

            // If current node's weight XOR x
            // is maximum so far
            if (maxi < (weight[i] ^ x))
            {
                maxi = (weight[i] ^ x);
                ans = i;
            }
        }
    }

    // Driver Code
    x = 15;
    let n = 5;

   // Weights of the node
    weight[1] = -1;
    weight[2] = 5;
    weight[3] = -1;
    weight[4] = 3;
    weight[5] = -2;

    // Edges of the tree
    graph[1].push(2);
    graph[2].push(3);
    graph[2].push(4);
    graph[1].push(5);

    dfs(1, 1);
    findMaxX(n, x);
    document.write(ans);

    // This code is contributed by unknown2108
</script>
```

**Output:** 

```
4
```

**<u>复杂度分析:</u>**

*   **时间复杂度:** O(N)。
    在 dfs 中，树的每个节点都被处理一次，因此如果树中总共有 N 个节点，由于 dfs 而导致的复杂性是 O(N)。因此，时间复杂度为 O(N)。
*   **辅助空间:** O(n)。
    递归栈。