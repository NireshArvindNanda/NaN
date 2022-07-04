# Stack in C++ STL
- Stacks are a type of container adaptors with LIFO(Last In First Out) type of working, where a new element is added at one end (top) and an element is removed from that end only.
- Stack uses an encapsulated object of either vector or deque (by default) or list (sequential container class) as its underlying container, providing a specific set of member functions to access its elements.

## Stack Syntax:-
For creating  a stack, we must include the <stack> header file in our code. We then use this syntax to define the std::stack:

>
    template <class Type, class Container = deque<Type> > class stack;
- **Type** is the type of element contained in the std::stack.
- It can be any valid C++ type or even a user-defined type.
- **Container** is the Type of underlying container object.
- **empty() –** Returns whether the stack is empty – Time Complexity : O(1) 
- **size() –** Returns the size of the stack – Time Complexity : O(1) 
- **top() –** Returns a reference to the top most element of the stack – Time Complexity : O(1) 
- **push(g) –** Adds the element ‘g’ at the top of the stack – Time Complexity : O(1) 
- **pop() –** Deletes the top most element of the stack – Time Complexity : O(1) 
- **swap()**
>
    stackname1.swap(stackname2)
- **emplace()**
>
    stackname.emplace(value)

### Difference between stack::emplace() and stack::push() function. 
While push() function inserts a copy of the value or the parameter passed to the function into the container at the top, the emplace() function constructs a new element as the value of the parameter and then adds it to the top of the container. 

### Container adaptors

- Container adaptors provide a different interface for sequential containers. 
    - **stack:** Adapts a container to provide stack (LIFO data structure) (class template).
    - **queue:** Adapts a container to provide queue (FIFO data structure) (class template).
    - **priority_queue:** Adapts a container to provide priority queue (class template). 
