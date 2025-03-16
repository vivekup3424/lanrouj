**Problem Statement:** Given a linked list where every node in the linked list contains two pointers:

1. ‘next’ which points to the next node in the list.
2. ‘random’ which points to a random node in the list or ‘null’.

Create a ‘deep copy’ of the given linked list and return it.

My Approach
```cpp
    Node* copyRandomList(Node* head) {
        if (!head) return nullptr;

        unordered_map<Node*, Node*> mp;

        // First pass: create new nodes and map original nodes to new nodes
        Node* current = head;
        while (current) {
            mp[current] = new Node(current->val);
            current = current->next;
        }

        // Second pass: link next and random pointers of new nodes
        current = head;
        while (current) {
            Node* newNode = mp[current];
            newNode->next = mp[current->next];
            newNode->random = mp[current->random];
            current = current->next;
        }

        // Return the head of the copied list
        return mp[head];
    }

```

