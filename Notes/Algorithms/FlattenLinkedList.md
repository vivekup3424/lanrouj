## Problem Statement
Given a linked list of node which are sorted in increasing order of their value, where every node itself is a linked list which is also sorted in increasing order of their value

We want a flattened  linked list that is to merge all the linked lists in a singular linked list where the elements are in sorted order.

*Other information about the nodes in the linked list*
(i) a **next** pointer to the next node,  
(ii) a **bottom** pointer to a linked list where this node is head.


### My Approach
```cpp
Node *mergeList(Node *headA, Node *headB){
    auto head = new Node(-1);
    auto temp = head;
    while(headA!=nullptr and headB!=nullptr){
        if(headA->data < headB->data){
            auto newNode = new Node(headA->data);
            temp->bottom = newNode;
            temp = newNode;
            headA = headA->bottom;
        }else{
            auto newNode = new Node(headB->data);
            temp->bottom = newNode;
            temp = newNode;
            headB = headB->bottom;
        }
    }
    if(headA!=nullptr){
        temp->bottom = headA;
    }
    if(headB!=nullptr){
        temp->bottom = headB;
    }
    return head->bottom;
}

Node *mergeKLists(Node *head){
    if(head == nullptr||head->next == nullptr){
        return head;
    }
    head->next = mergeKLists(head->next);
    head = mergeList(head, head->next);
    return head;
}

```

