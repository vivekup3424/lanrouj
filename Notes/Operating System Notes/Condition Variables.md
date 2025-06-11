**Condition variables** are synchronization primitives in multithreaded programming used to block a thread until a specific condition is met.

### Why Do We Use Condition Variables?
- **Efficient Waiting**: Instead of continuously polling a condition (which can waste CPU resources), condition variables allow threads to **sleep** and be efficiently **woken up** only when the condition is met.
    
- **Coordination**: They enable **coordination** between threads, where one thread produces a result and another consumes it. For example, a thread waiting for a resource can sleep until another thread signals its availability.
    
- **Avoid Busy Waiting**: Condition variables avoid **busy waiting** (constantly checking the condition) by putting threads to sleep until they are notified, saving CPU cycles.

Solution of Producer and Consumer problem using mutex and condition Variables