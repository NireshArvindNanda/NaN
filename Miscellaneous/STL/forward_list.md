# Forward list
+ Forward list in STL implements singly linked list.
+ Introduced from C++11, forward list are more useful than other containers in insertion, removal, and moving operations (like sort) and allow time constant insertion and removal of elements. 
+ It differs from the list by the fact that the forward list keeps track of the location of only the next element while the list keeps track of both the next and previous elements, thus increasing the storage space required to store each element. 
+ The drawback of a forward list is that it cannot be iterated backward and its individual elements cannot be accessed directly. 
+ Forward List is preferred over the list when only forward traversal is required (same as the singly linked list is preferred over doubly linked list) as we can save space. 
+ Some example cases are, chaining in hashing, adjacency list representation of the graph, etc.

## Operations on Forward List
- **assign():** This function is used to assign values to the forward list, its other variant is used to assign repeated elements and using the values of another list.
>
    Version 1:forward_list_name.assign(iterator it1, iterator it2)
    Version 2:forward_list_name.assign(int n, val)
    Version 3:forward_list_name.assign(initializer_list li)
- **push_front():** This function is used to insert the element at the first position on forward list. The value from this function is copied to the space before first element in the container. The size of forward list increases by 1.
- **emplace_front():** This function is similar to the previous function but in this no copying operation occurs, the element is created directly at the memory before the first element of the forward list.
- **pop_front():** This function is used to delete the first element of the list.  
- **insert_after():** This function gives us a choice to insert elements at any position in forward list. The arguments in this function are copied at the desired position.
    + **position, element:** The parameter position is of type iterator and it points to the location after which the value of parameter element is to be inserted.
    + **position, n, element:** The parameter position is of type iterator and it points to the location after which the value of parameter element is to be inserted. The parameter n specifies the number of times the value element is to inserted.
    + **position, itr1, itr2:** The parameter position is of type iterator and it points to the location after which the values to be inserted. The iterators itr1 and itr2 denotes a range [itr1, itr2) and the elements in this range including itr1 and excluding itr2 will be inserted to the forward list after the iterator pointing to the given position.
    + **position, list:** The parameter position is of type iterator and it points to the location after which the values are to be inserted. The second parameter list defines the list of elements to be inserted in the forward_list.
    + **Return Value :** This function returns an iterator that points to the last inserted element.

>
    forward_list_name.insert_after(iterator position, element)

    forward_list_name.insert_after(iterator position, n, element)

    forward_list_name.insert_after(iterator position, itr1, itr2)

    forward_list_name.insert_after(iterator position, list)

- **emplace_after():** This function also does the same operation as the above function but the elements are directly made without any copy operation.
>
    forward_list_name.emplace_after(iterator position, elements)
- **erase_after():** This function is used to erase elements from a particular position in the forward list. There are two varients of ‘erase after’ function.
>
    forwardlistname.clear()

    flistname.erase_after(position)

    flistname.erase_after(startingposition, endingposition)
    // deletes range (start,end) -> [start+1, end)

- **remove():** This function removes the particular element from the forward list mentioned in its argument.
>
    forwardlistname.remove(value)
- **remove_if():** This function removes according to the condition in its argument. 
>
    forwardlistname.remove_if(predicate)

- **clear():** This function deletes all the elements from the list. 
    forwardlistname.clear()
- **splice_after():** This function transfers elements from one forward list to other.
    + forward_list::splice_after() is an inbuilt function in CPP STL which transfers the elements in the range of first+1 to last from a given forward_list to another forward_list.
    + The elements are inserted after the element pointed to by position in the parameter.
    + **position –** Specifies the position in the forward_list after which the new elements are to be inserted.
    + **forwardlist2_name –** Specifies the list from which elements are to be inserted.
    + **first –** Specifies the iterator after which insertion is to be done.
    + **last –** Specifies the iterator till which insertion is to be done.
    + **Return value:** The function has no return value.

    >
        forwardlist1_name.splice_after(position iterator, forwardlist2_name, first iterator, last iterator)
    
- **front() -**	This function is used to reference the first element of the forward list container.
- **begin() -**	This function is used to return an iterator pointing to the first element of the forward list container.
- **end() -**	This function is used to return an iterator pointing to the last element of the list container.
- **cbegin() -**	Returns a constant iterator pointing to the first element of the forward_list.
- **cend() -**	Returns a constant iterator pointing to the past-the-last element of the forward_list.
- **before_begin() -**	Returns an iterator that points to the position before the first element of the forward_list.
- **cbefore_begin() -**	Returns a constant random access iterator which points to the position before the first element of the forward_list.
- **max_size() -**	Returns the maximum number of elements that can be held by forward_list.
- **resize() -**	Changes the size of forward_list.
- **unique() -**	Removes all consecutive duplicate elements from the forward_list. It uses a binary predicate for comparison.
- **reverse() -** 	Reverses the order of the elements present in the forward_list.
>
    forwardlist_name.reverse()
- **merge() :-** This function is used to merge one forward list with other. If both the lists are sorted then the resultant list returned is also sorted. 
    + Merge two forward lists that are sorted in ascending order into one.
    + Merge two forward lists into one using a comparison function.
    >
        forwardlist_name1.merge(forward_list& forwardlist_name2)
                    or
        forwardlist_name1.merge(forward_list& forwardlist_name2, Compare comp)
- **operator “=” :-** This operator copies one forward list into other. The copy made in this case is deep copy. 
- **sort() :-** This function is used to sort the forward list.
>
    forwardlistname.sort()
    forwardlistname.sort(predicate)
- swap() :- This function swaps the content of one forward list with other. 
>
    forwardlistname1.swap(forwardlistname2)