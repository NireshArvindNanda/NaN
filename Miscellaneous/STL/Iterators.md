# Iterators in C++
+ Iterators are used to point at the memory addresses of STL containers.
+ An iterator is an object (like a pointer) that points to an element inside the container.
+ We can use iterators to move through the contents of the container.
+ They can be visualized as something similar to a pointer pointing to some location and we can access the content at that particular location using them.
+ Iterators play a critical role in connecting algorithm with containers along with the manipulation of data stored inside the containers.
+ The most obvious form of an iterator is a pointer.
+ A pointer can point to elements in an array and can iterate through them using the increment operator (++).
+ But, all iterators do not have similar functionality as that of pointers.
+ Depending upon the functionality of iterators they can be classified into five categories
+ Each one of these iterators are not supported by all the containers in STL, different containers support different iterators.

## Input Iterators:
+ They are the weakest of all the iterators and have very limited functionality.
+ They can only be used in a single-pass algorithms, i.e., those algorithms which process the container sequentially, such that no element is accessed more than once.
+ They are the iterators that can be used in sequential input operations, where each value pointed by the iterator is read-only once and then the iterator is incremented.
+ One important thing to be kept in mind is that forward, bidirectional and random-access iterators are also valid input iterators.
+ Input iterators are used only when we want to access elements and not when we have to assign elements to them.
### Equality / Inequality Comparison:
+ An input iterator can be compared for equality with another iterator.
+ Since, iterators point to some location, so the two iterators will be equal only when they point to the same position, otherwise not.
>
    A == B  // Checking for equality
    A != B  // Checking for inequality
### Dereferencing:
>
    *A       // Dereferencing using *
    A -> m   // Accessing a member element m
### Incrementable:
+ An input iterator can be incremented, so that it refers to the next element in the sequence, using operator ++().
+ The fact that we can use input iterators with increment operator doesn’t mean that operator – -() can also be used with them.
+ Remember, that input iterators are unidirectional and can only move in the forward direction.
>
    A++   // Using post increment operator
    ++A   // Using pre increment operator
### Swappable

### Relational Operators:
>
    If A and B are input iterators, then
    A == B     // Allowed
    A <= B     // Not Allowed
### Arithmetic Operators:
>
    If A and B are input iterators, then
    A + 1     // Not allowed
    B - 2     // Not allowed
## Output Iterators:
+ Just like input iterators, they are also very limited in their functionality and can only be used in single-pass algorithm, but not for accessing elements, but for being assigned elements.
### Equality / Inequality Comparison:
+ Unlike input iterators, output iterators cannot be compared for equality with another iterator.
>
    A == B  // Invalid - Checking for equality
    A != B  // Invalid - Checking for inequality
### Dereferencing:
+ An input iterator can be dereferenced as an rvalue, using operator * and ->, whereas an output iterator can be dereferenced as an lvalue to provide the location to store the value.
>
    *A = 1      // Dereferencing using *
    A -> m = 7   // Assigning a member element m
### Incrementable:
>
    A++   // Using post increment operator
    ++A   // Using pre increment operator
### Swappable

>
    If A is an output iterator,then
    A--    // Not allowed with output iterators

## Forward Iterator:
+ They are higher in the hierarchy than input and output iterators, and contain all the features present in these two iterators. But, as the name suggests, they also can only move in a forward direction and that too one step at a time.
### Usability:
+ Performing operations on a forward iterator that is dereferenceable never makes its iterator value non-dereferenceable, as a result this enables algorithms that use this category of iterators to use multiple copies of an iterator to pass more than once by the same iterator values.
+ So, it can be used in multi-pass algorithms.
### Equality / Inequality Comparison:
+ A forward iterator can be compared for equality with another iterator. Since, iterators point to some location, so the two iterators will be equal only when they point to the same position, otherwise not.
>
    A == B  // Checking for equality
    A != B  // Checking for inequality
### Dereferencing:
+ Because an input iterator can be dereferenced, using the operator * and -> as an rvalue and an output iterator can be dereferenced as an lvalue, so forward iterators can be used for both the purposes.
```cpp
for (i1 = v1.begin(); i1 != v1.end(); ++i1) {
    // Assigning values to locations pointed by iterator
    *i1 = 1;
}

for (i1 = v1.begin(); i1 != v1.end(); ++i1) {
    // Accessing values at locations pointed by iterator
    cout << (*i1) << " ";
}
```
### Incrementable:
>
    A++   // Using post increment operator
    ++A   // Using pre increment operator

### Swappable
### Limitations
#### Can not be decremented
>  
    A--    // Not allowed with forward iterators
#### Relational Operators
>
    A == B     // Allowed
    A <= B     // Not Allowed
#### Arithmetic Operators
>
    If A and B are forward iterators, then

    A + 1     // Not allowed
    B - 2     // Not allowed
#### Use of offset dereference operator ( [] )
>
    If A is a forward iterator, then
    A[3]    // Not allowed 
