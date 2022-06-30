# List in C++
- Lists are sequence containers that allow non-contiguous memory allocation.
- As compared to vector, the list has slow traversal, but once a position has been found, insertion and deletion are quick.
- Normally, when we say a List, we talk about a doubly linked list.
- For implementing a singly linked list, we use a forward list.

+ **front()** -	Returns the value of the first element in the list.
    - Unlike the list::begin() function, this function returns a direct reference to the first element in the list container
+ **back()** -	Returns the value of the last element in the list.
+ **push_front(g)** -	Adds a new element ‘g’ at the beginning of the list.
>
    list_name.push_front(dataType value)
+ **push_back(g)** -	Adds a new element ‘g’ at the end of the list.
+ **pop_front()** -	Removes the first element of the list, and reduces size of the list by 1.
+ **pop_back()** -	Removes the last element of the list, and reduces size of the list by 1.
+ **list::begin()** - begin() function returns an iterator pointing to the first element of the list.
+ **list::end()** -	end() function returns an iterator pointing to the theoretical last element which follows the last element.
+ **list rbegin() and rend()** - rbegin() returns a reverse iterator which points to the last element of the list. rend() returns a reverse iterator which points to the position before the beginning of the list.
+ **list cbegin() and cend()** - cbegin() returns a constant random access iterator which points to the beginning of the list. cend() returns a constant random access iterator which points to the end of the list.
+ **list crbegin() and crend()** - crbegin() returns a constant reverse iterator which points to the last element of the list i.e reversed beginning of container. crend() returns a constant reverse iterator which points to the theoretical element preceding the first element in the list i.e. the reverse end of the list.
+ **empty()** - Returns whether the list is empty
+ **insert()** - Inserts new elements in the list before the element at a specified position.
    - This function takes 3 elements, position, number of elements to insert and value to insert.
    - If not mentioned, number of elements is default set to 1
    - Time Complexity – Linear O(N)
    >
        insert(pos_iter, ele_num, ele)

        pos_iter: Position in the container where the new elements are inserted.
        ele_num: Number of elements to insert. Each element is initialized to a copy of val.
        ele: Value to be copied (or moved) to the inserted elements.
+ **erase()** - Removes a single element or a range of elements from the list.
>
    iterator list_name.erase(iterator position)

>
    iterator list_name.erase(iterator first, iterator last)
+ **assign()** - Assigns new elements to list by replacing current elements and resizes the list.
>
    list_name.assign(count, value)
>
    first_list.assign(second_list.begin(), second_list.end());
+ **remove()** - Removes all the elements from the list, which are equal to given element.
>
    list_name.remove(val) 
+ **list::remove_if()** - Used to remove all the values from the list that correspond true to the predicate or condition given as parameter to the function.
>
    listname.remove_if(predicate)
    
    Parameters :
    The predicate in the form of aa function pointer or function object is passed as the parameter.
    
    Result :
    Removes all the elements of the container which return true for the predicate.
```cpp
bool even(const int& value) { return (value % 2) == 0; }
```

+ **reverse()** - Reverses the list.
>
    list_name.reverse()

+ **size()** - Returns the number of elements in the list.
    - Complexity
        + C++ 98 : Up to linear
        + C++ 11 : Constant 
    - Its a trade off, if size is O(1), then splice is O(n)
+ **list splice()** - Used to transfer elements from one list to another.
    - The list::splice() is a built-in function in C++ STL which is used to transfer elements from one list to another.
    - The splice() function can be used in three ways: 
        + Transfer all the elements of list x into another list at some position.
        + Transfer only the element pointed by i from list x into the list at some position.
        + Transfers the range [first, last) from list x into another list at some position.
    >
        list1_name.splice (iterator position, list2)
    >
        list1_name.splice (iterator position, list2, iterator i)
    >
        list1_name.splice (iterator position, list2, iterator first, iterator last)
    - C++11 now requires that size be constant and splice be linear.
+ **list resize()** - Used to resize a list container.
    - It takes a number n as parameter and resizes the list container to contain exactly n elements.
        + If the list already has more than n elements, then the function erases the elements from the list except the first n element.
        + If the list contains less than n elements, then the function adds the difference number of elements to the list with their default values.
        + The function also accepts a parameter val, if this parameter is specified and the number of elements in the list container is less than n then the function adds elements to the list with their value assigned to val.
    >
        list_name.resize(int n, value_type val = 0)
    - Complexity:
        + If the container grows, linear in the number number of elements inserted (constructor).
        + If the container shrinks, linear in the number of elements erased (destructions), plus up to linear in the size (iterator advance).

+ **std::list::sort()** -	Sorts the list in increasing order.
    - Lists are containers used in C++ to store data in a non contiguous fashion.
    -  Normally, Arrays and Vectors are contiguous in nature, therefore the insertion and deletion operations are costlier as compared to the insertion and deletion option in Lists.
    >
        listname.sort()
+ **list max_size()** - Returns the maximum number of elements a list container can hold.
    >
        list_name.max_size()
+ **list unique()** - Removes all duplicate consecutive elements from the list.
>
    list_name.unique()
>
    list_name.unique(BinaryPredicate name)

    bool name(data_type a, data_type b);

```cpp
bool compare(double a, double b)
{
    return ((int)a == (int)b);
}

list.unique(compare);
```
+ **list::emplace_front() and list::emplace_back()** - emplace_front() function is used to insert a new element into the list container, the new element is added to the beginning of the list. emplace_back() function is used to insert a new element into the list container, the new element is added to the end of the list.
>
    listname.emplace_front(value)
    - Time Complexity O(1)
+ **list::clear()** - clear() function is used to remove all the elements of the list container, thus making it size 0.
>
    listname.clear()
    - Time Complexity O(n)
+ **list::operator=** -	This operator is used to assign new contents to the container by replacing the existing contents.
>
    listname1 = listname2;
    - Time Complexity O(n)
+ **list::swap()** - This function is used to swap the contents of one list with another list of same type in constant time as it only changes the metadata.
>
    listname1.swap(listname2)
+ **list merge()** - Merges two sorted lists into one.
    - The list::merge() is an inbuilt function in C++ STL which merges two sorted lists into one.
    - The lists should be sorted in ascending order.
    - If no comparator is passed in parameter, then it merges two sorted lists into a single sorted list.
    - If a comparator is passed in the parameter, then it merges the list accordingly doing internal comparisons.
>
    list1_name.merge(list2_name)
```cpp
list<int> list1 = { 10, 20, 30 };
list<int> list2 = { 40, 50, 60 };

list2.merge(list1);
for (auto it = list2.begin(); it != list2.end(); ++it)
    cout << *it << " ";

// list1.size() = 0
```
    - Time complexity: O(n + m -1)
>
    list1_name.merge(list2_name, comparator)
    - comparator – It is a binary predicate which takes two values of the same type that of those contained in the list, returns true if the first argument is considered to go before the second in the strict weak ordering it defines, and false otherwise.
+ **list emplace()** - Extends list by inserting new element at a given position.
>
    list_name.emplace(position, element)

    position – it specifies the iterator which points to the position in the list where the new element is to be inserted.

    It returns a random access iterator which points to the newly inserted element.
```cpp
lis.emplace(lis.begin(), 2);
```