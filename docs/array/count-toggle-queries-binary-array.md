# 计数和切换二进制数组上的查询

> 原文： [https://www.geeksforgeeks.org/count-toggle-queries-binary-array/](https://www.geeksforgeeks.org/count-toggle-queries-binary-array/)

给定大小`n`，其中最初所有元素均为 0。任务是执行以下两种类型的多个查询。 查询可以按任何顺序出现。

1.  **`Toggle(start, end)`**：切换从`start`到`end`范围的值（从 0 到 1 或从 1 到 0）。

2.  **`Count(start, end)`**：计数从`start`到`end`的给定范围内的 1。

```
Input : n = 5       // we have n = 5 blocks
        toggle 1 2  // change 1 into 0 or 0 into 1
        Toggle 2 4
        Count  2 3  // count all 1's within the range
        Toggle 2 4
        Count  1 4  // count all 1's within the range
Output : Total number of 1's in range 2 to 3 is = 1
         Total number of 1's in range 1 to 4 is = 2

```



针对此问题的一种**简单解决方案**是遍历`Toggle`查询的完整范围，当您获得`Count`查询时，然后为给定范围计算所有 1。 但是这种方法的时间复杂度将是`O(q * n)`，其中`q =`查询总数。

针对此问题的有效解决方案是将[**段树**](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)与[**延迟传播**](https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree/)结合使用。 在这里，我们收集更新，直到获得`Count`查询。 当我们获得`Count`的查询时，我们会在数组中进行所有先前收集的`Toggle`更新，然后在给定范围内对数字 1 进行计数。

以下是上述方法的实现：

## C++ 

```cpp

// C++ program to implement toggle and count 
// queries on a binary array. 
#include<bits/stdc++.h> 
using namespace std; 
const int MAX = 100000; 

// segment tree to store count of 1's within range 
int tree[MAX] = {0}; 

// bool type tree to collect the updates for toggling 
// the values of 1 and 0 in given range 
bool lazy[MAX] = {false}; 

// function for collecting updates of toggling 
// node --> index of current node in segment tree 
// st --> starting index of current node 
// en --> ending index of current node 
// us --> starting index of range update query 
// ue --> ending index of range update query 
void toggle(int node, int st, int en, int us, int ue) 
{ 
    // If lazy value is non-zero for current node of segment 
    // tree, then there are some pending updates. So we need 
    // to make sure that the pending updates are done before 
    // making new updates. Because this value may be used by 
    // parent after recursive calls (See last line of this 
    // function) 
    if (lazy[node]) 
    { 
        // Make pending updates using value stored in lazy nodes 
        lazy[node] = false; 
        tree[node] = en - st + 1 - tree[node]; 

        // checking if it is not leaf node because if 
        // it is leaf node then we cannot go further 
        if (st < en) 
        { 
            // We can postpone updating children we don't 
            // need their new values now. 
            // Since we are not yet updating children of 'node', 
            // we need to set lazy flags for the children 
            lazy[node<<1] = !lazy[node<<1]; 
            lazy[1+(node<<1)] = !lazy[1+(node<<1)]; 
        } 
    } 

    // out of range 
    if (st>en || us > en || ue < st) 
        return ; 

    // Current segment is fully in range 
    if (us<=st && en<=ue) 
    { 
        // Add the difference to current node 
        tree[node] = en-st+1 - tree[node]; 

        // same logic for checking leaf node or not 
        if (st < en) 
        { 
            // This is where we store values in lazy nodes, 
            // rather than updating the segment tree itelf 
            // Since we don't need these updated values now 
            // we postpone updates by storing values in lazy[] 
            lazy[node<<1] = !lazy[node<<1]; 
            lazy[1+(node<<1)] = !lazy[1+(node<<1)]; 
        } 
        return; 
    } 

    // If not completely in rang, but overlaps, recur for 
    // children, 
    int mid = (st+en)/2; 
    toggle((node<<1), st, mid, us, ue); 
    toggle((node<<1)+1, mid+1,en, us, ue); 

    // And use the result of children calls to update this node 
    if (st < en) 
        tree[node] = tree[node<<1] + tree[(node<<1)+1]; 
} 

/* node --> Index of current node in the segment tree. 
          Initially 0 is passed as root is always at' 
          index 0 
   st & en  --> Starting and ending indexes of the 
                segment represented by current node, 
                i.e., tree[node] 
   qs & qe  --> Starting and ending indexes of query 
                range */
// function to count number of 1's within given range 
int countQuery(int node, int st, int en, int qs, int qe) 
{ 
    // current node is out of range 
    if (st>en || qs > en || qe < st) 
        return 0; 

    // If lazy flag is set for current node of segment tree, 
    // then there are some pending updates. So we need to 
    // make sure that the pending updates are done before 
    // processing the sub sum query 
    if (lazy[node]) 
    { 
        // Make pending updates to this node. Note that this 
        // node represents sum of elements in arr[st..en] and 
        // all these elements must be increased by lazy[node] 
        lazy[node] = false; 
        tree[node] = en-st+1-tree[node]; 

        // checking if it is not leaf node because if 
        // it is leaf node then we cannot go further 
        if (st<en) 
        { 
            // Since we are not yet updating children os si, 
            // we need to set lazy values for the children 
            lazy[node<<1] = !lazy[node<<1]; 
            lazy[(node<<1)+1] = !lazy[(node<<1)+1]; 
        } 
    } 

    // At this point we are sure that pending lazy updates 
    // are done for current node. So we can return value 
    // If this segment lies in range 
    if (qs<=st && en<=qe) 
        return tree[node]; 

    // If a part of this segment overlaps with the given range 
    int mid = (st+en)/2; 
    return countQuery((node<<1), st, mid, qs, qe) + 
           countQuery((node<<1)+1, mid+1, en, qs, qe); 
} 

// Driver program to run the case 
int main() 
{ 
    int n = 5; 
    toggle(1, 0, n-1, 1, 2);  //  Toggle 1 2 
    toggle(1, 0, n-1, 2, 4);  //  Toggle 2 4 

    cout << countQuery(1, 0, n-1, 2, 3) << endl;  //  Count 2 3 

    toggle(1, 0, n-1, 2, 4);  //  Toggle 2 4 

    cout << countQuery(1, 0, n-1, 1, 4) << endl;  //  Count 1 4 

   return 0; 
} 

```

## Java

```java

// Java program to implement toggle and  
// count queries on a binary array.  

class GFG 
{ 
static final int MAX = 100000; 

// segment tree to store count 
// of 1's within range  
static int tree[] = new int[MAX]; 

// bool type tree to collect the updates  
// for toggling the values of 1 and 0 in 
// given range  
static boolean lazy[] = new boolean[MAX]; 

// function for collecting updates of toggling  
// node --> index of current node in segment tree  
// st --> starting index of current node  
// en --> ending index of current node  
// us --> starting index of range update query  
// ue --> ending index of range update query  
static void toggle(int node, int st,  
                   int en, int us, int ue)  
{ 
    // If lazy value is non-zero for current  
    // node of segment tree, then there are  
    // some pending updates. So we need  
    // to make sure that the pending updates  
    // are done before making new updates. 
    // Because this value may be used by  
    // parent after recursive calls (See last  
    // line of this function)  
    if (lazy[node]) 
    { 

        // Make pending updates using value  
        // stored in lazy nodes  
        lazy[node] = false; 
        tree[node] = en - st + 1 - tree[node]; 

        // checking if it is not leaf node 
        // because if it is leaf node then 
        // we cannot go further  
        if (st < en) 
        { 
            // We can postpone updating children  
            // we don't need their new values now.  
            // Since we are not yet updating children 
            // of 'node', we need to set lazy flags  
            // for the children  
            lazy[node << 1] = !lazy[node << 1]; 
            lazy[1 + (node << 1)] = !lazy[1 + (node << 1)]; 
        } 
    } 

    // out of range  
    if (st > en || us > en || ue < st)  
    { 
        return; 
    } 

    // Current segment is fully in range  
    if (us <= st && en <= ue) 
    { 
        // Add the difference to current node  
        tree[node] = en - st + 1 - tree[node]; 

        // same logic for checking leaf node or not  
        if (st < en) 
        { 
            // This is where we store values in lazy nodes,  
            // rather than updating the segment tree itelf  
            // Since we don't need these updated values now  
            // we postpone updates by storing values in lazy[]  
            lazy[node << 1] = !lazy[node << 1]; 
            lazy[1 + (node << 1)] = !lazy[1 + (node << 1)]; 
        } 
        return; 
    } 

    // If not completely in rang,  
    // but overlaps, recur for children,  
    int mid = (st + en) / 2; 
    toggle((node << 1), st, mid, us, ue); 
    toggle((node << 1) + 1, mid + 1, en, us, ue); 

    // And use the result of children  
    // calls to update this node  
    if (st < en)  
    { 
        tree[node] = tree[node << 1] + 
                     tree[(node << 1) + 1]; 
    } 
} 

/* node --> Index of current node in the segment tree.  
    Initially 0 is passed as root is always at'  
    index 0  
st & en --> Starting and ending indexes of the  
            segment represented by current node,  
            i.e., tree[node]  
qs & qe --> Starting and ending indexes of query  
            range */
// function to count number of 1's  
// within given range  
static int countQuery(int node, int st,  
                      int en, int qs, int qe) 
{ 
    // current node is out of range  
    if (st > en || qs > en || qe < st) 
    { 
        return 0; 
    } 

    // If lazy flag is set for current  
    // node of segment tree, then there  
    // are some pending updates. So we  
    // need to make sure that the pending  
    // updates are done before processing  
    // the sub sum query  
    if (lazy[node]) 
    { 
        // Make pending updates to this node.  
        // Note that this node represents sum  
        // of elements in arr[st..en] and  
        // all these elements must be increased 
        // by lazy[node]  
        lazy[node] = false; 
        tree[node] = en - st + 1 - tree[node]; 

        // checking if it is not leaf node because if  
        // it is leaf node then we cannot go further  
        if (st < en)  
        { 
            // Since we are not yet updating children os si,  
            // we need to set lazy values for the children  
            lazy[node << 1] = !lazy[node << 1]; 
            lazy[(node << 1) + 1] = !lazy[(node << 1) + 1]; 
        } 
    } 

    // At this point we are sure that pending  
    // lazy updates are done for current node.  
    // So we can return value If this segment  
    // lies in range  
    if (qs <= st && en <= qe) 
    { 
        return tree[node]; 
    } 

    // If a part of this segment overlaps 
    // with the given range  
    int mid = (st + en) / 2; 
    return countQuery((node << 1), st, mid, qs, qe) +  
           countQuery((node << 1) + 1, mid + 1, en, qs, qe); 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    int n = 5; 
    toggle(1, 0, n - 1, 1, 2); // Toggle 1 2  
    toggle(1, 0, n - 1, 2, 4); // Toggle 2 4  

    System.out.println(countQuery(1, 0, n - 1, 2, 3)); // Count 2 3  

    toggle(1, 0, n - 1, 2, 4); // Toggle 2 4  

    System.out.println(countQuery(1, 0, n - 1, 1, 4)); // Count 1 4  
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python program to implement toggle and count 
# queries on a binary array. 
MAX = 100000

# segment tree to store count of 1's within range 
tree = [0] * MAX

# bool type tree to collect the updates for toggling 
# the values of 1 and 0 in given range 
lazy = [False] * MAX

# function for collecting updates of toggling 
# node --> index of current node in segment tree 
# st --> starting index of current node 
# en --> ending index of current node 
# us --> starting index of range update query 
# ue --> ending index of range update query 
def toggle(node: int, st: int, en: int, us: int, ue: int): 

    # If lazy value is non-zero for current node of segment 
    # tree, then there are some pending updates. So we need 
    # to make sure that the pending updates are done before 
    # making new updates. Because this value may be used by 
    # parent after recursive calls (See last line of this 
    # function) 
    if lazy[node]: 

        # Make pending updates using value stored in lazy nodes 
        lazy[node] = False
        tree[node] = en - st + 1 - tree[node] 

        # checking if it is not leaf node because if 
        # it is leaf node then we cannot go further 
        if st < en: 

            # We can postpone updating children we don't 
            # need their new values now. 
            # Since we are not yet updating children of 'node', 
            # we need to set lazy flags for the children 
            lazy[node << 1] = not lazy[node << 1] 
            lazy[1 + (node << 1)] = not lazy[1 + (node << 1)] 

    # out of range 
    if st > en or us > en or ue < st: 
        return

    # Current segment is fully in range 
    if us <= st and en <= ue: 

        # Add the difference to current node 
        tree[node] = en - st + 1 - tree[node] 

        # same logic for checking leaf node or not 
        if st < en: 

            # This is where we store values in lazy nodes, 
            # rather than updating the segment tree itelf 
            # Since we don't need these updated values now 
            # we postpone updates by storing values in lazy[] 
            lazy[node << 1] = not lazy[node << 1] 
            lazy[1 + (node << 1)] = not lazy[1 + (node << 1)] 
        return

    # If not completely in rang, but overlaps, recur for 
    # children, 
    mid = (st + en) // 2
    toggle((node << 1), st, mid, us, ue) 
    toggle((node << 1) + 1, mid + 1, en, us, ue) 

    # And use the result of children calls to update this node 
    if st < en: 
        tree[node] = tree[node << 1] + tree[(node << 1) + 1] 

# node --> Index of current node in the segment tree. 
#         Initially 0 is passed as root is always at' 
#         index 0 
# st & en --> Starting and ending indexes of the 
#             segment represented by current node, 
#             i.e., tree[node] 
# qs & qe --> Starting and ending indexes of query 
#             range 
# function to count number of 1's within given range 
def countQuery(node: int, st: int, en: int, qs: int, qe: int) -> int: 

    # current node is out of range 
    if st > en or qs > en or qe < st: 
        return 0

    # If lazy flag is set for current node of segment tree, 
    # then there are some pending updates. So we need to 
    # make sure that the pending updates are done before 
    # processing the sub sum query 
    if lazy[node]: 

        # Make pending updates to this node. Note that this 
        # node represents sum of elements in arr[st..en] and 
        # all these elements must be increased by lazy[node] 
        lazy[node] = False
        tree[node] = en - st + 1 - tree[node] 

        # checking if it is not leaf node because if 
        # it is leaf node then we cannot go further 
        if st < en: 

            # Since we are not yet updating children os si, 
            # we need to set lazy values for the children 
            lazy[node << 1] = not lazy[node << 1] 
            lazy[(node << 1) + 1] = not lazy[(node << 1) + 1] 

    # At this point we are sure that pending lazy updates 
    # are done for current node. So we can return value 
    # If this segment lies in range 
    if qs <= st and en <= qe: 
        return tree[node] 

    # If a part of this segment overlaps with the given range 
    mid = (st + en) // 2
    return countQuery((node << 1), st, mid, qs, qe) + countQuery( 
        (node << 1) + 1, mid + 1, en, qs, qe) 

# Driver Code 
if __name__ == "__main__": 

    n = 5
    toggle(1, 0, n - 1, 1, 2) # Toggle 1 2 
    toggle(1, 0, n - 1, 2, 4) # Toggle 2 4 

    print(countQuery(1, 0, n - 1, 2, 3)) # count 2 3 

    toggle(1, 0, n - 1, 2, 4) # Toggle 2 4 

    print(countQuery(1, 0, n - 1, 1, 4)) # count 1 4 

# This code is contributed by 
# sanjeev2552 

```

## C# 

```cs

// C# program to implement toggle and  
// count queries on a binary array. 
using System; 

public class GFG{ 

    static readonly int MAX = 100000;  

    // segment tree to store count  
    // of 1's within range  
    static int []tree = new int[MAX];  

    // bool type tree to collect the updates  
    // for toggling the values of 1 and 0 in  
    // given range  
    static bool []lazy = new bool[MAX];  

    // function for collecting updates of toggling  
    // node --> index of current node in segment tree  
    // st --> starting index of current node  
    // en --> ending index of current node  
    // us --> starting index of range update query  
    // ue --> ending index of range update query  
    static void toggle(int node, int st,  
                    int en, int us, int ue)  
    {  
        // If lazy value is non-zero for current  
        // node of segment tree, then there are  
        // some pending updates. So we need  
        // to make sure that the pending updates  
        // are done before making new updates.  
        // Because this value may be used by  
        // parent after recursive calls (See last  
        // line of this function)  
        if (lazy[node])  
        {  

            // Make pending updates using value  
            // stored in lazy nodes  
            lazy[node] = false;  
            tree[node] = en - st + 1 - tree[node];  

            // checking if it is not leaf node  
            // because if it is leaf node then  
            // we cannot go further  
            if (st < en)  
            {  
                // We can postpone updating children  
                // we don't need their new values now.  
                // Since we are not yet updating children  
                // of 'node', we need to set lazy flags  
                // for the children  
                lazy[node << 1] = !lazy[node << 1];  
                lazy[1 + (node << 1)] = !lazy[1 + (node << 1)];  
            }  
        }  

        // out of range  
        if (st > en || us > en || ue < st)  
        {  
            return;  
        }  

        // Current segment is fully in range  
        if (us <= st && en <= ue)  
        {  
            // Add the difference to current node  
            tree[node] = en - st + 1 - tree[node];  

            // same logic for checking leaf node or not  
            if (st < en)  
            {  
                // This is where we store values in lazy nodes,  
                // rather than updating the segment tree itelf  
                // Since we don't need these updated values now  
                // we postpone updates by storing values in lazy[]  
                lazy[node << 1] = !lazy[node << 1];  
                lazy[1 + (node << 1)] = !lazy[1 + (node << 1)];  
            }  
            return;  
        }  

        // If not completely in rang,  
        // but overlaps, recur for children,  
        int mid = (st + en) / 2;  
        toggle((node << 1), st, mid, us, ue);  
        toggle((node << 1) + 1, mid + 1, en, us, ue);  

        // And use the result of children  
        // calls to update this node  
        if (st < en)  
        {  
            tree[node] = tree[node << 1] +  
                        tree[(node << 1) + 1];  
        }  
    }  

    /* node --> Index of current node in the segment tree.  
        Initially 0 is passed as root is always at'  
        index 0  
    st & en --> Starting and ending indexes of the  
                segment represented by current node,  
                i.e., tree[node]  
    qs & qe --> Starting and ending indexes of query  
                range */
    // function to count number of 1's  
    // within given range  
    static int countQuery(int node, int st,  
                        int en, int qs, int qe)  
    {  
        // current node is out of range  
        if (st > en || qs > en || qe < st)  
        {  
            return 0;  
        }  

        // If lazy flag is set for current  
        // node of segment tree, then there  
        // are some pending updates. So we  
        // need to make sure that the pending  
        // updates are done before processing  
        // the sub sum query  
        if (lazy[node])  
        {  
            // Make pending updates to this node.  
            // Note that this node represents sum  
            // of elements in arr[st..en] and  
            // all these elements must be increased  
            // by lazy[node]  
            lazy[node] = false;  
            tree[node] = en - st + 1 - tree[node];  

            // checking if it is not leaf node because if  
            // it is leaf node then we cannot go further  
            if (st < en)  
            {  
                // Since we are not yet updating children os si,  
                // we need to set lazy values for the children  
                lazy[node << 1] = !lazy[node << 1];  
                lazy[(node << 1) + 1] = !lazy[(node << 1) + 1];  
            }  
        }  

        // At this point we are sure that pending  
        // lazy updates are done for current node.  
        // So we can return value If this segment  
        // lies in range  
        if (qs <= st && en <= qe)  
        {  
            return tree[node];  
        }  

        // If a part of this segment overlaps  
        // with the given range  
        int mid = (st + en) / 2;  
        return countQuery((node << 1), st, mid, qs, qe) +  
            countQuery((node << 1) + 1, mid + 1, en, qs, qe);  
    }  

    // Driver Code  
    public static void Main()  
    {  
        int n = 5;  
        toggle(1, 0, n - 1, 1, 2); // Toggle 1 2  
        toggle(1, 0, n - 1, 2, 4); // Toggle 2 4  

        Console.WriteLine(countQuery(1, 0, n - 1, 2, 3)); // Count 2 3  

        toggle(1, 0, n - 1, 2, 4); // Toggle 2 4  

        Console.WriteLine(countQuery(1, 0, n - 1, 1, 4)); // Count 1 4  
    }  
}  

/*This code is contributed by PrinciRaj1992*/

```

**输出**：

```
1
2

```



