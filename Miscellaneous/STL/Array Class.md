# Array class in C++
- The introduction of array class from C++11 has offered a better alternative for C-style arrays.
- The advantages of array class over C-style array are :- 
    + Array classes knows its own size, whereas C-style arrays lack this property. So when passing to functions, we don’t need to pass size of Array as a separate parameter.
    + With C-style array there is more risk of array being decayed into a pointer. Array classes don’t decay into pointers
    + Array classes are generally more efficient, light-weight and reliable than C-style arrays.

## Operations on array
- **at() :-** This function is used to access the elements of array. 
- **get() :-** This function is also used to access the elements of array. This function is not the member of array class but overloaded function from class tuple. 
- **operator[] :-** This is similar to C-style arrays. This method is also used to access array elements.
```cpp
array<int,6> ar = {1, 2, 3, 4, 5, 6};

ar.at(i);

get<0>(ar);
get<1>(ar);
get<2>(ar);

ar[i];
```
- **front() :-** This returns the first element of array. 
- **back() :-** This returns the last element of array.
- **size() :-** It returns the number of elements in array. This is a property that C-style arrays lack. 
- **max_size() :-** It returns the maximum number of elements array can hold i.e, the size with which array is declared. The size() and max_size() return the same value.
- **swap() :-** The swap() swaps all elements of one array with other.
>
    ar.swap(ar1);
- empty() :- This function returns true when the array size is zero else returns false. 
- fill() :- This function is used to fill the entire array with a particular value.
```cpp
array<int,6> ar;
ar.fill(0);
```