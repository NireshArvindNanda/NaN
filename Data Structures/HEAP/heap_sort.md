# Heap sort (in-place, not stable)

#### [https://practice.geeksforgeeks.org/problems/heap-sort/1/#](https://practice.geeksforgeeks.org/problems/heap-sort/1/#)


* **Approach to solve**

  1.  Two functions - ```heapify(arr,size of heap,index to heapify)``` and ```buildheap(arr,n)```
  2.  ```heapify()``` takes in the size of the array and recursively checks the node's children for any swap, if swapped recurse for ```heapify()``` for swapped node
  3.  ```buildheap()``` takes the array elements and builds the heap by calling ```heapify()``` on elements from ```(n/2)-1``` till ```0th``` index

* **Core Concept**

  * ```(n/2)-1``` is the last parent node in a heap
  * siftdown is better as it has least operations especially from ```n/2``` until ```0```

* **Code**

```
void heapify(int arr[], int n, int i) {
    // Find largest among root, left child and right child
    int largest = i;
    int left=2*i+1;
    int right = 2*i+2;
    
    if(left<n && arr[left]>arr[largest])
        largest=left;
    if(right<n && arr[right]>arr[largest])
        largest = right;
    if(largest!=i){
        int temp=arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;
        
        heapify(arr,n,largest);
    }
}

// Main function to do heap sort
void buildHeap(int arr[], int n) {
    // Build max heap
    for(int i=(n/2)-1;i>=0;i--){
        heapify(arr,n,i);
    }
    for(int i=n-1;i>0;i--){
        int temp=arr[i];
        arr[i]=arr[0];
        arr[0]=temp;
        
        heapify(arr,i,0);
    }
    
}
```

* **Time complexity** ```O(n*log n)```
* **Space complexity** ```O(log h)``` in worst case the stack space for ```heapify()```

* **References**

[https://www.geeksforgeeks.org/heap-sort/](https://www.geeksforgeeks.org/heap-sort/)
