# SRIB Interview Questions

DSA
* Given a string S and string array. I have to return the boolean array if array[i] string is a rotation of string S then array[i] is true otherwise false.
* Given an array that contains a unique integer and integer k. I have to return a count of pairs whose sum is equal to k. solve it by two approaches 1st one is to sort the array and apply a two-pointer and 2nd approach is to use set and apply the find operator.
* Given an array that contains a unique integer and integer k. I have to return the count of pairs whose sum is greater than k.
* Given a 1000 page book, each page has 100 words. I have to return the top 100 words based on a higher frequency of words. ( In this question interviewer Only focus on the data structure I used)

# Technical
## What are virtual functions?
A virtual function (also known as virtual methods) is a member function that is declared within a base class and is re-defined (overridden) by a derived class. When you refer to a derived class object using a pointer or a reference to the base class, you can call a virtual function for that object and execute the derived class's version of the method. Virtual functions ensure that the correct function is called for an object, regardless of the type of reference (or pointer) used for the function call. They are mainly used to achieve Runtime polymorphism. Functions are declared with a virtual keyword in a base class. The resolving of a function call is done at runtime.

### Rules for Virtual Functions 
The rules for the virtual functions in C++ are as follows: 
* Virtual functions cannot be static. 
* A virtual function can be a friend function of another class. 
* Virtual functions should be accessed using a pointer or reference of base class type to achieve runtime polymorphism. The prototype of virtual functions should be the same in the base as well as the derived class. They are always defined in the base class and overridden in a derived class. It is not mandatory for the derived class to override (or re-define the virtual function), in that case, the base class version of the function is used. A class may have a virtual destructor but it cannot have a virtual constructor.
![Alt text](https://media.geeksforgeeks.org/wp-content/uploads/VirtualFunctionInC.png)


## What is a memory leak? How does the OS know about memory leaks? What is a dangling pointer?
A memory leak occurs when programmers create a memory in a heap and forget to delete it. The consequence of the memory leak is that it reduces the performance of the computer by reducing the amount of available memory. Eventually, in the worst case, too much of the available memory may become allocated, all or part of the system or device stops working correctly, the application fails, or the system slows down vastly.

So basically, valgrind provides a virtual processor that executes your application. However, before your application instructions are processed, they are passed to tools (such as memcheck). These tools are kind of like plugins, and they are able to modify your application before it is run on the processor.

Dangling Pointer: When a memory is allocated in stack at runtime for a function call f() and after the function routine is over the stack memory get deallocated so at that point if we have any pointer pointing to that location it will be dangling pointer. 

NOTE: Stack is allocated at runtime; layout of each stack frame, however, is decided at compile time, except for variable-size arrays.

## Explain vtable and v-ptr.
The vTable, or Virtual Table, is a table of function pointers that is created by the compiler to support dynamic polymorphism. Whenever a class contains a virtual function, the compiler creates a Vtable for that class. Each object of the class is then provided with a hidden pointer to this table, known as Vptr. 

The Vtable has one entry for each virtual function accessible by the class. These entries are pointers to the most derived function that the current object should call. 

The virtual pointer or _vptr is a hidden pointer that is added by the compiler as a member of the class to point to the VTable of that class. For every object of a class containing virtual functions, a vptr is added to point to the vTable of that class. It's important to note that vptr is created only if a class has or inherits a virtual function.

* Implement your own sizeof operator in C.
* Difference between null pointer and void pointer.
* Any real-life use case of void pointer.
* Difference between processes and threads.
* How do threads communicate with each other?
* Implement a server socket with all API calls (related to Socket Programming in Java).
* Write the code to find the diameter of a Binary Tree (start with O(n2) and optimize to O(n)).
* Print the diameter of the tree (modification of the previous code).
* Design and implement an LRU Cache (using Linked List and HashMaps for optimization).
* Questions on Networking: NAT, Gateways, Routers, Network vs Transport Layer.
* Client-server architecture.
* L-value and R-value references.
* OOP concepts.
* MFC, COM, DCOM definitions.
* Big endian vs little endian – how to determine a machine's endianness?
* Templates.
* STL.
* Function pointers: how and why?
* Virtual and friend functions and classes: why and how?
* Singleton class: why and how?
* Abstract and pure virtual functions: why and how?
* Constant vs static functions and variables: differences, uses, and what happens behind the scenes.
* Interfaces.
* Namespaces: do they interact? If yes, how? If no, why not?
* *p = NULL; – Is it okay? Why or why not?
* &p = NULL; – Is it okay? Why or why not?
* Scheduling: which data structures to use and why?
* Class diagrams.
* ACID property and its usage.
* Which SDLC model to use for specific scenarios and why?
* Memory segments: heap, stack, data, code.
* Variable memory allocation: static, extern, register, auto, const, etc.
* Size of a class.
* Object of a class in the class declaration: when is it needed?
* Virtual destructor.
* Pointer types: null, smart, wild, void/generic, dangling.

## Diamond problem of inheritance and virtual classes.
The diamond problem is a well-known issue in object-oriented programming, particularly in languages like C++ that support multiple inheritance. It occurs when a class inherits from two classes that have a common base class, creating a diamond-shaped inheritance structure. The problem arises when the common base class has virtual functions, leading to ambiguity in which version of the function should be called.

One way to access the variables in B and C class is by using scope resolution operator.
To solve the diamond problem, use Virtual inheritance. Note that there is a difference between virtual function and virtual inheritance. Virtual inheritance ensures only one instance of the base class is passed when inherited through multiple roots.
While Virtual function is used for runtime polymorphism. It allows overriding base class function in derived class.

## Implement three stacks using one array.
Use an static array of size = 3*stackSize. Also use three pointer that points to the top of the each of stack. Initialize it to -1, stackSize - 1 and 2*(stackSize - 1). 

```cpp
class ThreeStack{
    int capacity;
    int top[3];
    int stackSize;
    int* arr;

    public:
        ThreeStack(int size){
            capacity = 3 * size;
            arr = new int[capacity];
            stackSize = size;
            top[0] = -1;
            top[1] = size - 1;
            top[2] = 2 * size - 1;
        }

        ~ThreeStack(){
            delete[] arr;
        }

        void push(int stackNum, int val){
            if(stackNum <0 || stackNum>2){
                throw out_of_range("Invalid stack number");
            }
           
            if(top[stackNum] >= (stackNum + 1)*(stackSize - 1)){
                throw overflow_error("Stack overflow");
            }

            top[stackNum]++;
            arr[top[stackNum]] = val;
        }

        int pop(int stackNum){
            if(stackNum <0 || stackNum>2){
                throw out_of_range("Invalid stack number");
            }
            if(top[stackNum] < stackNum*stackSize){
                throw underflow_error("stack underflow");
            }
            int value = arr[top[stackNum]];
            top[stackNum]--;
            return value;
        }

        int peek(int stackNum){
            if(stackNum <0 || stackNum>2){
                throw out_of_range("Invalid stack number");
            }
            return arr[top[stackNum]];
        }
        bool isEmpty(int stackNum){
            return top[stackNum] < stackNum * stackSize;
        }
};
```

## Copy constructor and default copy constructor.
A copy constructor is a constructor that initializes objects using another object of the same class. It is also called member-wise constructor. Copy constructor takes a reference to an object of the same class as an argument. In user defined copy constructor you can change ordering of the member copying. 

```cpp
class Base{
public:
    int a;
    int b;
    Base(int a_, int b_){
        a = a_;
        b = b_;
    }
    //copy constructor. Each member is initialized one by one. you can also
    // change the order of initialization
    Base(const Base& bobj){
        a = bobj.b;
        b = bobj.a;
    }
};
int main() {
    Base b1(2, 3);
    Base b2(b1);
    cout<<b2.a<<" "<<b2.b<<endl; //prints 3 2
    return 0;
}
```

Default Copy constructor: If the user does not define any copy constructor, the compiler does it for us. This is the default copy constructor. An implicitly defined copy constructor will copy the bases and members of an object in the same order that a constructor would initialize the bases and members of the object.
The default copy constructor provided by the compiler performs a member-wise copy of the object. This means that:
* For non-pointer data members (e.g., integers, floats, etc.), their values are directly copied.
* For pointer data members, only the pointer's value (address) is copied, not the object it points to.

## Deep copy vs shallow copy.
Creating a copy means to create an exact replica of the object having the same literal value, data type and resources. In shallow copy, only the pointer(references) will be copied, not the actual resources that the pointers are pointing to. This can lead to dangling pointers if the original object is deleted. Also, in shallow copy, any changes made in the original are reflected in the copy. Default copy constructor only does shallow copy.

Deep copy: A deep copy duplicates the entire structure, including any objects or pointers the original object contains. Changes to the original object do not affect the deep copy. This is done using only user defined copy constructors. In a user-defined copy constructor, we make sure that pointers (or references) of copied objects point to new copy of the dynamic resource allocated manually in the copy constructor using new operators. Thus no issue of dangling pointer.

* Runtime error, segmentation fault, compiler error, stack overflow.
* Runtime error:
* Deque.
* Print factorial (coding implementation and execution).
* Difference between Linked List and Array and their applications.
* DFS and BFS.
* Queue vs Stack.
* What is an Operating System?
* What is deadlock and how to prevent it?
* States of a process.
* Semaphore.
* OOP principles: Friend Function, class, and object, constructor and destructor, inheritance, polymorphism, encapsulation, and abstraction.
* Implement Queue using two stacks.
* Given an array of strings, report all strings that are prefixes of some other string in the array (Hint: Use Tries).
* Difference between Machine Learning and Deep Learning.
* Why do convolutional layers work better for image classification compared to fully connected layers?
* Different types of weight initialization techniques.
* Explain dropout and its resemblance to ensemble techniques.
* Explain gradient descent, mini-batch gradient descent, and stochastic gradient descent, and their preferences under different scenarios.
* Why is Adam optimizer often preferred over SGD?
* Dynamic Programming vs Recursion (Why use DP?).
* BFS vs DFS.
* Heap Memory vs Stack Memory.
* ArrayList vs Heap.
* ACID properties in DBMS.
* Basics of Computer Networking (TCP/IP, UDP, etc.).
* What is Dynamic Programming? Why do we use it?
* What's your favorite algorithm?
* How do you allocate and deallocate memory in C?
* Have you ever encountered a segmentation fault in your program?
* Explain Kadane's algorithm for the largest sum contiguous subarray.
* What are dangling pointers, null pointers, and void pointers? Why do we use void pointers, and what are their disadvantages?
* What is Inter-Process Communication (IPC), and what are its types?
* Producer-Consumer problem in process synchronization.
* Coding: Given an array of integers (both odd and even), sort the even numbers in ascending order and the odd numbers in descending order (opposite variant too).
* Find the middle element of a linked list.
* Find the square root of a perfect number.
* Calculate the value of ex using its expansion.
* Solve the puzzle: Measure 45 minutes using two identical wires
* Solve a biquadratic equation and find its real roots.

# Non-technical Questions
* Where do you see yourself in the next 5 years?
* How do I handle the situation if I have multiple tasks to finish at the time.
