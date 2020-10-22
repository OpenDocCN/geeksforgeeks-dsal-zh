# 合并重叠间隔

> 原文： [https://www.geeksforgeeks.org/merging-intervals/](https://www.geeksforgeeks.org/merging-intervals/)

给定一组任意时间间隔的时间，将所有重叠的时间间隔合并为一个，并输出仅具有互斥时间间隔的结果。 为了简单起见，将间隔表示为整数对。

例如，让给定的间隔集为`{{1,3}, {2,4}, {5,7}, {6,8}}`。 间隔`{1,3}`和`{2,4}`彼此重叠，因此应将它们合并并成为`{1, 4}`。 同样，`{5, 7}`和`{6, 8}`应该合并并成为`{5, 8}`。



编写一个函数，该函数为给定间隔集生成合并间隔集。

**简单方法**是从第一个间隔开始并将其与所有其他间隔进行比较以进行重叠，如果它与任何其他间隔重叠，则从列表中删除另一个间隔并将另一个合并到第一个间隔中。 首先，对剩余间隔重复相同的步骤。 这种方法无法在比`O(n ^ 2)`更好的时间内实现。

**有效方法**是首先根据开始时间对时间间隔进行排序。 获得排序间隔后，就可以将所有间隔进行线性遍历。 这个想法是，在间隔的排序数组中，如果`interval[i]`不与`interval[i-1]`重叠，则`interval[i + 1]`就不能与`interval[i-1]`重叠，因为`interval[i+1]`的开始时间必须大于或等于`interval[i]`。 以下是详细的逐步算法。

```
1. Sort the intervals based on increasing order of 
    starting time.
2\. Push the first interval on to a stack.
3\. For each interval do the following
   a. If the current interval does not overlap with the stack 
       top, push it.
   b. If the current interval overlaps with stack top and ending
       time of current interval is more than that of stack top, 
       update stack top with the ending  time of current interval.
4. At the end stack contains the merged intervals. 
```

以下是上述方法的实现。

## C++ 

```cpp

// A C++ program for merging overlapping intervals 
#include<bits/stdc++.h> 
using namespace std; 

// An interval has start time and end time 
struct Interval 
{ 
    int start, end; 
}; 

// Compares two intervals according to their staring time. 
// This is needed for sorting the intervals using library 
// function std::sort(). See http://goo.gl/iGspV 
bool compareInterval(Interval i1, Interval i2) 
{ 
    return (i1.start < i2.start); 
} 

// The main function that takes a set of intervals, merges 
// overlapping intervals and prints the result 
void mergeIntervals(Interval arr[], int n) 
{ 
    // Test if the given set has at least one interval 
    if (n <= 0) 
        return; 

    // Create an empty stack of intervals 
    stack<Interval> s; 

    // sort the intervals in increasing order of start time 
    sort(arr, arr+n, compareInterval); 

    // push the first interval to stack 
    s.push(arr[0]); 

    // Start from the next interval and merge if necessary 
    for (int i = 1 ; i < n; i++) 
    { 
        // get interval from stack top 
        Interval top = s.top(); 

        // if current interval is not overlapping with stack top, 
        // push it to the stack 
        if (top.end < arr[i].start) 
            s.push(arr[i]); 

        // Otherwise update the ending time of top if ending of current 
        // interval is more 
        else if (top.end < arr[i].end) 
        { 
            top.end = arr[i].end; 
            s.pop(); 
            s.push(top); 
        } 
    } 

    // Print contents of stack 
    cout << "\n The Merged Intervals are: "; 
    while (!s.empty()) 
    { 
        Interval t = s.top(); 
        cout << "[" << t.start << "," << t.end << "] "; 
        s.pop(); 
    } 
    return; 
} 

// Driver program 
int main() 
{ 
    Interval arr[] =  { {6,8}, {1,9}, {2,4}, {4,7} }; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    mergeIntervals(arr, n); 
    return 0; 
} 

```

## Java

```java

// A Java program for merging overlapping intervals 
import java.util.Arrays; 
import java.util.Comparator; 
import java.util.Stack; 
public class MergeOverlappingIntervals { 

    // The main function that takes a set of intervals, merges  
    // overlapping intervals and prints the result  
    public static void mergeIntervals(Interval arr[])  
    {  
        // Test if the given set has at least one interval  
        if (arr.length <= 0)  
            return;  

        // Create an empty stack of intervals  
        Stack<Interval> stack=new Stack<>(); 

        // sort the intervals in increasing order of start time  
        Arrays.sort(arr,new Comparator<Interval>(){ 
            public int compare(Interval i1,Interval i2) 
            { 
                return i1.start-i2.start; 
            } 
        }); 

        // push the first interval to stack  
        stack.push(arr[0]);  

        // Start from the next interval and merge if necessary  
        for (int i = 1 ; i < arr.length; i++)  
        {  
            // get interval from stack top  
            Interval top = stack.peek();  

            // if current interval is not overlapping with stack top,  
            // push it to the stack  
            if (top.end < arr[i].start)  
                stack.push(arr[i]);  

            // Otherwise update the ending time of top if ending of current  
            // interval is more  
            else if (top.end < arr[i].end)  
            {  
                top.end = arr[i].end;  
                stack.pop();  
                stack.push(top);  
            }  
        }  

        // Print contents of stack  
        System.out.print("The Merged Intervals are: "); 
        while (!stack.isEmpty())  
        {  
            Interval t = stack.pop();  
            System.out.print("["+t.start+","+t.end+"] "); 
        }   
    }   

    public static void main(String args[]) { 
        Interval arr[]=new Interval[4]; 
        arr[0]=new Interval(6,8); 
        arr[1]=new Interval(1,9); 
        arr[2]=new Interval(2,4); 
        arr[3]=new Interval(4,7); 
        mergeIntervals(arr); 
    } 
} 

class Interval 
{ 
    int start,end; 
    Interval(int start, int end) 
    { 
        this.start=start; 
        this.end=end; 
    } 
} 
// This code is contributed by Gaurav Tiwari  

```

Output:

```
 The Merged Intervals are: [1,9] 
```

该方法的时间复杂度是`O(nLogn)`，用于排序。 对间隔数组进行排序后，合并将花费线性时间。

**`O(N log N)`和`O(1)`额外空间解决方案**：

上述解决方案需要`O(n)`额外的栈空间。 通过原地进行合并操作，我们可以避免使用额外的空间。 以下是详细步骤。

```
1) Sort all intervals in decreasing order of start time.
2) Traverse sorted intervals starting from first interval, 
   do following for every interval.
      a) If current interval is not first interval and it 
         overlaps with previous interval, then merge it with
         previous interval. Keep doing it while the interval
         overlaps with the previous one.         
      b) Else add current interval to output list of intervals.
```

请注意，如果按开始时间的降序对时间间隔进行排序，则可以通过比较前一个时间间隔的开始时间与当前时间间隔的结束时间来快速检查时间间隔是否重叠。

下面是上述算法的实现。

## C++

```cpp

// C++ program to merge overlapping Intervals in  
// O(n Log n) time and O(1) extra space.  
#include<bits/stdc++.h>  
using namespace std;  

// An Interval  
struct Interval  
{  
    int s, e;  
};  

// Function used in sort  
bool mycomp(Interval a, Interval b)  
{ return a.s < b.s; }  

void mergeIntervals(Interval arr[], int n)  
{  
    // Sort Intervals in increasing order of 
    // start time 
    sort(arr, arr+n, mycomp);  

    int index = 0; // Stores index of last element  
    // in output array (modified arr[])  

    // Traverse all input Intervals  
    for (int i=1; i<n; i++)  
    {  
        // If this is not first Interval and overlaps  
        // with the previous one  
        if (arr[index].e >=  arr[i].s)  
        {  
               // Merge previous and current Intervals  
            arr[index].e = max(arr[index].e, arr[i].e);  
            arr[index].s = min(arr[index].s, arr[i].s);  
        }  
        else { 
            arr[index] = arr[i];  
            index++; 
        }     
    }  

    // Now arr[0..index-1] stores the merged Intervals  
    cout << "\n The Merged Intervals are: ";  
    for (int i = 0; i <= index; i++)  
        cout << "[" << arr[i].s << ", " << arr[i].e << "] ";  
}  

// Driver program  
int main()  
{  
    Interval arr[] = { {6,8}, {1,9}, {2,4}, {4,7} };  
    int n = sizeof(arr)/sizeof(arr[0]);  
    mergeIntervals(arr, n);  
    return 0;  
}  

```

## Java

```java
// Java program to merge overlapping Intervals in
// O(n Log n) time and O(1) extra space
 
import java.util.Arrays;
import java.util.Comparator;
 
// An Interval
class Interval
{
    int start,end;
     
    Interval(int start, int end)
    {
        this.start=start;
        this.end=end;
    }
}
 
public class MergeOverlappingIntervals {
     
    // Function that takes a set of intervals, merges 
    // overlapping intervals and prints the result 
    public static void mergeIntervals(Interval arr[]) 
    { 
        // Sort Intervals in decreasing order of 
        // start time 
        Arrays.sort(arr,new Comparator<Interval>(){
            public int compare(Interval i1,Interval i2)
            {
                return i2.start - i1.start;
            }
        });
   
        int index = 0; // Stores index of last element 
        // in output array (modified arr[]) 
   
        // Traverse all input Intervals 
        for (int i=1; i<arr.length; i++) 
        { 
            // If this is not first Interval and overlaps 
            // with the previous one 
            if (arr[index].end >=  arr[i].start) 
            { 
                   // Merge previous and current Intervals 
                arr[index].end = Math.max(arr[index].end, arr[i].end); 
                arr[index].start = Math.min(arr[index].start, arr[i].start); 
            } 
            else {
                index++;
                arr[index] = arr[i]; 
            }    
        }
         
        // Now arr[0..index-1] stores the merged Intervals 
        System.out.print("The Merged Intervals are: ");
        for (int i = 0; i <= index; i++) 
        {
            System.out.print("[" + arr[i].start + ","
                                        + arr[i].end + "]"); 
        }
    } 
 
    // Driver Code
    public static void main(String args[]) {
        Interval arr[]=new Interval[4];
        arr[0]=new Interval(6,8);
        arr[1]=new Interval(1,9);
        arr[2]=new Interval(2,4);
        arr[3]=new Interval(4,7);
        mergeIntervals(arr);
    }
}
 
// This code is contributed by Gaurav Tiwari
```

## Python3

```py
# Python3 program to merge overlapping Intervals 
# in O(n Log n) time and O(1) extra space
def mergeIntervals(arr):
         
        # Sorting based on the increasing order 
        # of the start intervals
        arr.sort(key = lambda x: x[0]) 
         
        # array to hold the merged intervals
        m = []
        s = -10000
        max = -100000
        for i in range(len(arr)):
            a = arr[i]
            if a[0] > max:
                if i != 0:
                    m.append([s,max])
                max = a[1]
                s = a[0]
            else:
                if a[1] >= max:
                    max = a[1]
         
        #'max' value gives the last point of 
        # that particular interval
        # 's' gives the starting point of that interval
        # 'm' array contains the list of all merged intervals
 
        if max != -100000 and [s, max] not in m:
            m.append([s, max])
        print("The Merged Intervals are :", end = " ")
        for i in range(len(m)):
            print(m[i], end = " ")
 
# Driver code
arr = [[6, 8], [1, 9], [2, 4], [4, 7]]
mergeIntervals(arr)
 
# This code is contributed 
# by thirumalai srinivasan
```

输出：

```
 The Merged Intervals are: [1,9] 
```

感谢 Gaurav Ahirwar 提出了这种方法。

<https://youtu.be/WdgAKCnWnwA>