- **Problem**: Merge \( k \) sorted linked lists.
- **Solution**: 
	- Use a Min-Heap to keep track of the smallest elements. 
	- Push the first element of each list into the heap. 
	- Continuously extract and push the next element from that list.

```cpp
ListNode* mergeKLists(vector<ListNode*>& lists) {
    auto cmp = [](ListNode* a, ListNode* b) { return a->val > b->val; };
    priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> minHeap(cmp);
    
    for (auto l : lists) {
        if (l) minHeap.push(l);
    }

    ListNode dummy(0), *tail = &dummy;
    while (!minHeap.empty()) {
        tail->next = minHeap.top(); minHeap.pop();
        tail = tail->next;
        if (tail->next) minHeap.push(tail->next);
    }
    return dummy.next;
}
```
