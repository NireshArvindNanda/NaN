
# Vector in CPP
+ Vectors are the same as dynamic arrays with the ability to resize itself automatically when an element is inserted or deleted, with their storage being handled automatically by the container.
+ Vector elements are placed in contiguous storage so that they can be accessed and traversed using iterators.
+ In vectors, data is inserted at the end.
+ Inserting at the end takes differential time, as sometimes the array may need to be extended.
+ Removing the last element takes only constant time because no resizing happens.
+ Inserting and erasing at the beginning or in the middle is linear in time.

## Certain functions associated with the vector 
### Iterators

+ **begin()** – Returns an iterator pointing to the first element in the vector
+ **end()** – Returns an iterator pointing to the theoretical element that follows the last element in the vector
+ **rbegin()** – Returns a reverse iterator pointing to the last element in the vector (reverse beginning). It moves from last to first element
+ **rend()** – Returns a reverse iterator pointing to the theoretical element preceding the first element in the vector (considered as reverse end)
```cpp
cout << "The vector elements in reverse order are:\n";
for (auto it = v.rbegin(); it != v.rend(); it++)
    cout << *it << " ";
// Note it is ++ and not --
```
+ **cbegin()** – Returns a constant iterator pointing to the first element in the vector.
>
    Iterator cannot modify the contents of the vector.
+ **cend()** – Returns a constant iterator pointing to the theoretical element that follows the last element in the vector.
```cpp
// Declare a regular iterator to a vector
vector<int>::iterator i;
// Declare a const_itearor to a vector
vector<int>::const_iterator ci;
```
+ **crbegin()** – Returns a constant reverse iterator pointing to the last element in the vector (reverse beginning). It moves from last to first element
+ **crend()** – Returns a constant reverse iterator pointing to the theoretical element preceding the first element in the vector (considered as reverse end)

### Related to size
+ **size()** – Returns the number of elements in the vector.
+ **empty()** – Returns whether the container is empty.
>
    empty() function does not use any comparison operators, thus it is more convenient to use
    empty() function is implemented in constant time, regardless of container type, whereas some implementations of size() function require O(n) time complexity such as list::size().


+ **max_size()** – Returns the maximum number of elements that the vector can hold.
>
    max_size() is the theoretical maximum number of items that could be put in your vector.
    On a 32-bit system, you could in theory allocate 4Gb == 2^32 
    which is 2^32 char values,
    2^30 int values 
    or 2^29 double values. 
>
    std::vector<char>::max_size() returns 232-1, size of char — 1 byte
    std::vector<int>::max_size() returns 230-1, size of int — 4 byte
    std::vector<double>::max_size() returns 229-1, size of double — 8 byte
+ **capacity()** – Returns the size of the storage space currently allocated to the vector expressed as number of elements.
    - This capacity is not necessarily equal to the vector size.
    - It can be equal to or greater, with the extra space allowing to accommodate for growth without the need to reallocate on each insertion. 
    - The capacity does not suppose a limit on the size of the vector.
    - When this capacity is exhausted and more is needed, it is automatically expanded by the container (reallocating it storage space).
    - The theoretical limit on the size of a vector is given by member max_size.
    - Capacity is the maximum number of elements that the vector can store without reallocation.
    - when size is becoming greater than capacity, the runtime library will request fresh memory from the heap and once memory is allocated, it will copy all elements in the vector from their old addresses to the newly allocated memory address.

+ **resize(n)** – Resizes the container so that it contains ‘n’ elements.
    - If the given value of n is less than the size at present then extra elements are demolished.
    - If n is more than current size of container then upcoming elements are appended at the end of the vector.
    >
        vectorname.resize(int n, int val = 0)
        n – it is new container size, expressed in number of elements.
        val – if this parameter is specified then new elements are initialized with this value.

+ **shrink_to_fit()** – Reduces the capacity of the container to fit its size and destroys all elements beyond the capacity.
    >
        vector_name.shrink_to_fit()
    - Time Complexity – Linear O(N)
+ **reserve()** – Requests that the vector capacity be at least enough to contain n elements.
    >
        void reserve(size_type n)
        Return Type: none
        Arguments: n which denotes the no of elements to be stored in vector

        Requests that vector is large enough to store n elements in the least. 
        If the current vector capacity is less than n, then reallocation will 
        take place. In other cases, reallocation will not happen. Function does
        not modify existing elements in the vector
    - Time Complexity – Linear O(N)
