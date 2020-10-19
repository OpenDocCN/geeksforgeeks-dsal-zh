# 康威的生命游戏程序

> 原文： [https://www.geeksforgeeks.org/program-for-conways-game-of-life/](https://www.geeksforgeeks.org/program-for-conways-game-of-life/)

最初，有一个网格，其中包含一些可能存在或死亡的单元格。 我们根据以下规则生成下一代单元的任务：

1.  任何具有少于两个活邻居的活细胞都会死亡，好像是由于人口不足所致。

2.  任何有两个或三个活邻居的活细胞都可以存活到下一代。

3.  任何具有三个以上活邻居的活细胞都会死亡，就好像人口过多一样。

4.  具有正好三个活邻居的任何死细胞都将变成一个活细胞，就像通过繁殖一样。

示例：

`"*"`代表存活的细胞，而`"."`代表死亡的细胞。

```
Input : ..........
        ...**.....
        ....*.....
        ..........
        ..........
Output: ..........
        ...**.....
        ...**.....
        ..........
        ..........
        ..........

Input : ..........
        ...**.....
        ....*.....
        ..........
        ..........
        ...**.....
        ..**......
        .....*....
        ....*.....
        ..........
Output: ..........
        ...**.....
        ...**.....
        ..........
        ..........
        ..***.....
        ..**......
        ...**.....
        ..........
        ..........
```



这是“生命游戏”的简单 Java 实现。 初始化为 0 的网格代表死细胞，而 1 的网格则代表活细胞。 `generate()`函数循环遍历每个单元并计算其邻居。 基于该值，实现上述规则。 以下实现忽略了边缘单元，因为它应该在无限平面上播放。

## Java

```java

// A simple Java program to implement Game of Life 
public class GameOfLife 
{ 
    public static void main(String[] args) 
    { 
        int M = 10, N = 10; 

        // Intiliazing the grid. 
        int[][] grid = { { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 1, 1, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 1, 1, 0, 0, 0, 0, 0 }, 
            { 0, 0, 1, 1, 0, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 0, 1, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 } 
        }; 

        // Displaying the grid 
        System.out.println("Original Generation"); 
        for (int i = 0; i < M; i++) 
        { 
            for (int j = 0; j < N; j++) 
            { 
                if (grid[i][j] == 0) 
                    System.out.print("."); 
                else
                    System.out.print("*"); 
            } 
            System.out.println(); 
        } 
        System.out.println(); 
        nextGeneration(grid, M, N); 
    } 

    // Function to print next generation 
    static void nextGeneration(int grid[][], int M, int N) 
    { 
        int[][] future = new int[M][N]; 

        // Loop through every cell 
        for (int l = 1; l < M - 1; l++) 
        { 
            for (int m = 1; m < N - 1; m++) 
            { 
                // finding no Of Neighbours that are alive 
                int aliveNeighbours = 0; 
                for (int i = -1; i <= 1; i++) 
                    for (int j = -1; j <= 1; j++) 
                        aliveNeighbours += grid[l + i][m + j]; 

                // The cell needs to be subtracted from 
                // its neighbours as it was counted before 
                aliveNeighbours -= grid[l][m]; 

                // Implementing the Rules of Life 

                // Cell is lonely and dies 
                if ((grid[l][m] == 1) && (aliveNeighbours < 2)) 
                    future[l][m] = 0; 

                // Cell dies due to over population 
                else if ((grid[l][m] == 1) && (aliveNeighbours > 3)) 
                    future[l][m] = 0; 

                // A new cell is born 
                else if ((grid[l][m] == 0) && (aliveNeighbours == 3)) 
                    future[l][m] = 1; 

                // Remains the same 
                else
                    future[l][m] = grid[l][m]; 
            } 
        } 

        System.out.println("Next Generation"); 
        for (int i = 0; i < M; i++) 
        { 
            for (int j = 0; j < N; j++) 
            { 
                if (future[i][j] == 0) 
                    System.out.print("."); 
                else
                    System.out.print("*"); 
            } 
            System.out.println(); 
        } 
    } 
} 

```

## C#

```
// A simple C# program to implement 
// Game of Life 
using System; 
  
public class GFG { 
      
    public static void Main() 
    { 
        int M = 10, N = 10; 
  
        // Intiliazing the grid. 
        int[,] grid = { 
            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 1, 1, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 1, 1, 0, 0, 0, 0, 0 }, 
            { 0, 0, 1, 1, 0, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 0, 1, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 }, 
            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 } 
        }; 
  
        // Displaying the grid 
        Console.WriteLine("Original Generation"); 
        for (int i = 0; i < M; i++) 
        { 
            for (int j = 0; j < N; j++) 
            { 
                if (grid[i,j] == 0) 
                    Console.Write("."); 
                else
                    Console.Write("*"); 
            } 
            Console.WriteLine(); 
        } 
        Console.WriteLine(); 
        nextGeneration(grid, M, N); 
    } 
  
    // Function to print next generation 
    static void nextGeneration(int [,]grid, 
                               int M, int N) 
    { 
        int[,] future = new int[M,N]; 
  
        // Loop through every cell 
        for (int l = 1; l < M - 1; l++) 
        { 
            for (int m = 1; m < N - 1; m++) 
            { 
                  
                // finding no Of Neighbours 
                // that are alive 
                int aliveNeighbours = 0; 
                for (int i = -1; i <= 1; i++) 
                    for (int j = -1; j <= 1; j++) 
                        aliveNeighbours +=  
                                grid[l + i,m + j]; 
  
                // The cell needs to be subtracted 
                // from its neighbours as it was  
                // counted before 
                aliveNeighbours -= grid[l,m]; 
  
                // Implementing the Rules of Life 
  
                // Cell is lonely and dies 
                if ((grid[l,m] == 1) &&  
                            (aliveNeighbours < 2)) 
                    future[l,m] = 0; 
  
                // Cell dies due to over population 
                else if ((grid[l,m] == 1) &&  
                             (aliveNeighbours > 3)) 
                    future[l,m] = 0; 
  
                // A new cell is born 
                else if ((grid[l,m] == 0) && 
                            (aliveNeighbours == 3)) 
                    future[l,m] = 1; 
  
                // Remains the same 
                else
                    future[l,m] = grid[l,m]; 
            } 
        } 
  
        Console.WriteLine("Next Generation"); 
        for (int i = 0; i < M; i++) 
        { 
            for (int j = 0; j < N; j++) 
            { 
                if (future[i,j] == 0) 
                    Console.Write("."); 
                else
                    Console.Write("*"); 
            } 
            Console.WriteLine(); 
        } 
    } 
} 
  
// This code is contributed by Sam007.
```


输出：

```
Original Generation
..........
...**.....
....*.....
..........
..........
...**.....
..**......
.....*....
....*.....
..........

Next Generation
..........
...**.....
...**.....
..........
..........
..***.....
..**......
...**.....
..........
..........
```

上面的实现是非常基本的。 尝试提出一个更有效的实现，并确保在下面对其进行评论。 另外，还可以尝试为细胞自动机创建自己的规则。
