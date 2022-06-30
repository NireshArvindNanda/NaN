# Deque in STL
- Double-ended queues are sequence containers with the feature of expansion and contraction on both ends.
- They are similar to vectors, but are more efficient in case of insertion and deletion of elements.
- Unlike vectors, contiguous storage allocation may not be guaranteed. 
- Double Ended Queues are basically an implementation of the data structure double-ended queue.
- A queue data structure allows insertion only at the end and deletion from the front.
- This is like a queue in real life, wherein people are removed from the front and added at the back.
- Double-ended queues are a special case of queues where insertion and deletion operations are possible at both the ends.
- The functions for deque are same as vector, with an addition of push and pop operations for both front and back.  
- Accessing Elements- O(1)
- Insertion or removal of elements- O(N)
- Insertion or removal of elements at start or end- O(1)

## Internal representation
- A deque is somewhat recursively defined:
- internally it maintains a double-ended queue of chunks of fixed size.
- Each chunk is a vector, and the queue (“map” in the graphic below) of chunks itself is also a vector.

![Internal representation](https://i.stack.imgur.com/SthOW.png)

- Deque is a double ended queue container that provides insertion and deletion at both ends i.e. front and back with high performance unlike vector that provides high performance insertion at end i.e. back only.
- Also it provides random access to elements just like a vector. Although one can insert an element in between other elements in dequeue with insert() function, but its performance will not be good just like vector.
- A deque is generally implemented as a collection of memory blocks.
- These memory blocks contains the elements at contiguous locations.

![Internal representation](https://thispointer.com/wp-content/uploads/2015/07/deque.png)
- Insertion at front is fast as compared to vector because it doesn’t need the elements to shift by 1 in current memory block to make space at front.
- It just checks if any space is left at left of first element in current memory block, if not then allocates a new memory block.
![Some more insight](https://i.stack.imgur.com/2m7Yk.png)

## Methods on Deque
- **deque::insert()** -	Inserts an element. And returns an iterator that points to the first of the newly inserted elements.
    + Extends deque by inserting a new element val at a position.
    + Extends deque by inserting n new element of value val in the deque.
    + Extends deque by inserting new element in the range [first, last).
>
    deque_name.insert (iterator position, const value_type& val)
                    or
    deque_name.insert (iterator position, size_type n, const value_type& val)
                    or
    deque_name.insert (iterator position, InputIterator first, InputIterator last)
- **deque::rbegin()** -	Returns a reverse iterator which points to the last element of the deque (i.e., its reverse beginning).
- **deque::rend()** -	Returns a reverse iterator which points to the position before the beginning of the deque (which is considered its reverse end).
- **deque::cbegin()** -	Returns a constant iterator pointing to the first element of the container, that is, the iterator cannot be used to modify, only traverse the deque.
- **deque::max_size()** -	Returns the maximum number of elements that a deque container can hold.
- **deque::assign()** -	Assign values to the same or different deque container.
>
    deque_name.assign(size, val)

>
    deque1_name.assign(iterator1, iterator2)
- **deque::resize()** - 	Function which changes the size of the deque.
- **deque::push_front()** -	It is used to push elements into a deque from the front.
- **deque::push_back()** - 	This function is used to push elements into a deque from the back.
- **deque::pop_front() and deque::pop_back()** -	pop_front() function is used to pop or remove elements from a deque from the front. pop_back() function is used to pop or remove elements from a deque from the back.
- **deque::front() and deque::back()** -	front() function is used to reference the first element of the deque container. back() function is used to reference the last element of the deque container.
- **deque::clear() and deque::erase()** - 	clear() function is used to remove all the elements of the deque container, thus making its size 0. erase() function is used to remove elements from a container from the specified position or range.
>
    dequename.erase(position)
    dequename.erase(startingposition, endingposition)
- **deque::empty() and deque::size()** -	empty() function is used to check if the deque container is empty or not. size() function is used to return the size of the deque container or the number of elements in the deque container.
- **deque::operator= and deque::operator[]** -	operator= operator is used to assign new contents to the container by replacing the existing contents. operator[] operator is used to reference the element present at position given inside the operator.
    + This operator is used to reference the element present at position given inside the operator. It is similar to the at() function, the only difference is that the at() function throws an out-of-range exception when the position is not in the bounds of the size of deque, while this operator causes undefined behavior
>
    dequename[position] -> O(1)
    dequename1 = (dequename2) -> O(n)

- **deque::at() and deque::swap()** -	at() function is used reference the element present at the position given as the parameter to the function. swap() function is used to swap the contents of one deque with another deque of same type and size.
>
    mydeque.at(3);
    dequename1.swap(dequename2) -> O(1)
- **deque::begin() and deque::end** - 	begin() function is used to return an iterator pointing to the first element of the deque container. end() function is used to return an iterator pointing to the last element of the deque container.
- **deque::emplace_front() and deque::emplace_back()** - 	emplace_front() function is used to insert a new element into the deque container. The new element is added to the beginning of the deque. emplace_back() function is used to insert a new element into the deque container. The new element is added to the end of the deque.
