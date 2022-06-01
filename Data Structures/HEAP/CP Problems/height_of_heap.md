# Height of heap

## Find the height of heap

[https://practice.geeksforgeeks.org/problems/height-of-heap5025/1/?page=1&difficulty[]=-1&category[]=Heap&sortBy=submissions](https://practice.geeksforgeeks.org/problems/height-of-heap5025/1/?page=1&difficulty[]=-1&category[]=Heap&sortBy=submissions)

* **Approach to solve**

  * think about the tallest path in the tree
  * we can use the fact that it is a complete binary tree
  * from the last leaf node we can trace back to the root and count the nodes along the way

* **Code**

```
class Solution{
public:
    int heapHeight(int N, int arr[]){
        // code here
        int i=N-1,cnt=0;
        while(i>0){
            i=(int)((i-1)/2);
            cnt++;
            
        }
        return cnt;
    }
};
```


