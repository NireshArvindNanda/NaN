
# The C++ Standard Template Library (STL)

It is a set of C++ template classes to provide common programming data structures and functions.
It is a generalized library and so, its components are parameterized.

STL has four components
- Algorithms
- Containers
- Functions
- Iterators

## Algorithms
The header algorithm defines a collection of functions especially designed to be used on ranges of elements.They act on containers and provide means for various operations for the contents of the containers.

### Sorting
This function internally uses IntroSort. In more details it is implemented using hybrid of QuickSort, HeapSort and InsertionSort.By default, it uses QuickSort but if QuickSort is doing unfair partitioning and taking more than N*logN time, it switches to HeapSort and when the array size becomes really small, it switches to InsertionSort. 

[Please read](https://www.geeksforgeeks.org/know-your-sorting-algorithm-set-2-introsort-cs-sorting-weapon/)

**sort(startaddress, endaddress)**

- **startaddress:** the address of the first element of the array
- **endaddress:** the address of the next contiguous location of the last element of the array.
- So actually sort() sorts in the range of [startaddress,endaddress)
- We can also write our own comparator function and pass it as a third parameter.
- This “comparator” function returns a value; convertible to bool, which basically tells us whether the passed “first” argument should be placed before the passed “second” argument or not. 

The **time complexity** of std::sort() is:
+ Best Case – O(N log N)
+ Average Case – O(N log N)
+ Worst Case – O(N log N)

**Space Complexity**

It may use O( log N) auxiliary space.
```cpp
int a[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
int asize = sizeof(a) / sizeof(a[0]);
sort(a, a + asize);
```

### Binary Search (divide and conquer)

**binary_search(startaddress, endaddress, valuetofind)**

- **startaddress:** the address of the first element of the array.
- **endaddress:** the address of the next contiguous location of the last element of the array.
- **valuetofind:** the target value which we have to search for.
- **returns** true if an element equal to valuetofind is found, else false.

```cpp
int a[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
int asize = sizeof(a) / sizeof(a[0]);
sort(a, a + asize);
binary_search(a, a + 10, 10);
```

### Other useful Algorithms

- **reverse(first_iterator, last_iterator)**
- ***max_element (first_iterator, last_iterator)**
It returns a pointer to the largest element 
in the range, and in case if there are more than one such element,
then it points to the first one.
It points to the last in case the range is empty.

```cpp
bool comp(int a, int b)
{
    return (a < b);
}
  
int main()
{
    int v[] = { 9, 4, 7, 2, 5, 10, 11, 12, 1, 3, 6 };
  
    // Finding the maximum value between the third and the
    // ninth element
  
    int* i1;
    i1 = std::max_element(v + 2, v + 9, comp);
  
    cout << *i1 << "\n";
    return 0;
}
```
- ***min_element (first_iterator, last_iterator)**
- **accumulate(first_iterator, last_iterator, initial value of sum)** – Does the summation of vector elements
- **count(first_iterator, last_iterator,x)** – To count the occurrences of x in vector.
- **find(first_iterator, last_iterator, x)** – Returns an iterator to the first occurrence of x in vector and points to last address ((name_of_vector).end()) if element is not present.
- **lower_bound(first_iterator, last_iterator, x)** – returns an iterator pointing to the first element in the range [first,last) which has a value not less than ‘x’.
- **upper_bound(first_iterator, last_iterator, x)** – returns an iterator pointing to the first element in the range [first,last) which has a value greater than ‘x’.

```cpp
// To count the number of occurences of x
upper_bound(first_iterator, last_iterator, x) - lower_bound(first_iterator, last_iterator, x);
```

- **arr.erase(position to be deleted)** – This erases selected element in vector and shifts and resizes the vector elements accordingly.
- **arr.erase(unique(arr.begin(),arr.end()),arr.end())** – This erases the duplicate occurrences in sorted vector in a single line.

**std::unique** is used to remove duplicates of any element present consecutively in a range[first, last). It performs this task for all the sub-groups present in the range having the same element present consecutively.

+ It does not delete all the duplicate elements, but it removes duplicacy by just replacing those elements by the next element present in the sequence which is not duplicate to the current element being replaced. All the elements which are replaced are left in an unspecified state.
+ Another interesting feature of this function is that it does not changes the size of the container after deleting the elements, it just returns a pointer pointing to the new end of the container, and based upon that we have to resize the container, or remove the garbage elements.

> 
    ForwardIterator unique (ForwardIterator first, ForwardIterator last);

+ **first:** Forward iterator to the first element in the container.
+ **last:** forward iterator to the last element in the container.
+ **Return Value:** It returns an iterator to the element that follows the last element not removed.

**It only removes repeated duplicates**
1,1,2,2,1,1,1 -> 1,2,1,$,$,$,$

To remove remove all duplicates, sort first.

lower_bound and upper_bound requires sorted vector
```cpp
ip = std::unique(v.begin(), v.begin() + 12);
v.resize(std::distance(v.begin(), ip));
```
```cpp
// Defining the BinaryFunction
bool Pred(char a, char b){
    // Checking if both the arguments are same and equal
    // to 'G' then only they are considered same
    // and duplicates are removed
    if (a == b && a == 'G') {
        return 1;
    } else {
        return 0;
    }
}
int main(){
    string s = "You arre vvvisiting GGGGFGGGG";
    auto ip = std::unique(s.begin(), s.end(), Pred);
  
    cout << string(s.begin(), ip);
    // prints You arre vvvisiting GFG
}
```
```cpp
count = std::distance(v.begin(),std::unique(v.begin(), v.end()));
cout << "Total no. of unique elements = " << count;
```

### vector::resize()
The function alters the container’s content in actual by inserting or deleting the elements from it. It happens so,

+ If the given value of n is less than the size at present then extra elements are demolished.
+ If n is more than current size of container then upcoming elements are appended at the end of the vector.

>
    vectorname.resize(int n, int val)
+ n - it is new container size, expressed in number of elements.
+ val - if this parameter is specified then new elements are initialized with this value.
+ no return value

### next_permutation(first_iterator, last_iterator)
This modified the vector to its next permutation.

### prev_permutation(first_iterator, last_iterator)
This modified the vector to its previous permutation. 

### distance(first_iterator,desired_position)
It returns the distance of desired position from the first iterator.This function is very useful while finding the index. 

```cpp
cout << "Max element at index : ";
cout << distance(vect.begin(), max_element(vect.begin(), vect.end()));
```
### bool all_of (InputIterator first, InputIterator last, UnaryPredicate pred);
```cpp
if (std::all_of(v.cbegin(), v.cend(), [](int i){ return i % 2 == 0; })) 
    std::cout << "All numbers are even\n";
```

- **any_of**
- **none_of**

### copy_n
```cpp
    int ar[6] =  {1, 2, 3, 4, 5, 6};
    int ar1[6];
    copy_n(ar, 6, ar1);
```
### iota
This function is used to assign continuous values to array. This function accepts 3 arguments, the array name, size, and the starting number.
```cpp
int ar[6] =  {0};
iota(ar, ar+6, 20);
// 20 21 22 23 24 25
```

### for_each
```cpp
// helper function 1
void printx2(int a)
{
    cout << a * 2 << " ";
}
 
// helper function 2
// object type function
struct Class2
{
    void operator() (int a)
    {
        cout << a * 3 << " ";
    }
} ob1;
```
```cpp
for_each(vect.begin(), vect.end(), printx2);
for_each(arr1, arr1+6, ob1);
```

### Using Lambdas
With the introduction of lambda functions, one can easily used to make the whole thing inline which is very compact and useful for people looking for using functional programming.

```cpp
for_each(vec.begin(), vec.end(), [](int a) { cout << a << " " << endl; });
```
### InputIterator find (InputIterator first, InputIterator last, const T& val)
```cpp
// Element to be searched
int ser = 30;
it = std::find (vec.begin(), vec.end(), ser);

if (it != vec.end())

index = it - vec.begin();
```
### find_if
Returns an iterator to the first element in the range [first, last) for which pred(Unary Function) returns true. If no such element is found, the function returns last.

> 
    InputIterator find_if (InputIterator first, InputIterator last, UnaryPredicate pred);

### find_if_not

Returns an iterator to the first element in the range [first, last) for which pred(Unary Function) returns false.

### find_end
- It is the reverse variant of **std::search.**
- You are not alone if you are thinking why it is called **std::find_end** and not **std::search_end**

>  
    ForwardIterator1 find_end (ForwardIterator1 first1, ForwardIterator1 last1, ForwardIterator2 first2, ForwardIterator2 last2, BinaryPredicate pred);

+ **first1:** Forward iterator to the first element in the first range.
+ **last1:** Forward iterator to the last element in the first range.
+ **first2:** Forward iterator to the first element in the second range.
+ **last2:** Forward iterator to the last element in the second range.
+ **pred:** by default it is ==. Binary function that accepts two elements as arguments (one of each of the two sequences, in the same order), and returns a value convertible to bool. The value returned indicates whether the elements are considered to match in the context of this function.

**Return Value:** It returns an iterator to the first element of 
the last occurrence of [first2,last2) in [first1,last1).
If the sequence is not found or [first2,last2) is empty,
the function returns last1.

### std::find_first_of 
is used to compare elements between two containers. It compares all the elements in a range [first1,last1) with the elements in the range [first2,last2), and if any of the elements present in the second range is found in the first one , then it returns an iterator to that element.

> 
    ForwardIterator1 find_first_of (ForwardIterator1 first1, 
                                   ForwardIterator1 last1,
                                   ForwardIterator2 first2, 
                                   ForwardIterator2 last2,
                                   BinaryPredicate pred);

+ One possible application of this is to find the first vowel in a sentence

```cpp
// Defining first container
string s1 = "You are reading about std::find_first_of";
  
// Defining second container containing list of vowels
string s2 = {'a', 'A', 'e', 'E', 'i', 'I', 'o', 'O', 'u', 'U'};
      
// Using std::find_first_of to find first occurrence of a vowel
auto ip = std::find_first_of(s1.begin(),s1.end(),s2.begin(),s2.end());
cout << "First vowel found at index "<< (ip - s1.begin()) 

// to find next vowel, i.e 2nd vowel
auto ip2 = std::find_first_of(ip,s1.end(),s2.begin(),s2.end());
```
+ **Time Complexity: O(n1 * n2)**, where, n1 is the number of elements in the first range and n2 is the number of elements in the second range.


### std::greater
is a functional object which is used for performing comparisons. It is defined as a Function object class for the greater-than inequality comparison.

> 
    template <class T> struct greater;

#### Member types:
+ result_type bool
+ first_argument_type T
+ second_argument_type T
These member types are obtained via publicly inheriting std::binary_function<T, T, bool>.

#### Member functions:
+ **operator()** - checks whether the first argument is greater than the second
+ it returns lhs > rhs.

> 
    std::less, std::greater, std::less_equal, and std::greater_equal

### std::adjacent_find

> 
    ForwardIt adjacent_find( ForwardIt first, ForwardIt last, BinaryPredicate p );
+ **first, last :** the range of elements to examine
+ **p :**  binary predicate which returns true if the elements should be treated as equal. 

+ **Return value :** An iterator to the first of the first pair of identical elements, that is, the first iterator it such that *it == *(it+1) for the first version with no pred function or p(*it, *(it + 1)) == true for the second version with BinaryPredicate.
+ If no such elements are found, **last** is returned.

### std::count() 
returns number of occurrences of an element in a given range. Returns the number of elements in the range [first,last) that compare equal to val.
>
    int count(Iterator first, Iterator last, T &val)
**Complexity** It’s order of complexity O(n). Compares once each element with the particular value.

### std::count_if() 
>
    template <class InputT, class UnaryPredicate>
    typename iterator_traits <InputT> :: difference_type
    count_if(InputT first, InputT last, UnaryPredicate p);

+ type of the predicate should be same as the type of the container. 

### std::mismatch()
>
    mismatch( start_iter1, end_iter1, start_iter2 ) 
This version of mismatch only test for inequality.
Here, there are 3 arguments,

**start_iter1:** Beginning iterator to 1st container

**end_iter1:** Last iterator to 1st container

**start_iter2:** Starting iterator to the 2nd iterator from where comparison is desired to begin.

This function returns the 1st mismatch pair pointer, first element pointing to position of first mismatch element of 1st container, second element pointing to position of first mismatch element of 2nd container. If no mismatch is found, 1st element points to position after last element of 1st container and 2nd points to corresponding position in 2nd container

```cpp
pair< vector<int>::iterator, vector<int>::iterator > mispair;

mispair = mismatch(v1.begin(), v1.end(), v2.begin());

cout << "The 1st mismatch element of 1st container : ";
cout << *mispair.first << endl;
```

>
    mismatch( start_iter1, end_iter1, start_iter2, comparator)

+ returns first pair where comparator returns false, i.e a mismatch

### std::equal() 
helps to compares the elements within the range [first_1,last_1) with those within range beginning at first_2.
>
    template bool equal (InputIterator1 first1, InputIterator1 last1, InputIterator2 first2)

>
    template bool equal (InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, BinaryPredicate pred);

+ returns true if pred is true for all pair of elements

>
    template  constexpr const T& max (const T& a, const T& b);

### is_permutation
> 
    template <class ForwardIterator1, class ForwardIterator2 >
    bool is_permutation(ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2);

**true :** if all the elements in range [first1, last1) 
compare equal to those of the range
starting at first2 in any order.

**false :** Any element missing or exceeding.

+ Check whether two strings are anagram of each other

>
    // (since C++14)
    template< class ForwardIt1, class ForwardIt2, class BinaryPredicate >
    bool is_permutation( ForwardIt1 first1, ForwardIt1 last1,
    ForwardIt2 first2, ForwardIt2 last2, BinaryPredicate p );

**Complexity**
At most O
(
N^2
)
 applications of the predicate, or exactly 
N
 if the sequences are already equal, where 
N
 is std::distance(first1, last1).

### search_n
>
    ForwardIterator search_n (ForwardIterator first, ForwardIterator last, Size count, const T& val);

+ **first:** Forward iterator to beginning of the container to be searched into.

+ **last:** Forward iterator to end of the container to be searched into.

+ **count:** Minimum number of successive elements to match. Size shall be (convertible to) an integral type.

+ **val:** Individual value to be compared.

+ **Returns:**  It returns an iterator to the first element of the sequence.

* If no such sequence is found, the function returns **last**.

> 
    ForwardIterator search_n ( ForwardIterator first, ForwardIterator last, Size count, const T& val, BinaryPredicate pred );

**pred:** **Binary function** that accepts two arguments 
(one element from the sequence as first, and val as second), and returns a value convertible to bool. The value returned indicates whether 
the element is considered a match in the context of this function.

## copy

### copy(strt_iter1, end_iter1, strt_iter2) 
- **strt_iter1 :** The pointer to the beginning of the source container, from where elements have to be started copying.
- **end_iter1 :** The pointer to the end of source container, till where elements have to be copied.
- **strt_iter2 :** The pointer to the beginning of destination container, to where elements have to be started copying.
```cpp
// to copy 1st 3 elements
copy(v1.begin(), v1.begin()+3, v2.begin());
```
### copy_n(strt_iter1, num, strt_iter2)
- **num :** Integer specifying how many numbers would be copied to destination container starting from strt_iter1. If a negative number is entered, no operation is performed.
```cpp
// to copy 1st 4 elements
copy_n(v1.begin(), 4, v3.begin());
```
- ensure vector2 (where vector1 is being copied to) of greater or equal size.
- If not, then locations after that will be replaced

### copy_if(): 
As the name suggests, this function copies according to the result of a “condition“.This is provided with the help of a 4th argument, a function returning a boolean value. 
This function takes 4 arguments, 3 of them similar to copy() and an additional function, which when returns true, a number is copied, else number is not copied.

```cpp
//to copy odd elements
copy_if(v1.begin(), v1.end(), v2.begin(), [](int i){return i%2!=0;});
```
### copy_backward(): 
This function starts copying elements into the destination container from backward and keeps on copying till all numbers are not copied. The copying starts from the “strt_iter2” but in the backward direction.
```cpp
// v2[v2_end-1] = v1[v1_end-1];
// v2[v2_end-2] = v1[v1_end-2];
// ...........................
// v2[v2_end_n] = v1[v1_begin];

// n = v1_end - v1_start
copy_backward(v1.begin(), v1.end(), v2.end());

// same as below if both vectors are of same size
copy(v1.begin(), v1.end(), v2.begin());
// if different size
copy_backward(v1.begin(), v1.end(), v2.end()-v1.size() );
```
### Copy using inserter()

```cpp
vector<int> v1 = {1, 5, 7, 3, 8, 3};
vector<int>::iterator itr;
vector<int> v2;

copy(v1.begin(), v1.end(), inserter(v2, itr));
```

### std :: move
+ Moves the elements in the range [first,last) into the range beginning at result.
+ The value of the elements in the [first,last) is transferred to the elements pointed by result. After the call, the elements in the range [first,last] are left in an unspecified but valid state.

>
    OutputIterator move (InputIterator first, InputIterator last, OutputIterator result);

+ **first, last** 
Input iterators to the initial and final positions in a sequence
to be moved. The range used is [first,last], which contains all
the elements between first and last, including the element pointed
by first but not the element pointed by last.

+ **result**
Output iterator to the initial position in the destination sequence.
This shall **not point** to any element in the range [first,last].

+ **Return type**
An iterator to the end of the destination range where elements have been moved.

### std::move_backward

+ Moves the elements in the range [first,last] starting from the end into the range terminating at result.
+ The function begins by moving *(last-1) into *(result-1), and then follows backward by the elements preceding these, until first is reached (and including it).

>
    BidirectionalIterator2 move_backward (BidirectionalIterator1 first, BidirectionalIterator1 last, BidirectionalIterator2 result);

+ **result**
Bidirectional iterator to the past-the-end position in the destination sequence.
This shall **not point** to any element in the range [first,last].

+ **Return Type :**
An iterator to the first element of the destination sequence where elements
have been moved.

### swap()
+ **Parameters:** The function accepts two mandatory parameters a and b which are to be swapped. The parameters can be of any data type.
+ **Return Value:** The function does not return anything, it swaps the values of the two variables.

```cpp
int a = 10;
int b = 20;
swap(a, b);
```
```cpp
string a = "Geeks";
string b = "function";
swap(a, b);
```

### swap_ranges
+ It simply exchanges the values of each of the elements in the range [first1, last1) with those of their respective elements in the range beginning at first2. 
+ If we look at its internal working, we will find that this function itself uses std::swap()
>
    swap_ranges (ForwardIterator1 first1, ForwardIterator1 last1, ForwardIterator2 first2);

+ **Returns:** It returns an iterator to the last element swapped in the second sequence.

### iter_swap
+ std::swap is used for swapping of elements between two containers.
+ One of the other way of doing this same thing is facilitated by std::iter_swap, which as the name suggests is used for swapping the elements with the help of an iterator.
+ It simply exchanges the values of the elements pointed to by the iterators.
+ If we look at its internal working, we will find that this function itself uses std::swap().

>
    void iter_swap (ForwardIterator1 a, ForwardIterator2 b);
```cpp
i1 = v1.begin();
i2 = v1.begin() + 5;
    
std::iter_swap(i1, i2);
```

### std::replace

+ Assigns new_value to all the elements in the range [first, last) that compare to old_value.
+ The function use operator == to compare the individual elements to old_value 
>
    void replace (ForwardIterator first, ForwardIterator last, const T& old_value, const T& new_value)

+ **first, last :** Forward iterators to the initial and final positions
in a sequence of elements.
+ **old_value :** Value to be replaced.
+ **new_value :** Replacement value.

### std::replace_if
>
    void replace_if (ForwardIterator first, ForwardIterator last,
    UnaryPredicate pred, const T& new_value)

+ **pred :** Unary function that accepts an element in the range as argument, and returns a value convertible to bool.The returned value indicate whether the element is to be replaced (if true, it is replaced). The function shall not modify its argument.

```cpp
replace_if(arr, arr + n, IsOdd, new_val);
```
### replace_copy()

>
    template <class InputIterator, class OutputIterator, class T>
    OutputIterator replace_copy (InputIterator first, InputIterator last, OutputIterator result, const T& old_value, const T& new_value); 

+ **first, last :** Input iterators to the initial and final positions in a sequence. 
+ **old_value :** Value to be replaced.
+ **new_value :** Replacement value.
+ **Returns** the position after the last copied element in the destination range (the first element that is not overwritten). 

### replace_copy_if()
>
    Template <class InputIterator, class OutputIterator, class UnaryPredicate, class T>
    OutputIterator replace_copy_if (InputIterator first, InputIterator last, OutputIterator result, UnaryPredicate pred, const T& new_value);

Both algorithms i.e. replace_copy and replace_copy_if, returns the position after the last copied element in the destination range (the first element that is not overwritten).

### fill()
It assigns the value ‘val’ to all the elements in the range **[begin, end)**
```cpp
vector<int> vect(8);
fill(vect.begin() + 2, vect.end() - 1, 4);

// 0 0 4 4 4 4 4 0
```
### fill_n() 
In fill_n(), we specify beginning position, number of elements to be filled and values to be filled.
>
    fill_n (OutputIterator first, Size n, const T& val);

### generate()
>
    void generate (ForwardIterator first, ForwardIterator last, Generator gen);

+ **first:** Forward iterator pointing to the first element of the container.
+ **last:** Forward iterator pointing to the last element of the container.
+ **gen**: A generator function, based upon which values will be assigned.
+ **Returns:** None

```cpp
int gen()
{
    static int i = 0;
    return ++i;
}

std::generate(v1.begin(), v1.end(), gen);
```

### generate_n()
>
    OutputIterator generate_n (OutputIterator first, Size n, Generator gen);

### std :: remove

+ It removes value from range, i.e. Transforms the range [first,last) into a range with all the elements that compare equal to val removed, and returns an iterator to the new end of that range. 
+ The function cannot alter the properties of the object containing the range of elements (i.e., it cannot alter the size of an array or a container).
+ The relative order of the elements not removed is preserved, while the elements between the returned iterator and last are left in a valid but unspecified state.

>
    ForwardIterator remove  (ForwardIterator first, ForwardIterator last, const T& val)

+ **first,last :** The range used is [first,last), which contains all the elements between first and last, including the element pointed by first but not the element pointed by last.
+ **val :** Value to be removed.
+ **Returns :** An iterator to the element that follows the last element not removed.

```cpp
vector<int>::iterator new_end;
new_end = remove(vec1.begin(), vec1.end(), 20);
```
### std :: remove_if
>
    ForwardIterator remove_if (ForwardIterator first, ForwardIterator last, UnaryPredicate pred);

### remove_copy()
+ It copies the elements in the range [first, last) to the range beginning at result, except those elements that compare equal to given elements.
+ The resulting range is shorter than [first,last) by as many elements as matches in the sequence, which are removed.
+ Returns end in copied container.
>
    ResultIterator remove_copy(ForwardIterator first, ForwardIterator last, ResultIterator result ,const T& ele);

### remove_copy_if()
>  
    ResultIterator remove_copy_if(ForwardIterator first, ForwardIterator last, ResultIterator result, UnaryPredicate pred);

### std::unique
+ It is used to remove duplicates of any element present consecutively in a range[first, last). It performs this task for all the sub-groups present in the range having the same element present consecutively.
+ It does not delete all the duplicate elements, but it removes duplicacy by just replacing those elements by the next element present in the sequence which is not duplicate to the current element being replaced. All the elements which are replaced are left in an unspecified state.
+ Another interesting feature of this function is that it does not changes the size of the container after deleting the elements, it just returns a pointer pointing to the new end of the container, and based upon that we have to resize the container, or remove the garbage elements.

> 
    ForwardIterator unique (ForwardIterator first, ForwardIterator last);

+ **first:** Forward iterator to the first element in the container.
+ **last:** forward iterator to the last element in the container.
+ **Return Value:** It returns an iterator to the element that follows the last element not removed.

**It only removes repeated duplicates**
1,1,2,2,1,1,1 -> 1,2,1,$,$,$,$

> 
    ForwardIterator unique (ForwardIterator first, ForwardIterator last, BinaryPredicate Pred);

### std::unique_copy()
what if we don’t want to alter with the original range and just want the result of std::unique to be copied into another container, for this we have another function defined in std::unique_copy().

>
    OutputIterator unique_copy (InputIterator first, InputIterator last, OutputIterator result);

**Return Value:** An iterator pointing to the end of the copied range, which contains no consecutive duplicates.

>
    OutputIterator unique_copy (InputIterator first, InputIterator last, OutputIterator result, BinaryPredicate pred);

### std::reverse()
+ It reverses the order of the elements in the range [first, last) of any container.
+ The time complexity is O(n). 

>
    void reverse(BidirectionalIterator first, BidirectionalIterator last)

### std::reverse_copy())
>
    reverse_copy(src, src + n, dest.begin());

### rotate()
>
    void rotate(ForwardIterator first, ForwardIterator middle, ForwardIterator last)
+ **first, last :** Forward Iterators to the initial and final positions of the sequence to be rotated
+ **middle :** Forward Iterator pointing to the element within the range [first, last) that is moved to the first position in the range.i.e, left rotate.

#### Types of Rotations

+ **Left Rotation:** To rotate left, we need to add the vector index. For example, you have to rotate the vector left 3 times. The 3rd index of the vector becomes the first element. vec.begin() + 3 will rotate vector 3 times left.
+ **Right Rotation:** To rotate right, we need to subtract the vector index. For example, you have to rotate the vector right 3 times. The 3th last index of the vector becomes the first element. vec.begin()+vec.size()-3 will rotate vector 3 times right.

```cpp
// Rotate vector left 3 times.
int rotL=3;
rotate(vec1.begin(), vec1.begin()+rotL, vec1.end());

// Rotate vector right 4 times.
int rotR = 4;
rotate(vec2.begin(), vec2.begin()+vec2.size()-rotR, vec2.end());
```

```cpp
rotate_copy(arr, arr + 3, arr + 7, copy.begin());
```

###  shuffle() and random_shuffle()
**shuffle**
+ This method rearranges the elements in the range [first, last) randomly, using g as a uniform random number generator.
+ It swaps the value of each element with that of some other randomly picked element.
+ It determines the element picked by calling g().

```
template 
  void shuffle (RandomAccessIterator first, 
                RandomAccessIterator last, 
                URNG&& g)
{
  for (auto i=(last-first)-1; i>0; --i) {
    std::uniform_int_distribution d(0, i);
    swap (arr[i], arr[d(g)]);
  }
}
```

```cpp
void shuffle_array(int arr[], int n){
    // To obtain a time-based seed
    unsigned seed = 0;
    shuffle(arr, arr + n, default_random_engine(seed));
}
```

**random_shuffle**

+ This function randomly rearranges elements in the range [first, last).
+ When provided, the function gen determines which element is picked in every case.
+ Otherwise, the function uses some unspecified source of randomness.

```cpp
// Shuffling our array using random_shuffle
random_shuffle(arr, arr + n);
```

**Which is better?**
+ shuffle introduced after C11++, uses functions which are better than rand() which random_shuffle uses.
+ shuffle is an improvement over random_shuffle, and we should prefer using the former for better results.
+ If we don’t pass our random generating function in random_shuffle then it uses its unspecified random values due to which all successive values are correlated.

### std::is_partitioned 
+ It is used for finding whether the range[first, last) is partitioned or not.
+ A range is said to be partitioned with respect to a condition if all the elements for which the condition evaluates to true precede those for which it is false.

>
    bool is_partitioned (InputIterator first, InputIterator last, UnaryPredicate pred);

+ **first:** Input iterator to the first element in the range.
+ **last:** Input iterator to the last element in the range.
+ **pred:** Unary function that accepts an element in the range as argument, and returns a value convertible to bool. The value returned indicates whether the element belongs to the first group (if true, the element is expected before all the elements for which it returns false). The function shall not modify its argument. This can either be a function pointer or a function object.
+ **Returns:** It returns true if all the elements in the range [first, last) for which pred returns true precede those for which it returns false. Otherwise it returns false. If the range is empty, the function returns true.

```cpp
bool pred(int a)
{
    return (a % 3 == 0);
}

vector<int> v1 = { 3, 6, 9, 10, 11, 13 };
bool b1 = std::is_partitioned(v1.begin(), v1.end(), pred);

vector<int> v2 = { 3, 6, 9, 10, 11, 13, 3 };
bool b2 = std::is_partitioned(v2.begin(), v2.end(), pred);

// b1 - > true
// b2 - > false
```

### partition(beg, end, condition)
This function is used to partition the elements on basis of condition mentioned in its arguments.

### stable_partition(beg, end, condition)
This function is used to partition the elements on basis of condition mentioned in its arguments in such a way that the relative order of the elements is preserved..
### partition_point(beg, end, condition)
This function returns an iterator pointing to the partition point of container i.e. the first element in the partitioned range [beg,end) for which condition is not true. The container should already be partitioned for this function to work.

### partition_copy(beg, end, beg1, beg2, condition)
+ This function copies the partitioned elements in the different containers mentioned in its arguments.
+ It takes 5 arguments.
+ Beginning and ending position of container, 
+ beginning position of new container where elements have to be copied (elements returning true for condition),
+ beginning position of new container where other elements have to be copied (elements returning false for condition)
+ and the condition.
+ Resizing new containers is necessary for this function.

```cpp
vector<int> vect = { 2, 1, 5, 6, 8, 7 };
vector<int> vect1, vect2;
    
// Resizing vectors to suitable size using count_if() and resize()
int n = count_if (vect.begin(), vect.end(), pred);
vect1.resize(n);
vect2.resize(vect.size()-n);
    
partition_copy(vect.begin(), vect.end(), vect1.begin(), vect2.begin(), pred);
```
### sort comp in c style
>
    int comparator(const void* p1, const void* p2);
Return value meaning
>
    less than 0 (<0) The element pointed by p1 goes before the element pointed by p2
    equal to 0  The element pointed by p1 is equivalent to the element pointed by p2
    greater than 0 (>0) The element pointed by p1 goes after the element pointed by p2

### stable_sort()
- It is like std::sort, but stable_sort() keeps the relative order of elements with equivalent values. 

>
    template< class RandomIterator>
    void stable_sort( RandomIterator first, RandomIterator last );

>
    template< class RandomIterator, class Compare>
    void stable_sort( RandomIterator first, RandomIterator last, Compare comp );

- **comp:** predicate function that accepts two arguments and returns true if the **two arguments are in order** and false otherwise.

- stable_sort() function usually uses **mergesort** unlike sort() which uses introsort.

**Time complexity**
+ **O(n*log^2(n))** - If additional memory linearly proportional to length is not available.
+ **O(n*log(n))** - If its available

### std::partial_sort
- is used for sorting not the entire range, but only a sub-part of it.
- It rearranges the elements in the range [first, last), in such a way that the elements before middle are sorted in ascending order, whereas the elements after middle are left without any specific order.
>
    void partial_sort (RandomAccessIterator first, RandomAccessIterator middle, RandomAccessIterator last);

+ **middle:** Random-Access iterator pointing to the element in the range [first, last), that is used as the upper boundary for the elements to be sorted.
>
    void partial_sort (RandomAccessIterator first, RandomAccessIterator middle, RandomAccessIterator last, Compare comp);
+ It is sorts in range **[first,middle)**
+ The complexity of partial_sort() is **O(N*log K)** where N is the number of elements in array and K is the number of elements between middle and start

#### Pseudocode
```
//ascending order first k elements
k = middle - start;
Take first k elements.

// O(k)
make_heap(start,start+k);
// max heap

// loop N-K times
for(i=k;i<end;++i){
    
    // O(log k)
    if(arr[i]<heap.top()){
        heap.pop();
        heap.add(arr[i]);
    }
    else{
        //nothing
        // O(1)
    }
}

// heap contains k smallest numbers
// so pop 
```
+ O(N-K) . log(k)
+ O(N log k)
+ In best case, O(k) for make heap, O(N-k) for loop. So O(N)

### nth_element()
+ It rearranges the list in such a way such that the element at the nth position is the one which should be at that position if we sort the list.
+ It does not sort the list, just that all the elements, which precede the nth element are not greater than it, and all the elements which succeed it are not less than it.

```cpp
// Using nth_element with n as 5
nth_element(v, v + 4, v + 8);
```
+ The specified middle position will contain the correct element.
+ So to find 5th element, give 5th address, which is begin()+4.

### std::partial_sort_copy
>
    RandomAccessIterator partial_sort_copy (InputIterator first, InputIterator last, RandomAccessIterator result_first, RandomAccessIterator result_last);

+ **first:** Input iterator to the first element in the container.
+ **last:** Input iterator to the last element in the container.
+ **result_first:** Random-Access iterator pointing to the initial position in the destination container.
+ **result_last:** Random-Access iterator pointing to the final position in the destination container.
+ **Return Value:** It returns an iterator pointing to the element that follows the last element written in the result sequence.
+ number of elements, i.e. k = result_last - result_first;
+ so size of copying container. 
+ given v_copy.begin(), v_copy.end() as 3rd and 4th parameter.

>
    RandomAccessIterator partial_sort_copy (InputIterator first, InputIterator last, RandomAccessIterator result_first, RandomAccessIterator result_last, Compare comp);

>
    bool is_sorted (ForwardIt first, ForwardIt last, Compare comp);

### is_sorted_until
>
    ForwardIterator is_sorted_until (ForwardIterator first, ForwardIterator last);

+ **first:** Forward iterator to the first element in the list.
+ **last:** forward iterator to the last element in the list.
+ **Return Value:** It returns an iterator to the first unsorted element in the list.
+ It returns last in case if there is only one element in the list or if all the elements are sorted.

### More on nth_element
>
    void nth_element (RandomAccessIterator first, RandomAccessIterator nth, RandomAccessIterator last);

+ **nth:** Random-access iterator pointing to the position in the list, which should be sorted.
+ If it points to end, then this function will do nothing.
#### Applications
+ It can be used if we want to find the first n smallest numbers, but they may or maynot be ordered.
+ It can be used to find the median of the elements given.

### More on lower_bound
+ It is enough that the container is partitioned on searching value.

### equal_range
+ This function requires the range to be either sorted or partitioned according to some condition such that all the elements for which the condition evaluates to true are to the left of the given value and rest all are to its right.
+ It returns the initial and the final bound of such a sub-range.
>
    Template
    pair equal_range (ForwardIterator first, ForwardIterator last, const T& val);

**Return Value:**
+ It returns a pair object, whose member **pair::first** is an iterator to the lower bound of the subrange of equivalent values,
+ and **pair::second** its upper bound.
+ If there is no element equivalent to val, then both first and second points to the nearest element greater than val,
+ or if val is greater than any other value, then both of them point to last.
+ This function can be used if we want to use both **std::lower_bound** and **std::upper_bound** at the same time, as its first pointer will be same as std::lower_bound and its second pointer will be same as std::upper_bound.

```cpp
std::pair<std::vector<int>::iterator, 
std::vector<int>::iterator> ip;
```

>
    pair 
    equal_range (ForwardIterator first, ForwardIterator last, const T& val, Compare comp);

+ if container is sorted or partitioned based on comp, then pass comp as it will perform binary search using comp to find val.

### binary_search
>
    bool binary_search(startaddress, endaddress, valuetofind)
### merge()
>
    template 
    outiter merge (initer1 beg1, initer1 end1,
    initer2 beg2, initer2 end2,
    outiter res)

+ **beg1 :**  Input iterator to initial position of first sequence.
+ **end1 :**  Input iterator to final position of first sequence.
+ **beg2 :**  Input iterator to initial position of second sequence.
+ **end2 :**  Input iterator to final position of second sequence.
+ **res :** Output Iterator to initial position of resultant container.
+ **Return value :** Iterator past the last element of the resulting container.

>
    template 
    outiter merge (initer1 beg1, initer1 end1,
                        initer2 beg2, initer2 end2,
                        outiter res, Compare comp)

+ if the 2 containers are sorted based on comp, pass comp as last parameter.

### includes(beg1, end1, beg2, end2)
+ This function is used to check whether one sorted container elements are including other sorted container elements or not.
+ Returns true if 1st container includes 2nd container else returns false.

```
container 1 = 1 2 4 5 6 8
container 2 = 1 4 5
container 3 = 9 10

includes(beg1, end1, beg2, end2) -> true
includes(beg1, end1, beg3, end3) -> false
```

### inplace_merge(beg1, beg2, end)
+ This function is used to sort two consecutively placed sorted ranges in a single container.
+ It takes 3 arguments, iterator to beginning of 1st sorted range, iterator to beginning of 2nd sorted range, and iterator to last position.

```cpp
vector<int> v1 = {1, 3, 4, 5, 20, 30};
vector<int> v2 = {1, 5, 6, 7, 25, 30};
    
vector<int> v3(12);

// using copy to copy both vectors into one container
auto it = copy(v1.begin(), v1.end(), v3.begin());
copy(v2.begin(), v2.end(), it);

inplace_merge(v3.begin(),it,v3.end());
```
### set_union(beg1, end1, beg2, end2, beg3) 
+ This function computes the set union of two containers and stores in new container.
+ It returns the iterator to the last element of resultant container.
+ The containers should be sorted and it is necessary that new container is resized to suitable size.

### set_intersection(beg1, end1, beg2, end2, beg3)
```cpp
auto it = set_intersection(v1.begin(), v1.end(), v2.begin(), v2.end(), v3.begin());
     
v3.resize(it - v3.begin());
```

### set_difference(beg1, end1, beg2, end2, beg3)
### set_symmetric_difference(beg1, end1, beg2, end2, beg3)

### lexicographical_compare
>
    template 
    bool lexicographical_compare(iter1 beg1, iter1 end1, iter2 beg2, iter2 end2)
 
+ **beg1 :**  Input iterator to initial position of first sequence.
+ **end1 :**  Input iterator to final position of first sequence.
+ **beg2 :**  Input iterator to initial position of second sequence.
+ **end2 :**  Input iterator to final position of second sequence.
+ **Returns** True, if range1 is strictly lexicographically smaller than range2 else returns a false.

>
    lexicographical_compare(iter1 beg1, iter1 end1, iter2 beg2, iter2 end2, Compare comp)
```cpp
// for case insensitive
bool comp (char s1, char s2)
{
    return tolower(s1)<tolower(s2);
}
```
### next_permutation and prev_permutation
>
    template 
    bool next_permutation (BidirectionalIterator first,
                       BidirectionalIterator last);

+ **first, last :** Bidirectional iterators to the initial and final positions of the sequence. The range used is [first, last), which contains all the elements between first and last, including the element pointed by first but not the element pointed by last.

+ **returns** true if the function could rearrange the object as a lexicographically greater permutation.
+ Otherwise, the function returns false to indicate that the arrangement is not greater than the previous, but the lowest possible (sorted in ascending order).

>
    template 
    bool prev_permutation (BidirectionalIterator first,
                         BidirectionalIterator last );
                
+ **returns** true if the function could rearrange the object as a lexicographically smaller permutation.
+ Otherwise, the function returns false to indicate that the arrangement is not less than the previous, but the largest possible (sorted in descending order).