# 按频率对元素排序 | 系列 2

> 原文： [https://www.geeksforgeeks.org/sort-elements-by-frequency-set-2/](https://www.geeksforgeeks.org/sort-elements-by-frequency-set-2/)

给定整数数组，请根据元素的频率对数组进行排序。 例如，如果输入数组是`{2, 3, 2, 4, 5, 12, 12, 2, 3, 3, 3, 12}`，则将该数组修改为`{3, 3, 3, 3, 2, 2, 2, 12, 12, 4, 5}`。



在[以前的文章](https://www.geeksforgeeks.org/sort-elements-by-frequency/)中，我们讨论了根据频率进行排序的所有方法。 在本文中，将详细讨论方法 2，并提供了该方法的 C++ 实现。

以下是详细的算法。

*   创建一个 [BST](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/) ，并在创建 BST 时保持同一 BST 中每个即将到来的元素的计数即频率。 如果使用自平衡 BST，则此步骤可能需要`O(nLogn)`时间。

*   对 BST 进行遍历，并将每个元素和每个元素的计数存储在辅助数组中。 让我们将辅助数组称为`count[]`。 注意，该数组的每个元素都是元素和频率对。 此步骤需要`O(n)`时间。

*   根据元素的频率对`count[]`进行排序。 如果使用`O(nLogn)`排序算法，则此步骤需要`O(nLogn)`时间。

*   遍历排序后的数组`count[]`。 对于每个元素`x`，请按`freq`倍数打印，其中`freq`是`x`的频率。 此步骤需要`O(n)`时间。

如果我们使用`O(nLogn)`排序算法，并且将自平衡 BST 与`O(nLogn)`插入操作。

以下是上述算法的实现。

```

// Implementation of above algorithm in C++. 
#include <iostream> 
#include <stdlib.h> 
using namespace std; 

/* A BST node has data, freq, left and right pointers */
struct BSTNode 
{ 
    struct BSTNode *left; 
    int data; 
    int freq; 
    struct BSTNode *right; 
}; 

// A structure to store data and its frequency 
struct dataFreq 
{ 
    int data; 
    int freq; 
}; 

/* Function for qsort() implementation. Compare frequencies to 
   sort the array according to decreasing order of frequency */
int compare(const void *a, const void *b) 
{ 
    return ( (*(const dataFreq*)b).freq - (*(const dataFreq*)a).freq ); 
} 

/* Helper function that allocates a new node with the given data, 
   frequency as 1 and NULL left and right  pointers.*/
BSTNode* newNode(int data) 
{ 
    struct BSTNode* node = new BSTNode; 
    node->data = data; 
    node->left = NULL; 
    node->right = NULL; 
    node->freq = 1; 
    return (node); 
} 

// A utility function to insert a given key to BST. If element 
// is already present, then increases frequency 
BSTNode *insert(BSTNode *root, int data) 
{ 
    if (root == NULL) 
        return newNode(data); 
    if (data == root->data) // If already present 
        root->freq += 1; 
    else if (data < root->data) 
        root->left = insert(root->left, data); 
    else
        root->right = insert(root->right, data); 
    return root; 
} 

// Function to copy elements and their frequencies to count[]. 
void store(BSTNode *root, dataFreq count[], int *index) 
{ 
    // Base Case 
    if (root == NULL) return; 

    // Recur for left substree 
    store(root->left, count, index); 

    // Store item from root and increment index 
    count[(*index)].freq = root->freq; 
    count[(*index)].data = root->data; 
    (*index)++; 

    // Recur for right subtree 
    store(root->right, count, index); 
} 

// The main function that takes an input array as an argument 
// and sorts the array items according to frequency 
void sortByFrequency(int arr[], int n) 
{ 
    // Create an empty BST and insert all array items in BST 
    struct BSTNode *root = NULL; 
    for (int i = 0; i < n; ++i) 
        root = insert(root, arr[i]); 

    // Create an auxiliary array 'count[]' to store data and 
    // frequency pairs. The maximum size of this array would 
    // be n when all elements are different 
    dataFreq count[n]; 
    int index = 0; 
    store(root, count, &index); 

    // Sort the count[] array according to frequency (or count) 
    qsort(count, index, sizeof(count[0]), compare); 

    // Finally, traverse the sorted count[] array and copy the 
    // i'th item 'freq' times to original array 'arr[]' 
    int j = 0; 
    for (int i = 0; i < index; i++) 
    { 
        for (int freq = count[i].freq; freq > 0; freq--) 
            arr[j++] = count[i].data; 
    } 
} 

// A utility function to print an array of size n 
void printArray(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
    cout << endl; 
} 

/* Driver program to test above functions */
int main() 
{ 
    int arr[] = {2, 3, 2, 4, 5, 12, 2, 3, 3, 3, 12}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    sortByFrequency(arr, n); 
    printArray(arr, n); 
    return 0; 
} 

```

**输出**：

```
3 3 3 3 2 2 2 12 12 5 4
```

**练习**：

上面的实现并不能保证具有相同频率的元素的原始顺序（例如，输入 4 在 5 之前，而输出 4 在 5 之后）。 扩展实现以保持原始顺序。 例如，如果两个元素具有相同的频率，则在输入数组中打印第一个出现的元素。