## Bidirectional Iterators:
+ They have all the features of forward iterators along with the fact that they overcome the drawback of forward iterators, as they can move in both the directions, that is why their name is bidirectional.
+ list, map, multimap, set and multiset support bidirectional iterators.
+ This means that if we declare normal iterators for them, and then those will be bidirectional iterators, just like in case of vectors and deque they are random-access iterators.
```cpp
template 
void random_shuffle(RandomAccessIterator first, RandomAccessIterator last, RandomNumberGenerator& gen)
{
    iterator_traits::difference_type i, n;
    n = (last - first);
    for (i=n-1; i>0; --i) 
    {
        swap (first[i],first[gen(i+1)]);
    }
}
```
+ Here, we can see that we have made use of Random-access iterators, as although we can increment a bidirectional iterator, decrement it as well, but we cannot apply **arithmetic operator like +, –** to it and this what is required in this algorithm , where **(last – first)** is done, so, for this reason, we cannot use a bidirectional iterator in these scenarios.
### Limitations
#### Relational Operators
>
    If A and B are Bidirectional iterators, then

    A == B     // Allowed
    A <= B     // Not Allowed

#### Arithmetic Operators
>
    If A and B are Bidirectional iterators, then

    A + 1     // Not allowed
    B - 2     // Not allowed
```cpp
list<int>v1 = {1, 2, 3, 4, 5};

list<int>::iterator i1;
list<int>::iterator i2;

i1 = v1.begin();
i2 = v1.end();

// Applying relational operator to them
if ( i1 > i2)
    cout << "Yes";
// Error, because of use of arithmetic and relational operators with bidirectional iterators 
```
#### Use of offset dereference operator ( [] )
>
    If A is a Bidirectional iterator, then
    A[3]    // Not allowed 
## Random-Access Iterators:
+ They are the most powerful iterators.
+ They are not limited to moving sequentially, as their name suggests, they can randomly access any element inside the container.
+ Random-access iterators are iterators that can be used to access elements at an arbitrary offset position relative to the element they point to, offering the same functionality as pointers.
+ Random-access iterators are the most complete iterators in terms of functionality.
+ All pointer types are also valid random-access iterators.
+ Iterator algorithms do not depend on the container type. As the iterators provide common usage for all of them, the internal structure of a container does not matter.

## Benefits of Iterators
### Convenience in programming:
+ It is better to use iterators to iterate through the contents of containers as if we will not use an iterator and access elements using [ ] operator, then we need to be always worried about the size of the container, whereas with iterators we can simply use member function end() and iterate through the contents without having to keep anything in mind. 
### Code reusability:
+ Now consider if we make var a list in place of vector in a program and if we were not using iterators to access the elements and only using [ ] operator, then in that case this way of accessing was of no use for list (as they don’t support random-access iterators). However, if we were using iterators for vectors to access the elements, then just changing the vector to list in the declaration of the iterator would have served the purpose, without doing anything else.
+ So, iterators support reusability of code, as they can be used to access elements of any container.
### Dynamic processing of the container:
+ Iterators provide us the ability to dynamically add or remove elements from the container as and when we want with ease.
```cpp
int main()
{
    // Declaring a vector
    vector<int> v = { 1, 2, 3 };
 
    // Declaring an iterator
    vector<int>::iterator i;
 
    int j;
 
    // Inserting element using iterators
    for (i = v.begin(); i != v.end(); ++i) {
        if (i == v.begin()) {
            i = v.insert(i, 5);
            // inserting 5 at the beginning of v
        }
    }
     
    // v contains 5 1 2 3
 
    // Deleting a element using iterators
    for (i = v.begin(); i != v.end(); ++i) {
        if (i == v.begin() + 1) {
            i = v.erase(i);
            // i now points to the element after the
            // deleted element
        }
    }
     
    // v contains 5 2 3
 
    // Accessing the elements using iterators
    for (i = v.begin(); i != v.end(); ++i) {
        cout << *i << " ";
    }
 
    return 0;
}
```

## Operations of iterators :-

### begin() :-
+ This function is used to return the beginning position of the container.

### end() :-
+ This function is used to return the after end position of the container.
```cpp
vector<int> ar = { 1, 2, 3, 4, 5 };
vector<int>::iterator ptr;
ptr = ar.begin();
```
### advance() :-
+ This function is used to increment the iterator for the specified number of times mentioned in its arguments.
```cpp
advance(ptr, 3);
```

###  next() :-
+ This function returns the new iterator that the iterator would point after advancing the positions mentioned in its arguments.

### prev() :-
+ This function returns the new iterator that the iterator would point after decrementing the positions mentioned in its arguments.
```cpp
auto it = next(ptr, 3);
auto it1 = prev(ptr1, 3);
```

### std::next vs std::advance
>
    template
    void advance( InputIt& it, Distance n );

    it: Iterator to be advanced
    n: Distance to be advanced

>
    ForwardIterator next (ForwardIterator it,
        typename iterator_traits::difference_type n = 1);

    it: Iterator pointing to base position
    n: Distance to be advanced from base position.

+ std::advance does not return anything, whereas std::next returns an iterator after advancing n positions from the given base position.
+ std::next has a default argument of 1, whereas if we use std::advance, it has no such default argument.
+ std::advance modifies it arguments such that it points to the desired position, whereas, std::next does not modify its argument, infact it returns a new iterator pointing to the desired position.
+ std::next requires the iterator passed as argument to be of type at least forward iterator, whereas std::advance doesnot have such restrictions, as it can work with any iterator, even with input iterator or better than it.

Inserter(https://www.geeksforgeeks.org/stdinserter-in-cpp/)