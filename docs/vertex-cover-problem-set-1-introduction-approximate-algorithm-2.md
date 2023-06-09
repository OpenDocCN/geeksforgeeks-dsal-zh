# 顶点覆盖问题|集合 1(介绍及近似算法)

> 原文:[https://www . geesforgeks . org/顶点-覆盖-问题-集合-1-简介-近似-算法-2/](https://www.geeksforgeeks.org/vertex-cover-problem-set-1-introduction-approximate-algorithm-2/)

无向图的顶点覆盖是其顶点的子集，使得对于图的每条边(u，v ), u 或 v 都在顶点覆盖中。虽然名称是顶点覆盖，但是集合覆盖了给定图形的所有边。 ***给定一个无向图，顶点覆盖问题是求最小尺寸的顶点覆盖*** 。
以下是一些例子。

![VertexCover](img/87bd7bd460f0e2648534ae16a5fd4969.png)

[顶点覆盖问题](http://en.wikipedia.org/wiki/Vertex_cover)是一个已知的 [NP 完全问题](https://www.geeksforgeeks.org/np-completeness-set-1/)，即这个问题没有多项式时间解，除非 P = NP。尽管有近似多项式时间算法来解决这个问题。下面是一个简单的近似算法，改编自 [CLRS 书籍](http://www.flipkart.com/introduction-algorithms-english-3rd/p/itmdwxyrafdburzg?pid=9788120340077&affid=sandeepgfg)。

**天真方法:**

逐个考虑顶点的所有子集，找出它是否覆盖了图的所有边。例如，在只有 3 个顶点的图中，由顶点组合组成的集合是:{0，1，2，{0，1}，{0，2}，{1，2}，{0，1，2}。使用这个集合的每个元素检查这些顶点是否覆盖了图的所有边。因此更新最佳答案。并因此打印具有最小顶点数的子集，该子集也覆盖图的所有边。

**顶点覆盖的近似算法:**

```
1) Initialize the result as {}
2) Consider a set of all edges in given graph.  Let the set be E.
3) Do following while E is not empty
...a) Pick an arbitrary edge (u, v) from set E and add 'u' and 'v' to result
...b) Remove all edges from E which are either incident on u or v.
4) Return result 
```

下图显示了上述近似算法的执行情况:

![vertexCover](img/994520baa83d60d915bcebafd01d5e8e.png)

**以上算法表现如何？**
可以证明上面的近似算法从来没有找到过大小超过最小可能顶点覆盖大小两倍的顶点覆盖(参考[这个](http://www.personal.kent.edu/~rmuhamma/Algorithms/MyAlgorithms/AproxAlgor/vertexCover.htm)进行证明)
**实现:**
下面是上面近似算法的 C++和 Java 实现。

## C++

```
// Program to print Vertex Cover of a given undirected graph
#include<iostream>
#include <list>
using namespace std;

// This class represents a undirected graph using adjacency list
class Graph
{
    int V;    // No. of vertices
    list<int> *adj;  // Pointer to an array containing adjacency lists
public:
    Graph(int V);  // Constructor
    void addEdge(int v, int w); // function to add an edge to graph
    void printVertexCover();  // prints vertex cover
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w); // Add w to v’s list.
    adj[w].push_back(v); // Since the graph is undirected
}

// The function to print vertex cover
void Graph::printVertexCover()
{
    // Initialize all vertices as not visited.
    bool visited[V];
    for (int i=0; i<V; i++)
        visited[i] = false;

    list<int>::iterator i;

    // Consider all edges one by one
    for (int u=0; u<V; u++)
    {
        // An edge is only picked when both visited[u] and visited[v]
        // are false
        if (visited[u] == false)
        {
            // Go through all adjacents of u and pick the first not
            // yet visited vertex (We are basically picking an edge
            // (u, v) from remaining edges.
            for (i= adj[u].begin(); i != adj[u].end(); ++i)
            {
                int v = *i;
                if (visited[v] == false)
                {
                     // Add the vertices (u, v) to the result set.
                     // We make the vertex u and v visited so that
                     // all edges from/to them would be ignored
                     visited[v] = true;
                     visited[u]  = true;
                     break;
                }
            }
        }
    }

    // Print the vertex cover
    for (int i=0; i<V; i++)
        if (visited[i])
          cout << i << " ";
}

// Driver program to test methods of graph class
int main()
{
    // Create a graph given in the above diagram
    Graph g(7);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(3, 4);
    g.addEdge(4, 5);
    g.addEdge(5, 6);

    g.printVertexCover();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print Vertex
// Cover of a given undirected graph
import java.io.*;
import java.util.*;
import java.util.LinkedList;

// This class represents an undirected
// graph using adjacency list
class Graph
{
    private int V;   // No. of vertices

    // Array  of lists for Adjacency List Representation
    private LinkedList<Integer> adj[];

    // Constructor
    Graph(int v)
    {
        V = v;
        adj = new LinkedList[v];
        for (int i=0; i<v; ++i)
            adj[i] = new LinkedList();
    }

    //Function to add an edge into the graph
    void addEdge(int v, int w)
    {
        adj[v].add(w);  // Add w to v's list.
        adj[w].add(v);  //Graph is undirected
    }

    // The function to print vertex cover
    void printVertexCover()
    {
        // Initialize all vertices as not visited.
        boolean visited[] = new boolean[V];
        for (int i=0; i<V; i++)
            visited[i] = false;

        Iterator<Integer> i;

        // Consider all edges one by one
        for (int u=0; u<V; u++)
        {
            // An edge is only picked when both visited[u]
            // and visited[v] are false
            if (visited[u] == false)
            {
                // Go through all adjacents of u and pick the
                // first not yet visited vertex (We are basically
                //  picking an edge (u, v) from remaining edges.
                i = adj[u].iterator();
                while (i.hasNext())
                {
                    int v = i.next();
                    if (visited[v] == false)
                    {
                         // Add the vertices (u, v) to the result
                         // set. We make the vertex u and v visited
                         // so that all edges from/to them would
                         // be ignored
                         visited[v] = true;
                         visited[u]  = true;
                         break;
                    }
                }
            }
        }

        // Print the vertex cover
        for (int j=0; j<V; j++)
            if (visited[j])
              System.out.print(j+" ");
    }

    // Driver method
    public static void main(String args[])
    {
        // Create a graph given in the above diagram
        Graph g = new Graph(7);
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 3);
        g.addEdge(3, 4);
        g.addEdge(4, 5);
        g.addEdge(5, 6);

        g.printVertexCover();
    }
}

// This code is contributed by Aakash Hasija
```

## 蟒蛇 3

```
# Python3 program to print Vertex Cover
# of a given undirected graph
from collections import defaultdict

# This class represents a directed graph
# using adjacency list representation
class Graph:

    def __init__(self, vertices):

        # No. of vertices
        self.V = vertices

        # Default dictionary to store graph
        self.graph = defaultdict(list)

    # Function to add an edge to graph
    def addEdge(self, u, v):
        self.graph[u].append(v)

    # The function to print vertex cover
    def printVertexCover(self):

        # Initialize all vertices as not visited.
        visited = [False] * (self.V)

        # Consider all edges one by one
        for u in range(self.V):

            # An edge is only picked when
            # both visited[u] and visited[v]
            # are false
            if not visited[u]:

                # Go through all adjacents of u and
                # pick the first not yet visited
                # vertex (We are basically picking
                # an edge (u, v) from remaining edges.
                for v in self.graph[u]:
                    if not visited[v]:

                        # Add the vertices (u, v) to the
                        # result set. We make the vertex
                        # u and v visited so that all
                        # edges from/to them would
                        # be ignored
                        visited[v] = True
                        visited[u] = True
                        break

        # Print the vertex cover
        for j in range(self.V):
            if visited[j]:
                print(j, end = ' ')

        print()

# Driver code

# Create a graph given in
# the above diagram
g = Graph(7)
g.addEdge(0, 1)
g.addEdge(0, 2)
g.addEdge(1, 3)
g.addEdge(3, 4)
g.addEdge(4, 5)
g.addEdge(5, 6)

g.printVertexCover()

# This code is contributed by Prateek Gupta
```

## C#

```
// C# Program to print Vertex
// Cover of a given undirected
// graph
using System;
using System.Collections.Generic;

// This class represents an
// undirected graph using
// adjacency list
class Graph{

// No. of vertices
public int V;

// Array of lists for
// Adjacency List Representation
public List<int> []adj;

// Constructor
public Graph(int v)
{
  V = v;
  adj = new List<int>[v];

  for (int i = 0; i < v; ++i)
    adj[i] = new List<int>();
}

//Function to add an edge
// into the graph
void addEdge(int v, int w)
{
   // Add w to v's list.
  adj[v].Add(w);

  //Graph is undirected
  adj[w].Add(v);
}

// The function to print
// vertex cover
void printVertexCover()
{
  // Initialize all vertices
  // as not visited.
  bool []visited = new bool[V];

  // Consider all edges one
  // by one
  for (int u = 0; u < V; u++)
  {
    // An edge is only picked
    // when both visited[u]
    // and visited[v] are false
    if (visited[u] == false)
    {
      // Go through all adjacents
      // of u and pick the first
      // not yet visited vertex
      // (We are basically picking
      // an edge (u, v) from remaining
      // edges.
      foreach(int i in adj[u])
      {
        int v = i;
        if (visited[v] == false)
        {
          // Add the vertices (u, v)
          // to the result set. We
          // make the vertex u and
          // v visited so that all
          // edges from/to them would
          // be ignored
          visited[v] = true;
          visited[u] = true;
          break;
        }
      }
    }
  }

  // Print the vertex cover
  for (int j = 0; j < V; j++)
    if (visited[j])
      Console.Write(j + " ");
}

// Driver method
public static void Main(String []args)
{
  // Create a graph given in
  // the above diagram
  Graph g = new Graph(7);
  g.addEdge(0, 1);
  g.addEdge(0, 2);
  g.addEdge(1, 3);
  g.addEdge(3, 4);
  g.addEdge(4, 5);
  g.addEdge(5, 6);

  g.printVertexCover();
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript Program to print Vertex
// Cover of a given undirected graph

// This class represents an undirected
// graph using adjacency list
class Graph
{   
    // Constructor
    constructor(v)
    {
        this.V=v;
        this.adj = new Array(v);
        for (let i = 0; i < v; ++i)
            this.adj[i] = [];
    }

    // Function to add an edge into the graph
    addEdge(v, w)
    {
        this.adj[v].push(w);  // Add w to v's list.
        this.adj[w].push(v);  //Graph is undirected
    }

     // The function to print vertex cover
    printVertexCover()
    {
        // Initialize all vertices as not visited.
        let visited = new Array(this.V);
        for (let i = 0; i < this.V; i++)
            visited[i] = false;

        // Consider all edges one by one
        for (let u = 0; u < this.V; u++)
        {
            // An edge is only picked when both visited[u]
            // and visited[v] are false
            if (visited[u] == false)
            {
                // Go through all adjacents of u and pick the
                // first not yet visited vertex (We are basically
                //  picking an edge (u, v) from remaining edges.

                for(let i = 0; i < this.adj[u].length; i++)
                {
                    let v = this.adj[u][i];
                    if (visited[v] == false)
                    {

                         // Add the vertices (u, v) to the result
                         // set. We make the vertex u and v visited
                         // so that all edges from/to them would
                         // be ignored
                         visited[v] = true;
                         visited[u]  = true;
                         break;
                    }
                }
            }
        }

        // Print the vertex cover
        for (let j = 0; j < this.V; j++)
            if (visited[j])
              document.write(j+" ");
    }
}

// Driver method
// Create a graph given in the above diagram
let g = new Graph(7);
g.addEdge(0, 1);
g.addEdge(0, 2);
g.addEdge(1, 3);
g.addEdge(3, 4);
g.addEdge(4, 5);
g.addEdge(5, 6);

g.printVertexCover();

// This code is contributed by patel2127
</script>
```

输出:

```
0 1 3 4 5 6
```

上述算法的时间复杂度为 O(V + E)。
**精确算法:**
虽然问题是 NP 完全的，但对于以下类型的图，可以在多项式时间内解决。
1) [二部图](https://www.geeksforgeeks.org/bipartite-graph/)
2) [树形图](http://geeksquiz.com/check-given-graph-tree/)
如果 k 以 O(LogV)为界，那么检查是否存在大小小于或等于给定数 k 的顶点覆盖的问题也可以在多项式时间内解决(参考[这个](http://en.wikipedia.org/wiki/Vertex_cover#Fixed-parameter_tractability) )
我们很快将讨论顶点覆盖的精确算法。
本文由**舒巴姆**供稿。如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论