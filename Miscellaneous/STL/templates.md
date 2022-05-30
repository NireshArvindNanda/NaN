# Templates in C++

The idea of templates is to pass data type as a parameter so that we don’t need to write the same code for different data types.
C++ adds two new keywords to support templates: **template** and **typename**. The second keyword can always be replaced by keyword **class**.

## Working of templates

Templates are expanded at compiler time. This is like macros. The difference is, the compiler does type checking before template expansion. The idea is simple, source code contains only function/class, but compiled code may contain multiple copies of same function/class. 

### Generics
Generics is the idea to allow type (Integer, String, … etc and user-defined types) to be a parameter to methods, classes and interfaces.
The method of Generic Programming is implemented to increase the efficiency of the code. Generic Programming enables the programmer to write a general algorithm which will work with all data types. It eliminates the need to create different algorithms if the data type is an integer, string or a character.

The advantages of Generic Programming are
- Code Reusability
- Avoid Function Overloading
- Once written it can be used for multiple times and cases.

### Function Templates
We write a generic function that can be used for different data types.
```cpp
template <typename T> T myMax(T x, T y)
    return (x > y) ? x : y;

```
```cpp
template <class T> void bubbleSort(T a[], int n)
{
    for (int i = 0; i < n - 1; i++)
        for (int j = n - 1; i < j; j--)
            if (a[j] < a[j - 1])
                swap(a[j], a[j - 1]);
}
```
```cpp
myMax<int>(3, 7);
myMax<double>(3.0, 7.0);

int a[5] = { 10, 50, 30, 40, 20 };
int n = sizeof(a) / sizeof(a[0]);
bubbleSort<int>(a, n);
```

### Class Templates
Like function templates, class templates are useful when a class defines something that is independent of the data type. Can be useful for classes like LinkedList, BinaryTree, Stack, Queue, Array, etc.
```cpp
template <typename T> class Array {
private:
    T* ptr;
    int size;
  
public:
    Array(T arr[], int s);
    void print();
};
  
template <typename T> Array<T>::Array(T arr[], int s)
{
    ptr = new T[s];
    size = s;
    for (int i = 0; i < size; i++)
        ptr[i] = arr[i];
}
```
There be more than one arguments and default value to templates 
```cpp
template <class T, class U = char> class A {
    T x;
    U y;
};
```

### What is the difference between function overloading and templates? 
Both function overloading and templates are examples of polymorphism feature of OOP. Function overloading is used when multiple functions do similar operations, templates are used when multiple functions do identical operations.

### Templates and Static variables in C++
##### Function templates and static variables:
Each instantiation of function template has its own copy of local static variables.
```cpp
template <typename T>
void fun(const T& x)
{
  static int i = 10;
  cout << ++i;
  return;
}
```

```cpp
fun<int>(1);  // prints 11
cout << endl;
fun<int>(2);  // prints 12
cout << endl;
fun<double>(1.1); // prints 11
cout << endl;
```
#### Class templates and static variables:
The rule for class templates is same as function templates
Each instantiation of class template has its own copy of member static variables

```cpp
template <class T> class Test
{  
private:
  T val; 
public:
  static int count;
  Test()
  {
    count++;
  }
};

// IMPORTANT
// Static members in a function must be instantiated like this only
// The initialization of the static member must not be in the header file.
// Reason is that putting such an initialization in the header file would
// duplicate the initialization code in every place where the header is included.

template<class T>
int Test<T>::count = 0;
  
int main()
{
  Test<int> a;  // value of count for Test<int> is 1 now
  Test<int> b;  // value of count for Test<int> is 2 now
  Test<double> c;  // value of count for Test<double> is 1 now
  cout << Test<int>::count   << endl;  // prints 2  
  cout << Test<double>::count << endl; //prints 1
}
```
### Template Specialization in C++
It is possible in C++ to get a special behavior for a particular data type. This is called template specialization. 

```cpp
template <class T>
void sort(T arr[], int size)
{
    //generic
}

template <>
void sort<char>(char arr[], int size)
{
    //specific to char
}
```

```cpp
template <class T>
void fun(T a)
{
   cout << "The main template fun(): " << endl;
}
 
template<>
void fun(int a)
{
    cout << "Specialized Template for int type: " << endl;
}
```
```cpp
template <class T>
class Test
{
public:
   //
};
 
template <>
class Test <int>
{
public:
   //
};
```

### How does template specialization work? 
When we write any template based function or class, compiler creates a copy of that function/class whenever compiler sees that being used for a new data type or new set of data types(in case of multiple template arguments). 
If a specialized version is present, compiler first checks with the specialized version and then the main template. Compiler first checks with the most specialized version by matching the passed parameter with the data type(s) specified in a specialized version.

### Template MetaProgramming

```cpp
#include <iostream>
using namespace std;

template<int n> struct funStruct
{
	enum { val = 2*funStruct<n-1>::val };
};

template<> struct funStruct<0>
{
	enum { val = 1 };
};

int main()
{
	cout << funStruct<8>::val << endl;
	return 0;
}
```

calculation is done at compile time. So, it is compiler that calculates 2^8. To understand how compiler does this, let us consider the following facts about templates and enums:
- We can pass nontype parameters (parameters that are not data types) to class/function templates. 
- Like other const expressions, values of enumeration constants are evaluated at compile time. 
- When compiler sees a new argument to a template, compiler creates a new instance of the template.

###  Nontype parameters to template
We can pass non-type arguments to templates. Non-type parameters are mainly used for specifying max or min values or any other constant value for a particular instance of a template. The important thing to note about non-type parameters is, they must be const. The compiler must know the value of non-type parameters at compile time. Because the compiler needs to create functions/classes for a specified non-type value at compile time. In below program, if we replace 10000 with a variable, we get a compiler error.

```cpp
template <class T, int max> int arrMin(T arr[], int n)
{
    int m = max;
    for (int i = 0; i < n; i++)
        if (arr[i] < m)
            m = arr[i];
  
    return m;
}

int arr1[] = { 10, 20, 15, 12 };
int n1 = sizeof(arr1) / sizeof(arr1[0]);
cout << arrMin<int, 10000>(arr1, n1) << endl;
```