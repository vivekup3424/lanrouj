![[Pasted image 20241113174420.png]]

### Implementing Stack Using Queues

There are two main approaches to implement a stack using queues:
1. **Push-Heavy Approach**: Makes the `push` operation costly, while keeping the `pop` operation efficient.
2. **Pop-Heavy Approach**: Keeps the `push` operation efficient, while making the `pop` operation costly.

Each approach uses two queues to simulate the Last-In-First-Out (LIFO) behavior of a stack.

---

### 1. Push-Heavy Approach

In this approach, we maintain two queues, `q1` and `q2`. The main stack elements are always in `q1`. When we push a new element, we make it the front of `q1`.

#### Steps:
1. **Push(x)**:
   - Enqueue `x` to `q2`.
   - Move all elements from `q1` to `q2`.
   - Swap `q1` and `q2`.
   
2. **Pop()**:
   - Simply dequeue from `q1`.

#### Complexity:
- **Time Complexity**:
  - Push: \(O(n)\), where \(n\) is the number of elements in `q1`, since we move all elements to `q2`.
  - Pop: \(O(1)\), as we just dequeue from `q1`.

- **Space Complexity**:
  - \(O(n)\), where \(n\) is the number of elements in the stack.

---

### 2. Pop-Heavy Approach

In this approach, we also use two queues, `q1` and `q2`. The main stack elements are in `q1`, and `q2` is only used temporarily during `pop`.

#### Steps:
1. **Push(x)**:
   - Enqueue `x` to `q1`.

2. **Pop()**:
   - Move all elements from `q1` to `q2`, except for the last element.
   - Dequeue the last element from `q1` (this is the "top" of the stack).
   - Swap `q1` and `q2`.

#### Complexity:
- **Time Complexity**:
  - Push: \(O(1)\), since we directly enqueue to `q1`.
  - Pop: \(O(n)\), where \(n\) is the number of elements in `q1`, as we move all elements except the last to `q2`.

- **Space Complexity**:
  - \(O(n)\), where \(n\) is the number of elements in the stack.

---

### Summary Table

| Approach         | Operation | Time Complexity | Space Complexity |
|------------------|-----------|-----------------|------------------|
| **Push-Heavy**   | Push      | \(O(n)\)        | \(O(n)\)        |
|                  | Pop       | \(O(1)\)        | \(O(n)\)        |
| **Pop-Heavy**    | Push      | \(O(1)\)        | \(O(n)\)        |
|                  | Pop       | \(O(n)\)        | \(O(n)\)        |