#### useful
>
    std::int8_t   # exactly  8 bits
    std::int16_t  # exactly 16 bits
    std::int32_t  # exactly 32 bits
    std::int64_t  # exactly 64 bits

    std::size_t   # can hold all possible object sizes, used for indexing

### Element access:
+ **vector::operator=** 
>
    vectorname1 = (vectorname2)
    
    Parameters :
    Another container of the same type.
    
    Result :
    Assign the contents of the container passed as parameter to the container written on left side of the operator.
    
    Errors and Exceptions:
    If the containers are of different types, an error is thrown. 

    Time Complexity – Linear O(N)

+ **reference operator [g]** – Returns a reference to the element at position ‘g’ in the vector
    - This operator is used to reference the element present at position given inside the operator.
    -  It is similar to the at() function, the only difference is that the at() function throws an out-of-range exception when the position is not in the bounds of the size of vector, while this operator causes undefined behavior.
    >
        vectorname[position]

        Parameters :
        Position of the element to be fetched.
        
        Returns :
        Direct reference to the element at the given position.

        Time Complexity – Constant O(1)

+ **at(g)** – Returns a reference to the element at position ‘g’ in the vector
+ **front()** – Returns a reference to the first element in the vector
    - If the vector container is empty, it causes undefined behavior. 
    - begin() and end() function return an iterator(like a pointer)

+ **back()** – Returns a reference to the last element in the vector
>
    vectorname.back()

+ **data()** – Returns a direct pointer to the memory array used internally by the vector to store its owned elements.
>
    vector_name.data()
    
    Parameters: 
    The function does not accept any parameters.
    
    Return value:
    The function returns a pointer to the first element in the array which is used internally by the vector.

    Time Complexity – Constant O(1)

```cpp
int* pos = vec.data();

for (int i = 0; i < vec.size(); ++i)
    cout << *pos++ << " ";
```

### Modifiers: 
+ **assign()** – It assigns new value to the vector elements by replacing old ones
>
    vectorname.assign(int size, int value);

    Parameters: 
    size - number of values to be assigned
    value - value to be assigned to the vectorname

>
    vectorname.assign(arr, arr + size);

>
    vectorname.assign(InputIterator first, InputIterator last);

>
    vectorname.assign({initializer_list});
+ **push_back()** – It push the elements into a vector from the back
>
    vectorname.push_back(value)
+ **pop_back()** – It is used to pop or remove elements from a vector from the back.
+ **insert()** – It inserts new elements before the element at the specified position
    - Time Complexity – Linear O(N)
    >
        vector_name.insert (position, val)

        position – It specifies the iterator which points to the position where the insertion is to be done.
        val – It specifies the value to be inserted.
    
    >
        vector_name.insert(position, size, val)
        size – It specifies the number of times a val is to be inserted at the specified position.
    
    >
        vector_name.insert(position, iterator1, iterator2)
        iterator1 – It specifies the starting position from which the elements are to be inserted
        iterator2 – It specifies the ending position till which elements are to be inserted

+ **swap()** – It is used to swap the contents of one vector with another vector of same type. Sizes may differ.
    >
        vectorname1.swap(vectorname2)
        
        Parameters:
        The name of the vector with which the contents have to be swapped.
        
        Result: 
        All the elements of the 2 vectors are swapped.

        Errors and Exceptions  
        It throws an error if the vector is not of the same type.

        Time Complexity – Constant O(1)
        It swaps the addresses(i.e. the containers exchange references to their data) of two vectors rather than swapping each element one by one which is done in constant time O(1).

+ **clear()** – It is used to remove all the elements of the vector container, thus making its size 0.
    - Time Complexity: O(N) 
    - All elements are destroyed one by one.
>
    vectorname.clear()

+ **erase()** – It is used to remove elements from a container from the specified position or range.
    - Time Complexity: O(N) in the worst case as an erase takes linear time.

>
    vectorname.erase(position)
    vectorname.erase(startingposition, endingposition)

```cpp
for (auto i = myvector.begin(); i != myvector.end(); ++i) {
    if (*i % 2 == 0) {
        myvector.erase(i);
        i--;
    }
}
```
+ **emplace()** – It extends the container by inserting new element at position
>
    template 
    iterator vector_name.emplace (const_iterator position, element);
+ **emplace_back()** – It is used to insert a new element into the vector container, the new element is added to the end of the vector
>
    vectorname.emplace_back(value)
#### emplace vs insert
- The advantage of emplace is, it does in-place insertion and avoids an unnecessary copy of object.
- For primitive data types, it does not matter which one we use.
- But for objects, use of emplace() is preferred for efficiency reasons.