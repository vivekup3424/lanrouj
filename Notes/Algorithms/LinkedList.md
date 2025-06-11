Here's a concise version:

1. **Definition**: A linked list is a data structure where each element, called a node, contains data and a pointer to the next node, allowing storage in non-contiguous memory.
![[Pasted image 20241109163615.png]]
2. **Types**:
   - **Singly Linked List**: Each node points to the next node only.
   - **Doubly Linked List**: Nodes have pointers to both next and previous nodes.
   - **Circular Linked List**: The last node points back to the first.

3. **Basic Operations**:
   - **Insertion**: Adding nodes.
   - **Deletion**: Removing nodes.
   - **Traversal**: Accessing each node’s data.

```cpp
class Node{
    Public: // access modifier
    int data; // the data value
    Node* next; // the pointer to the next value
    Public:
    // constructor
    Node (int data1, Node* next1){
        data=data1;  // Initialize data with the provided value
        next=next1;  // Initialize next with the provided
    }
    Node (int data1){
        data=data1;  // Initialize data with the provided value
        next=nullptr;  // Initialize next as null since it's the end of the list

    }
};
int main(){
    vector<int> arr={2,5,8,7};
    Node* y= new Node(arr[0]);
    cout<<y<<'\n'; // returns the memory value
    cout<<y->data<<'\n'; // returns the data stored at that memory point
}
```
> [!OUTPUT]
> 0x11b7f90  
> 2

### **Understanding the difference between Node and pointer to Node***
A **node** refers to **the structure** that contains data and the pointer to the next node. In contrast, Node* ***(Node pointer)** specifically denotes a pointer variable that stores the **address of the Node** it is pointing to.
![[Pasted image 20241109163912.png]]

## Memory Space used by LinkedList

- Since in an array we only storing integers (which are 32 bits in c/c++) so only 4 bytes are required for this.
- But for linked list we storing the data, which is an integer but also a next pointer which has 32-bit if we are on a 32-bit architecture, or 64-bit if we are on a modern computer which are 64-bit.
- 

|                       | 32 Bit System    | 64 Bit System<br> |
| --------------------- | ---------------- | ----------------- |
| Data- Integer         | 32 bit - 4 bytes | 32 bits- 4 bytes  |
| Next- Address Pointer | 32 bit - 4 bytes | 64 bits- 8 bytes  |
| Total                 | 8 bytes          | 12 bytes          |
|                       |                  |                   |


## Problems based on linked list
1. [[CopyListWithRandomPointer]]
2. [[LRU Cache]]
3. 
