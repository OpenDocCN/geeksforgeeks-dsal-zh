# 洪水填充算法–如何在绘图中实现`fill()`？

> 原文： [https://www.geeksforgeeks.org/flood-fill-algorithm-implement-fill-paint/](https://www.geeksforgeeks.org/flood-fill-algorithm-implement-fill-paint/)

在 MS-Paint 中，当我们将画笔带到一个像素并单击时，该像素区域的颜色将替换为新的选定颜色。 以下是执行此任务的问题说明。

给定 2D 屏幕，屏幕中像素的位置和颜色，用给定颜色替换给定像素和所有相邻的相同彩色像素的颜色。

**示例**：

```
Input:
       screen[M][N] = {{1, 1, 1, 1, 1, 1, 1, 1},
                      {1, 1, 1, 1, 1, 1, 0, 0},
                      {1, 0, 0, 1, 1, 0, 1, 1},
                      {1, 2, 2, 2, 2, 0, 1, 0},
                      {1, 1, 1, 2, 2, 0, 1, 0},
                      {1, 1, 1, 2, 2, 2, 2, 0},
                      {1, 1, 1, 1, 1, 2, 1, 1},
                      {1, 1, 1, 1, 1, 2, 2, 1},
                      };
    x = 4, y = 4, newColor = 3
The values in the given 2D screen indicate colors of the pixels.
x and y are coordinates of the brush, newColor is the color that
should replace the previous color on screen[x][y] and all surrounding
pixels with same color.

Output:
Screen should be changed to following.
       screen[M][N] = {{1, 1, 1, 1, 1, 1, 1, 1},
                      {1, 1, 1, 1, 1, 1, 0, 0},
                      {1, 0, 0, 1, 1, 0, 1, 1},
                      {1, 3, 3, 3, 3, 0, 1, 0},
                      {1, 1, 1, 3, 3, 0, 1, 0},
                      {1, 1, 1, 3, 3, 3, 3, 0},
                      {1, 1, 1, 1, 1, 3, 1, 1},
                      {1, 1, 1, 1, 1, 3, 3, 1},
                      };

```



[**Flood-Fill 算法**](http://en.wikipedia.org/wiki/Flood_fill)：

这个想法很简单，我们首先替换当前像素的颜色，然后对 4 个周围的点进行递归。 以下是详细的算法。

```
// A recursive function to replace previous color 'prevC' at  '(x, y)' 
// and all surrounding pixels of (x, y) with new color 'newC' and
floodFil(screen[M][N], x, y, prevC, newC)
1) If x or y is outside the screen, then return.
2) If color of screen[x][y] is not same as prevC, then return
3) Recur for north, south, east and west.
    floodFillUtil(screen, x+1, y, prevC, newC);
    floodFillUtil(screen, x-1, y, prevC, newC);
    floodFillUtil(screen, x, y+1, prevC, newC);
    floodFillUtil(screen, x, y-1, prevC, newC); 
```

以下是上述算法的实现。

## C++ 

```cpp

// A C++ program to implement flood fill algorithm 
#include<iostream> 
using namespace std; 

// Dimentions of paint screen 
#define M 8 
#define N 8 

// A recursive function to replace previous color 'prevC' at  '(x, y)'  
// and all surrounding pixels of (x, y) with new color 'newC' and 
void floodFillUtil(int screen[][N], int x, int y, int prevC, int newC) 
{ 
    // Base cases 
    if (x < 0 || x >= M || y < 0 || y >= N) 
        return; 
    if (screen[x][y] != prevC) 
        return; 
    if (screen[x][y] == newC)  
        return;  

    // Replace the color at (x, y) 
    screen[x][y] = newC; 

    // Recur for north, east, south and west 
    floodFillUtil(screen, x+1, y, prevC, newC); 
    floodFillUtil(screen, x-1, y, prevC, newC); 
    floodFillUtil(screen, x, y+1, prevC, newC); 
    floodFillUtil(screen, x, y-1, prevC, newC); 
} 

// It mainly finds the previous color on (x, y) and 
// calls floodFillUtil() 
void floodFill(int screen[][N], int x, int y, int newC) 
{ 
    int prevC = screen[x][y]; 
    floodFillUtil(screen, x, y, prevC, newC); 
} 

// Driver program to test above function 
int main() 
{ 
    int screen[M][N] = {{1, 1, 1, 1, 1, 1, 1, 1}, 
                      {1, 1, 1, 1, 1, 1, 0, 0}, 
                      {1, 0, 0, 1, 1, 0, 1, 1}, 
                      {1, 2, 2, 2, 2, 0, 1, 0}, 
                      {1, 1, 1, 2, 2, 0, 1, 0}, 
                      {1, 1, 1, 2, 2, 2, 2, 0}, 
                      {1, 1, 1, 1, 1, 2, 1, 1}, 
                      {1, 1, 1, 1, 1, 2, 2, 1}, 
                     }; 
    int x = 4, y = 4, newC = 3; 
    floodFill(screen, x, y, newC); 

    cout << "Updated screen after call to floodFill: \n"; 
    for (int i=0; i<M; i++) 
    { 
        for (int j=0; j<N; j++) 
           cout << screen[i][j] << " "; 
        cout << endl; 
    } 
} 

```