The semantics of the lock() and unlock() routines are simple. Call-
ing the routine lock() tries to acquire the lock; 
if no other thread holds the lock (i.e., it is free), the thread will acquire the lock and enter the critical section;  this thread is sometimes said to be the owner of the lock. 
If another thread then calls lock() on that same lock variable (mutex in
this example), it will not return while the lock is held by another thread;
in this way, other threads are prevented from entering the critical section
while the first thread that holds the lock is in there
Once the owner of the lock calls unlock(), the lock is now available
(free) again. If no other threads are waiting for the lock (i.e., no other
thread has called lock() and is stuck therein), the state of the lock is
simply changed to free. If there are waiting threads (stuck in lock()),
one of them will (eventually) notice (or be informed of) this change of the
lock’s state, acquire the lock, and enter the critical section.
Locks provide some minimal amount of control over scheduling to
programmers. In general, we view threads as entities created by the pro-
grammer but scheduled by the OS, in any fashion that the OS chooses.
Locks yield some of that control back to the programmer; by putting
a lock around a section of code, the programmer can guarantee that no
more than a single thread can ever be active within that code. Thus locks
help transform the chaos that is traditional OS scheduling into a more
controlled activity