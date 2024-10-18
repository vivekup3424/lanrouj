
Sure! Here are some concise notes on semaphores, along with C++ examples that you can use for your Obsidian notes.

---

# Semaphores

## What is a Semaphore?
A semaphore is a synchronization primitive that is used to control access to a common resource in concurrent programming. It is a signaling mechanism that can be used to manage multiple threads or processes.

### Types of Semaphores
1. **Binary Semaphore**: Can take only two values, 0 and 1. Used for mutual exclusion (similar to a mutex).
2. **Counting Semaphore**: Can take non-negative integer values. Used to manage access to a resource pool.

## Key Operations
- **Wait (P operation)**: Decreases the semaphore value. If the value is greater than zero, the thread proceeds; otherwise, it blocks until the value is greater than zero.
- **Signal (V operation)**: Increases the semaphore value. If there are threads waiting, one of them is woken up.

## Use Cases
- Managing access to a limited number of resources (e.g., a pool of database connections).
- Implementing producer-consumer problems.
- Controlling access to shared data.
```c++
#include <condition_variable>
#include <mutex>
class Semaphore{
private:
  std::mutex mtx;
  std::condition_variable cv;
  int count;
public:
  Semaphore(int a): count(a){}
  void setCount(int a){
    count = a;
  }
  void signal(){
    std::unique_lock<std::mutex> lock(mtx);
    count++;
    if(count<=0){ //this means some threads would have been waiting
      cv.notify_one();
    }
  }
  void wait(){
    std::unique_lock<std::mutex> lock(mtx);
    count--;
    while(count<0){
      cv.wait(lock);
    }
  }
};

```