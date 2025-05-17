# Conditional Variables and Semaphores for Thread Synchronization

## 1. What is a Conditional Variable?

A conditional variable is a synchronization primitive that allows threads to wait for a specific condition to occur.

In other words, if a thread needs to wait for some event or condition to happen, it can wait using a conditional variable.

### 1.a) How Does a Conditional Variable Work?

A conditional variable works together with a lock.

When a thread waits on a conditional variable, it first must acquire the lock.

When the thread goes into the waiting state, it releases the lock so that other threads can access the critical section.

The waiting thread remains in the wait state until another thread satisfies the condition and notifies it.

Once notified, the waiting thread immediately re-acquires the lock and continues its work.

### 1.b) Why Use Conditional Variables?

The main reason is to avoid busy waiting.

Busy waiting means a thread continuously checks whether a condition has been met, which wastes CPU time.

With conditional variables, the thread goes into a wait state without wasting CPU resources.

### 1.c) Contention (threads fighting for the same resource) does not happen here.

## 2. What are Semaphores?

A semaphore is a synchronization method that coordinates threads.

It is an integer value that indicates how many resources are available.

### 2.a) What is the Purpose of Semaphores?

Multiple threads can enter the critical section simultaneously as long as resources are available.

This means if the resource count is high, that many threads can work concurrently.

### 2.b) Semaphores vs Mutex

A semaphore allows multiple threads to access a finite number of resources simultaneously.

Whereas a mutex is a lock that allows only one thread at a time to access a shared resource.

**Summary:**

- Semaphore is used for multiple instances of resources.

- Mutex is used for a single resource.

### 2.c) Types of Semaphores:

- **Binary Semaphore:**  
  Its value can only be 0 or 1.  
  It can be used like a mutex lock and is sometimes called a "mutex."

- **Counting Semaphore:**  
  Its value can be any positive integer.  
  It controls a finite number of instances of resources like printers, database connections, etc.

### 2.d) How do Semaphores Avoid Busy Waiting?

When a process performs a `wait()` operation and the semaphore value is zero (or negative), the process does not busy wait.

Instead, it is blocked and moved to a wait queue.

The process state changes to "Waiting."

Then the CPU scheduler runs other processes.

### 2.e) When Another Process Performs a `signal()` Operation:

The blocked process is restarted via a `wakeup()` operation.

This `wakeup` changes the process state from "Waiting" to "Ready."

Then it moves to the ready queue and executes when the CPU allocates time to it.

---

## Summary

Conditional variables provide a mechanism for threads to wait and get notified on specific conditions, thus avoiding busy waiting.

Semaphores synchronize threads to access finite resources, including both binary semaphores (mutexes) and counting semaphores.

Semaphores avoid busy waiting by blocking threads and waking them up when resources become available.

---