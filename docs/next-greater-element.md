# 下一个更大的元素

> 原文： [https://www.geeksforgeeks.org/next-greater-element/](https://www.geeksforgeeks.org/next-greater-element/)

给定一个数组，为每个元素打印下一更大元素（NGE）。 元素`x`的下一个更大元素是数组`x`中右侧第一个更大的元素。 对于不存在更大元素的元素，请将下一个更大元素视为 -1。

**示例**：

1.  对于任何数组，最右边的元素始终将下一个更大的元素设为 -1。

2.  对于以降序排列的数组，所有元素的下一个更大元素为 -1。

3.  对于输入数组`[4, 5, 2, 25]`，每个元素的下一个更大元素如下。

```
Element       NGE
   4      -->   5
   5      -->   25
   2      -->   25
   25     -->   -1

```

4.  对于输入数组`[13, 7, 6, 12]`，每个元素的下一个更大元素如下。

```
  Element        NGE
   13      -->    -1
   7       -->     12
   6       -->     12
   12      -->     -1

```



**方法 1（简单）**：

使用两个循环：外循环一个接一个地选取所有元素。 内循环为外循环选取的元素寻找第一个更大的元素。 如果找到更大的元素，则该元素将作为下一个被打印，否则将打印 -1。

## C++ 

```cpp

// Simple C++ program to print 
// next greater elements in a 
// given array 
#include<iostream> 
using namespace std; 

/* prints element and NGE pair  
for all elements of arr[] of size n */
void printNGE(int arr[], int n) 
{ 
    int next, i, j; 
    for (i = 0; i < n; i++) 
    { 
        next = -1; 
        for (j = i + 1; j < n; j++) 
        { 
            if (arr[i] < arr[j]) 
            { 
                next = arr[j]; 
                break; 
            } 
        } 
        cout << arr[i] << " -- " 
             << next << endl; 
    } 
} 

// Driver Code 
int main() 
{ 
    int arr[] = {11, 13, 21, 3}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    printNGE(arr, n); 
    return 0; 
} 

// This code is contributed  
// by Akanksha Rai(Abby_akku) 

```

## C

```c

// Simple C program to print next greater elements 
// in a given array 
#include<stdio.h> 

/* prints element and NGE pair for all elements of 
arr[] of size n */
void printNGE(int arr[], int n) 
{ 
    int next, i, j; 
    for (i=0; i<n; i++) 
    { 
        next = -1; 
        for (j = i+1; j<n; j++) 
        { 
            if (arr[i] < arr[j]) 
            { 
                next = arr[j]; 
                break; 
            } 
        } 
        printf("%d -- %dn", arr[i], next); 
    } 
} 

int main() 
{ 
    int arr[]= {11, 13, 21, 3}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    printNGE(arr, n); 
    return 0; 
} 

```

## Java

```java

// Simple Java program to print next  
// greater elements in a given array 

class Main 
{  
    /* prints element and NGE pair for  
     all elements of arr[] of size n */
    static void printNGE(int arr[], int n) 
    { 
        int next, i, j; 
        for (i=0; i<n; i++) 
        { 
            next = -1; 
            for (j = i+1; j<n; j++) 
            { 
                if (arr[i] < arr[j]) 
                { 
                    next = arr[j]; 
                    break; 
                } 
            } 
            System.out.println(arr[i]+" -- "+next); 
        } 
    } 

    public static void main(String args[]) 
    { 
        int arr[]= {11, 13, 21, 3}; 
        int n = arr.length; 
        printNGE(arr, n); 
    } 
} 

```

## Python

```py

# Function to print element and NGE pair for all elements of list 
def printNGE(arr): 

    for i in range(0, len(arr), 1): 

        next = -1
        for j in range(i+1, len(arr), 1): 
            if arr[i] < arr[j]: 
                next = arr[j] 
                break

        print(str(arr[i]) + " -- " + str(next)) 

# Driver program to test above function 
arr = [11,13,21,3] 
printNGE(arr) 

# This code is contributed by Sunny Karira 

```

## C# 

```cs

// Simple C# program to print next  
// greater elements in a given array 
using System; 

class GFG 
{ 

    /* prints element and NGE pair for  
    all elements of arr[] of size n */
    static void printNGE(int []arr, int n) 
    { 
        int next, i, j; 
        for (i = 0; i < n; i++) 
        { 
            next = -1; 
            for (j = i + 1; j < n; j++) 
            { 
                if (arr[i] < arr[j]) 
                { 
                    next = arr[j]; 
                    break; 
                } 
            } 
            Console.WriteLine(arr[i] + " -- " + next); 
        } 
    } 

    // driver code 
    public static void Main() 
    { 
        int []arr= {11, 13, 21, 3}; 
        int n = arr.Length; 

        printNGE(arr, n); 
    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php 
// Simple PHP program to print next 
// greater elements in a given array 

/* prints element and NGE pair for  
   all elements of arr[] of size n */
function printNGE($arr, $n) 
{ 
    for ($i = 0; $i < $n; $i++) 
    { 
        $next = -1; 
        for ($j = $i + 1; $j < $n; $j++) 
        { 
            if ($arr[$i] < $arr[$j]) 
            { 
                $next = $arr[$j]; 
                break; 
            } 
        } 
        echo $arr[$i]." -- ". $next."\n"; 

    } 
} 

    // Driver Code 
    $arr= array(11, 13, 21, 3); 
    $n = count($arr); 
    printNGE($arr, $n); 

// This code is contributed by Sam007 
?> 

```

**输出**：

```
11 -- 13
13 -- 21
21 -- -1
3 -- -1
```

**时间复杂度**：`O(n ^ 2)`。 当所有元素以降序排序时，会发生最坏的情况。

**方法 2（使用栈）**：

*   将第一个元素推入栈。

*   一个接一个地选取其余元素，然后循环执行以下步骤。

    1.  标记当前元素为`next`。

    2.  如果栈不为空，则将栈的顶部元素与`next`比较。

    3.  如果`next`大于顶部元素，则从栈中弹出元素。 `next`是弹出元素的下一个更大元素。

    4.  当弹出的元素小于`next`时，继续从栈中弹出。 `next`成为所有此类弹出元素的下一个更大元素。

*   最后，将`next`推入栈。

*   步骤 2 中的循环结束后，从栈中弹出所有元素，并将 -1 打印为它们的下一个元素。

下图是上述方法的模拟：

![](img/27b81ef281dfd24d9634420c545261aa.png)

下面是上述方法的实现：

## C++

```cpp

// A Stack based C++ program to find next 
// greater element for all array elements. 
#include <bits/stdc++.h> 
using namespace std; 

/* prints element and NGE pair for all 
elements of arr[] of size n */
void printNGE(int arr[], int n) { 
  stack < int > s; 

  /* push the first element to stack */
  s.push(arr[0]); 

  // iterate for rest of the elements 
  for (int i = 1; i < n; i++) { 

    if (s.empty()) { 
      s.push(arr[i]); 
      continue; 
    } 

    /* if stack is not empty, then 
       pop an element from stack. 
       If the popped element is smaller 
       than next, then 
    a) print the pair 
    b) keep popping while elements are 
    smaller and stack is not empty */
    while (s.empty() == false && s.top() < arr[i]) 
    {          
        cout << s.top() << " --> " << arr[i] << endl; 
        s.pop(); 
    } 

    /* push next to stack so that we can find 
    next greater for it */
    s.push(arr[i]); 
  } 

  /* After iterating over the loop, the remaining 
  elements in stack do not have the next greater 
  element, so print -1 for them */
  while (s.empty() == false) { 
    cout << s.top() << " --> " << -1 << endl; 
    s.pop(); 
  } 
} 

/* Driver program to test above functions */
int main() { 
  int arr[] = {11, 13, 21, 3}; 
  int n = sizeof(arr) / sizeof(arr[0]); 
  printNGE(arr, n); 
  return 0; 
}

```

## C

```c

// A Stack based C program to find next greater element 
// for all array elements. 
#include<stdio.h> 
#include<stdlib.h> 
#include<stdbool.h> 
#define STACKSIZE 100 

// stack structure 
struct stack 
{ 
    int top; 
    int items[STACKSIZE]; 
}; 

// Stack Functions to be used by printNGE() 
void push(struct stack *ps, int x) 
{ 
    if (ps->top == STACKSIZE-1) 
    { 
        printf("Error: stack overflown"); 
        getchar(); 
        exit(0); 
    } 
    else
    { 
        ps->top += 1; 
        int top = ps->top; 
        ps->items [top] = x; 
    } 
} 

bool isEmpty(struct stack *ps) 
{ 
    return (ps->top == -1)? true : false; 
} 

int pop(struct stack *ps) 
{ 
    int temp; 
    if (ps->top == -1) 
    { 
        printf("Error: stack underflow n"); 
        getchar(); 
        exit(0); 
    } 
    else
    { 
        int top = ps->top; 
        temp = ps->items [top]; 
        ps->top -= 1; 
        return temp; 
    } 
} 

/* prints element and NGE pair for all elements of 
arr[] of size n */
void printNGE(int arr[], int n) 
{ 
    int i = 0; 
    struct stack s; 
    s.top = -1; 
    int element, next; 

    /* push the first element to stack */
    push(&s, arr[0]); 

    // iterate for rest of the elements 
    for (i=1; i<n; i++) 
    { 
        next = arr[i]; 

        if (isEmpty(&s) == false) 
        { 
            // if stack is not empty, then pop an element from stack 
            element = pop(&s); 

            /* If the popped element is smaller than next, then 
                a) print the pair 
                b) keep popping while elements are smaller and 
                stack is not empty */
            while (element < next) 
            { 
                printf("n %d --> %d", element, next); 
                if(isEmpty(&s) == true) 
                   break; 
                element = pop(&s); 
            } 

            /* If element is greater than next, then push 
               the element back */
            if (element > next) 
                push(&s, element); 
        } 

        /* push next to stack so that we can find 
           next greater for it */
        push(&s, next); 
    } 

    /* After iterating over the loop, the remaining 
       elements in stack do not have the next greater 
       element, so print -1 for them */
    while (isEmpty(&s) == false) 
    { 
        element = pop(&s); 
        next = -1; 
        printf("n %d --> %d", element, next); 
    } 
} 

/* Driver program to test above functions */
int main() 
{ 
    int arr[]= {11, 13, 21, 3}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    printNGE(arr, n); 
    getchar(); 
    return 0; 
} 

```

## Java

```java

//Java program to print next 
//greater element using stack 

public class NGE  
{ 
    static class stack  
    { 
        int top; 
        int items[] = new int[100]; 

        // Stack functions to be used by printNGE 
        void push(int x)  
        { 
            if (top == 99)  
            { 
                System.out.println("Stack full"); 
            }  
            else 
            { 
                items[++top] = x; 
            } 
        } 

        int pop()  
        { 
            if (top == -1)  
            { 
                System.out.println("Underflow error"); 
                return -1; 
            }  
            else 
            { 
                int element = items[top]; 
                top--; 
                return element; 
            } 
        } 

        boolean isEmpty()  
        { 
            return (top == -1) ? true : false; 
        } 
    } 

    /* prints element and NGE pair for  
       all elements of arr[] of size n */
    static void printNGE(int arr[], int n)  
    { 
        int i = 0; 
        stack s = new stack(); 
        s.top = -1; 
        int element, next; 

        /* push the first element to stack */
        s.push(arr[0]); 

        // iterate for rest of the elements 
        for (i = 1; i < n; i++)  
        { 
            next = arr[i]; 

            if (s.isEmpty() == false)  
            { 

                // if stack is not empty, then  
                // pop an element from stack 
                element = s.pop(); 

                /* If the popped element is smaller than  
                   next, then a) print the pair b) keep  
                   popping while elements are smaller and  
                   stack is not empty */
                while (element < next)  
                { 
                    System.out.println(element + " --> " + next); 
                    if (s.isEmpty() == true) 
                        break; 
                    element = s.pop(); 
                } 

                /* If element is greater than next, then  
                   push the element back */
                if (element > next) 
                    s.push(element); 
            } 

            /* push next to stack so that we can find next 
               greater for it */
            s.push(next); 
        } 

        /* After iterating over the loop, the remaining  
           elements in stack do not have the next greater  
           element, so print -1 for them */
        while (s.isEmpty() == false)  
        { 
            element = s.pop(); 
            next = -1; 
            System.out.println(element + " -- " + next); 
        } 
    } 

    public static void main(String[] args)  
    { 
        int arr[] = { 11, 13, 21, 3 }; 
        int n = arr.length; 
        printNGE(arr, n); 
    } 
} 

// Thanks to Rishabh Mahrsee for contributing this code  

```

## Python

```py

# Python program to print next greater element using stack 

# Stack Functions to be used by printNGE() 
def createStack(): 
    stack = [] 
    return stack 

def isEmpty(stack): 
    return len(stack) == 0

def push(stack, x): 
    stack.append(x) 

def pop(stack): 
    if isEmpty(stack): 
        print("Error : stack underflow") 
    else: 
        return stack.pop() 

'''prints element and NGE pair for all elements of 
   arr[] '''
def printNGE(arr): 
    s = createStack() 
    element = 0
    next = 0

    # push the first element to stack 
    push(s, arr[0]) 

    # iterate for rest of the elements 
    for i in range(1, len(arr), 1): 
        next = arr[i] 

        if isEmpty(s) == False: 

            # if stack is not empty, then pop an element from stack 
            element = pop(s) 

            '''If the popped element is smaller than next, then 
                a) print the pair 
                b) keep popping while elements are smaller and 
                   stack is not empty '''
            while element < next : 
                print(str(element)+ " -- " + str(next)) 
                if isEmpty(s) == True : 
                    break
                element = pop(s) 

            '''If element is greater than next, then push 
               the element back '''
            if  element > next: 
                push(s, element) 

        '''push next to stack so that we can find 
           next greater for it '''
        push(s, next) 

    '''After iterating over the loop, the remaining 
       elements in stack do not have the next greater 
       element, so print -1 for them '''

    while isEmpty(s) == False: 
            element = pop(s) 
            next = -1
            print(str(element) + " -- " + str(next)) 

# Driver program to test above functions 
arr = [11, 13, 21, 3] 
printNGE(arr) 

# This code is contributed by Sunny Karira 

```

## C#

```cs

using System; 

// c# program to print next  
//greater element using stack  

public class NGE 
{ 
    public class stack 
    { 
        public int top; 
        public int[] items = new int[100]; 

        // Stack functions to be used by printNGE  
        public virtual void push(int x) 
        { 
            if (top == 99) 
            { 
                Console.WriteLine("Stack full"); 
            } 
            else
            { 
                items[++top] = x; 
            } 
        } 

        public virtual int pop() 
        { 
            if (top == -1) 
            { 
                Console.WriteLine("Underflow error"); 
                return -1; 
            } 
            else
            { 
                int element = items[top]; 
                top--; 
                return element; 
            } 
        } 

        public virtual bool Empty 
        { 
            get
            { 
                return (top == -1) ? true : false; 
            } 
        } 
    } 

    /* prints element and NGE pair for   
       all elements of arr[] of size n */
    public static void printNGE(int[] arr, int n) 
    { 
        int i = 0; 
        stack s = new stack(); 
        s.top = -1; 
        int element, next; 

        /* push the first element to stack */
        s.push(arr[0]); 

        // iterate for rest of the elements  
        for (i = 1; i < n; i++) 
        { 
            next = arr[i]; 

            if (s.Empty == false) 
            { 

                // if stack is not empty, then   
                // pop an element from stack  
                element = s.pop(); 

                /* If the popped element is smaller than   
                   next, then a) print the pair b) keep   
                   popping while elements are smaller and   
                   stack is not empty */
                while (element < next) 
                { 
                    Console.WriteLine(element + " --> " + next); 
                    if (s.Empty == true) 
                    { 
                        break; 
                    } 
                    element = s.pop(); 
                } 

                /* If element is greater than next, then   
                   push the element back */
                if (element > next) 
                { 
                    s.push(element); 
                } 
            } 

            /* push next to stack so that we can find next  
               greater for it */
            s.push(next); 
        } 

        /* After iterating over the loop, the remaining   
           elements in stack do not have the next greater   
           element, so print -1 for them */
        while (s.Empty == false) 
        { 
            element = s.pop(); 
            next = -1; 
            Console.WriteLine(element + " -- " + next); 
        } 
    } 

    public static void Main(string[] args) 
    { 
        int[] arr = new int[] {11, 13, 21, 3}; 
        int n = arr.Length; 
        printNGE(arr, n); 
    } 
} 

// This code is contributed by Shrikant13 

```

**输出**：

```
 11 -- 13
 13 -- 21
 3 -- -1
 21 -- -1

```

**时间复杂度**：`O(n)`。

当所有元素以降序排序时，会发生最坏的情况。 如果元素按降序排序，则每个元素最多处理 4 次。

1.  最初被推入栈。

2.  处理下一个元素时从栈中弹出。

3.  由于下一个元素较小，因此被推回栈。

4.  在算法的第 3 步中从栈中弹出。

请参见[优化解决方案](https://www.geeksforgeeks.org/next-greater-element-in-same-order-as-input/)，以相同顺序进行打印。

如果您发现上述代码/算法有误，请写评论，或者找到其他解决相同问题的方法。

