
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

## C++ Example: Binary Semaphore

```cpp
#include <iostream>
#include <thread>
#include <semaphore.h> // Include semaphore header for POSIX systems

class BinarySemaphore {
private:
    sem_t semaphore;

public:
    BinarySemaphore() {
        sem_init(&semaphore, 0, 1); // Initialize semaphore to 1
    }

    ~BinarySemaphore() {
        sem_destroy(&semaphore); // Clean up semaphore
    }

    void wait() {
        sem_wait(&semaphore); // Decrease the semaphore value
    }

    void signal() {
        sem_post(&semaphore); // Increase the semaphore value
    }
};

void critical_section(int id, BinarySemaphore& sem) {
    sem.wait();
    std::cout << "Thread " << id << " entering critical section.\n";
    // Simulate work
    std::this_thread::sleep_for(std::chrono::seconds(1));
    std::cout << "Thread " << id << " leaving critical section.\n";
    sem.signal();
}

int main() {
    const int num_threads = 3;
    BinarySemaphore sem;
    std::thread threads[num_threads];

    for (int i = 0; i < num_threads; ++i) {
        threads[i] = std::thread(critical_section, i, std::ref(sem));
    }

    for (auto& t : threads) {
        t.join();
    }

    return 0;
}
```

## C++ Example: Counting Semaphore

```cpp
#include <iostream>
#include <thread>
#include <semaphore.h> // Include semaphore header for POSIX systems

class CountingSemaphore {
private:
    sem_t semaphore;

public:
    CountingSemaphore(int initial) {
        sem_init(&semaphore, 0, initial); // Initialize semaphore with a given count
    }

    ~CountingSemaphore() {
        sem_destroy(&semaphore); // Clean up semaphore
    }

    void wait() {
        sem_wait(&semaphore); // Decrease the semaphore value
    }

    void signal() {
        sem_post(&semaphore); // Increase the semaphore value
    }
};

void worker(int id, CountingSemaphore& sem) {
    sem.wait();
    std::cout << "Worker " << id << " is working.\n";
    // Simulate work
    std::this_thread::sleep_for(std::chrono::seconds(1));
    std::cout << "Worker " << id << " finished working.\n";
    sem.signal();
}

int main() {
    const int max_concurrent_workers = 2;
    const int total_workers = 5;
    CountingSemaphore sem(max_concurrent_workers);
    std::thread threads[total_workers];

    for (int i = 0; i < total_workers; ++i) {
        threads[i] = std::thread(worker, i, std::ref(sem));
    }

    for (auto& t : threads) {
        t.join();
    }

    return 0;
}
```

## Summary
- Semaphores are crucial for synchronizing access to shared resources in concurrent programming.
- They can be binary or counting, each serving different purposes.
- Proper use of semaphores can prevent race conditions and ensure safe data sharing among threads.

## Implementing Semaphores
```c++
struct semaphore {
  
    enum value(0, 1);

    // q contains all Process Control Blocks (PCBs)
    // corresponding to processes got blocked
    // while performing down operation.
    Queue<process> q;

};
P(semaphore s)
{
    if (s.value == 1) {
        s.value = 0;
    }
    else {
        // add the process to the waiting queue
        q.push(P) sleep();
    }
}
V(semaphore s)
{
    if (s.q is empty) {
        s.value = 1;
    }
    else {

        // select a process from waiting queue
        Process p = q.front();
        // remove the process from waiting as it has been
        // sent for CS
        q.pop();
        wakeup(p);
    }
}

// This code is modified by Susobhan Akhuli

```
--- 

Feel free to modify any part of the notes or code snippets to better fit your style or needs!