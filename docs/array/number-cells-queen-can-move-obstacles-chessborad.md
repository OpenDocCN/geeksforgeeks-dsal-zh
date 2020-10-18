# 皇后可以在棋盘上移动的障碍物数量

> 原文： [https://www.geeksforgeeks.org/number-cells-queen-can-move-obstacles-chessborad/](https://www.geeksforgeeks.org/number-cells-queen-can-move-obstacles-chessborad/)

考虑带有女王和`K`障碍物的`N X N`棋盘。 女王不能穿越障碍。 给定皇后的位置`(x, y)`，任务是找到皇后可以移动的单元格数。

例子：

```
Input : N = 8, x = 4, y = 4, 
        K = 0
Output : 27

Input : N = 8, x = 4, y = 4, 
        K = 1, kx1 = 3, ky1 = 5
Output : 24

```



**方法 1**：

这个想法是迭代女王可以攻击并停止的单元格，直到有障碍物或棋盘末端为止。 为此，我们需要水平，垂直和对角线迭代。 从位置`(x, y)`的移动可以是：

`(x + 1, y)`：向右水平移动一级。

`(x-1, y)`：向左水平移动一级。

`(x + 1, y + 1)`：对角线向右移动一级。

`(x-1, y-1)`：对角线向左下移动。

`(x-1, y + 1)`：对角线左移一格。

`(x + 1, y-1)`：对角线向右下移 1 步。

`(x, y + 1)`：下移一步。

`(x, y-1)`：向上迈出一步。

以下是此方法的 C++ 实现：

```

// C++ program to find number of cells a queen can move  
// with obstacles on the chessborad 
#include<bits/stdc++.h> 
using namespace std; 

// Return if position is valid on chessboard 
int range(int n, int x, int y) 
{ 
  return (x <= n && x > 0 && y <= n && y > 0); 
} 

// Return the number of moves with a given direction 
int check(int n, int x, int y, int xx, int yy,  
                  map <pair<int, int>, int> mp) 
{ 
  int ans = 0; 

  // Checking valid move of Queen in a direction. 
  while (range(n, x, y) && ! mp[{x, y}]) 
  { 
    x += xx; 
    y += yy; 
    ans++; 
  } 

  return ans; 
} 

// Return the number of position a Queen can move. 
int numberofPosition(int n, int k, int x, int y,  
                  int obstPosx[], int obstPosy[]) 
{ 
  int x1, y1, ans = 0; 
  map <pair<int, int>, int> mp; 

  // Mapping each obstacle's position 
  while(k--) 
  { 
    x1 = obstPosx[k]; 
    y1 = obstPosy[k]; 

    mp[{x1, y1}] = 1; 
  } 

  // Fetching number of position a queen can 
  // move in each direction. 
  ans += check(n, x + 1, y, 1, 0, mp); 
  ans += check(n, x-1, y, -1, 0, mp); 
  ans += check(n, x, y + 1, 0, 1, mp); 
  ans += check(n, x, y-1, 0, -1, mp); 
  ans += check(n, x + 1, y + 1, 1, 1, mp); 
  ans += check(n, x + 1, y-1, 1, -1, mp); 
  ans += check(n, x-1, y + 1, -1, 1, mp); 
  ans += check(n, x-1, y-1, -1, -1, mp); 

  return ans; 
} 

// Driven Program 
int main() 
{ 
  int n = 8;  // Chessboard size 
  int k = 1;  // Number of obstacles 
  int Qposx = 4; // Queen x position 
  int Qposy = 4; // Queen y position 
  int obstPosx[] = { 3 };  // x position of obstacles 
  int obstPosy[] = { 5 };  // y position of obstacles 

  cout << numberofPosition(n, k, Qposx, Qposy,  
                   obstPosx, obstPosy) << endl; 
  return 0; 
} 

```

输出：

```
24

```

**方法 2**：

这个想法是要遍历障碍物，对于那些走在皇后大道上的人，我们计算到达障碍物的自由细胞。 如果路径上没有障碍，我们必须计算到该方向上板端的空闲单元数。

对于任何`(x1, y1)`和`(x2, y2)`：

*   如果它们在同一水平线上：`abs(x1 – x2 – 1)`。

*   如果它们在垂直方向上处于同一水平：`abs(y1 – y2 – 1)`是它们之间的空闲单元数。

*   如果它们是对角线：`abs(x1 – x2 – 1)`或`abs(y1 – y2 – 1 )`是之间的空闲单元数。

以下是此方法的实现：

## C++ 

```cpp

// C++ program to find number of cells a queen can move 
// with obstacles on the chessborad 
#include <bits/stdc++.h> 
using namespace std; 

// Return the number of position a Queen can move. 
int numberofPosition(int n, int k, int x, int y, 
                    int obstPosx[], int obstPosy[]) 
{ 
    // d11, d12, d21, d22 are for diagnoal distances. 
    // r1, r2 are for vertical distance. 
    // c1, c2 are for horizontal distance. 
    int d11, d12, d21, d22, r1, r2, c1, c2; 

    // Initialise the distance to end of the board. 
    d11 = min( x-1, y-1 ); 
    d12 = min( n-x, n-y ); 
    d21 = min( n-x, y-1 ); 
    d22 = min( x-1, n-y ); 

    r1 = y-1; 
    r2 = n-y; 
    c1 = x-1; 
    c2 = n-x; 

    // For each obstacle find the minimum distance. 
    // If obstacle is present in any direction, 
    // distance will be updated. 
    for (int i = 0; i < k; i++) 
    { 
        if ( x > obstPosx[i] && y > obstPosy[i] && 
                 x-obstPosx[i] == y-obstPosy[i] ) 
            d11 = min(d11, x-obstPosx[i]-1); 

        if ( obstPosx[i] > x && obstPosy[i] > y && 
                  obstPosx[i]-x == obstPosy[i]-y ) 
            d12 = min( d12, obstPosx[i]-x-1); 

        if ( obstPosx[i] > x && y > obstPosy[i] && 
                   obstPosx[i]-x == y-obstPosy[i] ) 
            d21 = min(d21, obstPosx[i]-x-1); 

        if ( x > obstPosx[i] && obstPosy[i] > y && 
                    x-obstPosx[i] == obstPosy[i]-y ) 
            d22 = min(d22, x-obstPosx[i]-1); 

        if ( x == obstPosx[i] && obstPosy[i] < y ) 
            r1 = min(r1, y-obstPosy[i]-1); 

        if ( x == obstPosx[i] && obstPosy[i] > y ) 
            r2 = min(r2, obstPosy[i]-y-1); 

        if ( y == obstPosy[i] && obstPosx[i] < x ) 
            c1 = min(c1, x-obstPosx[i]-1); 

        if ( y == obstPosy[i] && obstPosx[i] > x ) 
            c2 = min(c2, obstPosx[i]-x-1); 
    } 

    return d11 + d12 + d21 + d22 + r1 + r2 + c1 + c2; 
} 

// Driver code 
int main(void) 
{ 
    int n = 8;  // Chessboard size 
    int k = 1;  // number of obstacles 
    int Qposx = 4; // Queen x position 
    int Qposy = 4; // Queen y position 
    int obstPosx[] = { 3 };  // x position of obstacles 
    int obstPosy[] = { 5 };  // y position of obstacles 

    cout << numberofPosition(n, k, Qposx, Qposy, 
                             obstPosx, obstPosy); 
    return 0; 
} 

```