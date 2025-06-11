
```c++
//implementing stack using linked list

#include <cstdlib>
#include <exception>
#include <iostream>
#include <stdexcept>
class Node{
public:
  int data;
  Node *next;
  Node(int _val):data(_val),next(nullptr){};
};
class Stack{
public:
  Node *top;
  Stack():top(nullptr){} //abusing initializer list
  int pop(){
    //removes element from the stack and returns it
    //NOTE:- error = -1
    try {
    if(top==nullptr){
        throw std::runtime_error("Stack Empty: Can't remove element it (⊙_☉)");
      }
      int data = top->data;
      Node *nextNode = top->next;
      delete top;
      top = nextNode;
      return data;
    } catch (std::exception &e) {
      std::cout<<e.what()<<std::endl;
      return -1;
    }
  }
  void push(int _val){
    Node *newNode = new Node(_val);
    newNode->next = top;
    top = newNode;
  }
  ~Stack(){
    while(top!=nullptr){
      auto nextNode = top->next;
      delete top;
      top = nextNode;
    }
  }
};

```

### Benefits of implementing a stack using a singly linked list include:

****Dynamic memory allocation****: The size of the stack can be increased or decreased dynamically by adding or removing nodes from the linked list, without the need to allocate a fixed amount of memory for the stack upfront.

****Efficient memory usage:**** Since nodes in a singly linked list only have a next pointer and not a prev pointer, they use less memory than nodes in a doubly linked list.

****Easy implementation****: Implementing a stack using a singly linked list is straightforward and can be done using just a few lines of code.

****Versatile****: Singly linked lists can be used to implement other data structures such as queues, linked lists, and trees.

In summary, implementing a stack using a singly linked list is a simple and efficient way to create a dynamic stack data structure in Python.
