# K nearly sorted elements

## Problem statement

Sort the array wherein each element is at most k position away from it's original position when sorted

* **Approach to solve**

  * Use a priority queue to push in the elements until there are k+1 elements into a min queue
  * When the size is k+1, the root will have the min element and also that will be it's correct place as the elements are k position away from its sorted position

* **Code**

```cpp
class Solution
{
    public:
    //Function to return the sorted array.
    vector <int> nearlySorted(int arr[], int num, int K){
        // Your code here
        priority_queue<int , vector<int> , greater<int> > pq;
        vector<int> v;
        for(int i=0;i<num;i++){
            pq.push(arr[i]);
            
            if(pq.size()==K+1){
                v.push_back(pq.top());
                pq.pop();
            }
        }
        
        while(pq.size()){
            v.push_back(pq.top());pq.pop();
        }
        return v;
        
        
    }
    

};

```
