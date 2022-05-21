
# HEAP

- MAX-HEAP The parent element value is greater than its child values

- siftDown swaps a node that is too small with its largest child (thereby moving it down) until it is at least as large as both nodes below it.

- siftUp swaps a node that is too large with its parent (thereby moving it up) until it is no larger than the node above it. The buildHeap function takes an array of unsorted items and moves them until it they all satisfy the heap property.

There are two approaches one might take for buildHeap. One is to start at the top of the heap (the beginning of the array) and call siftUp on each item. At each step, the previously sifted items (the items before the current item in the array) form a valid heap, and sifting the next item up places it into a valid position in the heap. After sifting up each node, all items satisfy the heap property. The second approach goes in the opposite direction: start at the end of the array and move backwards towards the front. At each iteration, you sift an item down until it is in the correct location.

The normal approach is to do a bottom up scan of the array, and perform a sift-down of each node. The time for each level would be the number of nodes in the level multiplied by the height (since sift-down is recusrive and might swap all the way to the bottom level). The total time would be O(1*n/2 + 2*n/4 + 3*n/8 + ...)=O(n)*(1/2 + 2/4 + 3/8 + ...)=O(n)*2=O(n). [**Taylor series**]

- siftDown swaps a node that is too small with its largest child (thereby moving it down) until it is at least as large as both nodes below it.
  + ( Step 1 ) The first n/2 elements go on the bottom row of the heap. h=0, so heapify is not needed.

  + ( Step 2 ) The next n/22 elements go on the row 1 up from the bottom. h=1, heapify filters 1 level down.

  + ( Step i ) The next n/2i elements go in row i up from the bottom. h=i, heapify filters i levels down.

  + ( Step log(n) ) The last n/2log2(n) = 1 element goes in row log(n) up from the bottom. h=log(n), heapify filters log(n) levels down.

  - (0 * n/2) + (1 * n/4) + (2 * n/8) + ... + (h * 1).
- siftUp swaps a node that is too large with its parent (thereby moving it up) until it is no larger than the node above it.
  - (h * n/2) + ((h-1) * n/4) + ((h-2)*n/8) + ... + (0 * 1).

> Note:
> - Root is at index 0 in array.
> - Left child of i-th node is at (2*i + 1)th index.
> - Right child of i-th node is at (2*i + 2)th index.
> - Parent of i-th node is at (i-1)/2 index.

> - Last non-leaf node = parent of last-node.
> - or, Last non-leaf node = parent of node at (n-1)th index.
> - or, Last non-leaf node = Node at index ((n-1) - 1)/2.
> -                        = (n/2) - 1.


```cpp
void heapify(int arr[], int n, int i)
{
    int largest = i; // Initialize largest as root
    int l = 2 * i + 1; // left = 2*i + 1
    int r = 2 * i + 2; // right = 2*i + 2
 
    // If left child is larger than root
    if (l < n && arr[l] > arr[largest])
        largest = l;
 
    // If right child is larger than largest so far
    if (r < n && arr[r] > arr[largest])
        largest = r;
 
    // If largest is not root
    if (largest != i) {
        swap(arr[i], arr[largest]);
 
        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}
 
// Function to build a Max-Heap from the given array
void buildHeap(int arr[], int n)
{
    // Index of last non-leaf node
    int startIdx = (n / 2) - 1;
 
    // Perform reverse level order traversal
    // from last non-leaf node and heapify
    // each node
    for (int i = startIdx; i >= 0; i--) {
        heapify(arr, n, i);
    }
}
```