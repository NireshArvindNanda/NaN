# Priority Queue in C++ Standard Template Library (STL)

- Priority queues are a type of container adapters, specifically designed such that the first element of the queue is either the greatest or the smallest of all elements in the queue and elements are in nonincreasing order (hence we can see that each element of the queue has a priority {fixed order}).
- However in C++ STL, by default, the top element is always the greatest element.
- We can also change it to the smallest element at the top.
- **Priority queues are built on the top to the max heap and uses array or vector as an internal structure.**
    + so custom function is a reverse
    + usually in stl, comp(a,b) 
        * returns ture is a is logically less than b
        * or a is before b in order
    + as priority_queue is implemented on top of max heap, if comp(a,b) return true, it means a < b -> meaning b will be placed higher in level (near root)

```cpp
    template <class T, class Container = vector<T>,
    class Compare = less<typename Container::value_type> > class priority_queue;
```

- **empty -** Test whether container is empty (public member function )
- **size -** Return size (public member function )
- **top -** Access top element (public member function )
- **push -** Insert element (public member function )
- **emplace -** Construct and insert element (public member function )
- **pop -** Remove top element (public member function )
- **swap -** Swap contents (public member function )

### How to create a min-heap for the priority queue? 
We can pass another parameter while creating the priority queue to make it a min heap. C++ provides the below syntax for the same.  

Syntax:
>
    priority_queue <int, vector<int>, greater<int>> g = gq;  

- The above syntax may be difficult to remember, so in case of numeric values, we can multiply the values with -1 and use max heap to get the effect of min heap.

```cpp
priority_queue<int> pq1(arr, arr+3);     // creating priority queue using array
```