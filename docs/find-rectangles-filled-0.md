# 查找所有填充为 0 的矩形

> 原文： [https://www.geeksforgeeks.org/find-rectangles-filled-0/](https://www.geeksforgeeks.org/find-rectangles-filled-0/)

我们有一个 2D 数组，其中填充了零和一。 我们必须找到所有填充为 0 的矩形的起点和终点。假定矩形是分开的并且彼此不接触，但是它们可以接触数组的边界。一个矩形可能只包含一个元素。

例子：

```
input = [
            [1, 1, 1, 1, 1, 1, 1],
            [1, 1, 1, 1, 1, 1, 1],
            [1, 1, 1, 0, 0, 0, 1],
            [1, 0, 1, 0, 0, 0, 1],
            [1, 0, 1, 1, 1, 1, 1],
            [1, 0, 1, 0, 0, 0, 0],
            [1, 1, 1, 0, 0, 0, 1],
            [1, 1, 1, 1, 1, 1, 1]
        ]

Output:
[
  [2, 3, 3, 5], [3, 1, 5, 1], [5, 3, 6, 5]
]

Explanation:
We have three rectangles here, starting from 
(2, 3), (3, 1), (5, 3)

Input = [
            [1, 0, 1, 1, 1, 1, 1],
            [1, 1, 0, 1, 1, 1, 1],
            [1, 1, 1, 0, 0, 0, 1],
            [1, 0, 1, 0, 0, 0, 1],
            [1, 0, 1, 1, 1, 1, 1],
            [1, 1, 1, 0, 0, 0, 0],
            [1, 1, 1, 1, 1, 1, 1],
            [1, 1, 0, 1, 1, 1, 0]
        ]

Output:
[
  [0, 1, 0, 1], [1, 2, 1, 2], [2, 3, 3, 5], 
  [3, 1, 4, 1], [5, 3, 5, 6], [7, 2, 7, 2], 
  [7, 6, 7, 6]
]

```



步骤 1：按行和列查找 0

第 2 步：遇到任何 0 时，将其位置保存在输出数组中，并使用循环以任何公共数字更改与此位置相关的所有 0，以便我们下次可以将其排除在外。

步骤 3：在步骤 2 中更改所有相关的 0 时，将最后处理的 0 的位置存储在同一索引的输出数组中。

第 4 步：触摸边缘时要特别小心，不要减去 -1，因为循环在确切的位置上已经断开。

下面是上述方法的实现：

```

# Python program to find all  
# rectangles filled with 0 

def findend(i,j,a,output,index): 
    x = len(a) 
    y = len(a[0]) 

    # flag to check column edge case, 
    # initializing with 0 
    flagc = 0

    # flag to check row edge case, 
    # initializing with 0 
    flagr = 0

    for m in range(i,x):  

        # loop breaks where first 1 encounters 
        if a[m][j] == 1:  
            flagr = 1 # set the flag 
            break

        # pass because already processed 
        if a[m][j] == 5:  
            pass

        for n in range(j, y):  

            # loop breaks where first 1 encounters 
            if a[m][n] == 1: 
                flagc = 1 # set the flag 
                break

            # fill rectangle elements with any 
            # number so that we can exclude 
            # next time 
            a[m][n] = 5

    if flagr == 1: 
        output[index].append( m-1) 
    else: 
        # when end point touch the boundary 
        output[index].append(m)  

    if flagc == 1: 
        output[index].append(n-1) 
    else: 
        # when end point touch the boundary 
        output[index].append(n)  

def get_rectangle_coordinates(a): 

    # retrieving the column size of array 
    size_of_array = len(a)  

    # output array where we are going 
    # to store our output  
    output = []  

    # It will be used for storing start 
    # and end location in the same index 
    index = -1

    for i in range(0,size_of_array): 
        for j in range(0, len(a[0])): 
            if a[i][j] == 0: 

                # storing initial position  
                # of rectangle 
                output.append([i, j])  

                # will be used for the  
                # last position 
                index = index + 1        
                findend(i, j, a, output, index)  

    print (output) 

# driver code 
tests = [ 

            [1, 1, 1, 1, 1, 1, 1], 
            [1, 1, 1, 1, 1, 1, 1], 
            [1, 1, 1, 0, 0, 0, 1], 
            [1, 0, 1, 0, 0, 0, 1], 
            [1, 0, 1, 1, 1, 1, 1], 
            [1, 0, 1, 0, 0, 0, 0], 
            [1, 1, 1, 0, 0, 0, 1], 
            [1, 1, 1, 1, 1, 1, 1] 

        ] 

get_rectangle_coordinates(tests) 

```

输出：

```
[[2, 3, 3, 5], [3, 1, 5, 1], [5, 3, 6, 5]]

```


