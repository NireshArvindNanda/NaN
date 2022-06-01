# k largest elements

## Return the k largest elements from array

[https://practice.geeksforgeeks.org/problems/k-largest-elements3736/1/?page=1&difficulty[]=-1&category[]=Heap&sortBy=submissions#](https://practice.geeksforgeeks.org/problems/k-largest-elements3736/1/?page=1&difficulty[]=-1&category[]=Heap&sortBy=submissions#)


* **Approach to solve**

  * whenever there is top k or least k asked think heaps first 
  * if heaps cannot optimize the problem go with the usual way
  * use a max heap to return the k largest element
  
* **Code**

```
class Solution
{
    public:
    //Function to return k largest elements from an array.
    vector<int> kLargest(int arr[], int n, int k)
    {
        // code here
        priority_queue<int> pq;
        for(int i=0;i<n;i++){
            pq.push(arr[i]);
        }
        vector<int> v;
        for(int i=0;i<k;i++){
            v.push_back(pq.top());
            pq.pop();
        }
        return v;
    }
};
```

* **Data structures used**

  * priority queue
  
* **Library functions available**

  * [priority_queue](https://en.cppreference.com/w/cpp/container/priority_queue) 

* **Time complexity** O(n log k)

* **Space complexity** O(k)

  
