
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
