# Critical Section Problem and How to Address It

## 1. What are Process Synchronization Techniques?

When multiple processes or threads are working simultaneously and accessing shared data, process synchronization techniques are used. These techniques ensure the consistency of shared data, meaning the data remains correct and reliable without any conflicts.

## 2. What is a Critical Section (C.S)?

A critical section is a part of the code where processes or threads access shared resources such as common variables, files, or any data that is common for all.

This section usually involves write operations (modifying data).

The problem arises because when processes or threads execute simultaneously, any process can be interrupted in the middle. If shared resources are not handled properly, data corruption can occur.

## 3. Major Thread Scheduling Issue - Race Condition

Race condition happens when two or more threads try to access and modify the same shared data at the same time.

Since the thread scheduling algorithm can switch threads unpredictably, we cannot be sure about the execution order of threads.

In other words, the threads are "racing" to update the data, and the thread which executes first will decide the final data.

This leads to unpredictable output and creates problems for the system.

## 4. Solutions to Race Condition

To avoid race conditions, there are several solutions:

a. **Atomic Operations**  
Make the instructions in the critical section atomic, meaning they complete in a single CPU cycle without interruption.

b. **Mutual Exclusion using Locks**  
Apply a lock on the critical section so that only one thread can enter it at a time.

c. **Semaphores**  
A semaphore is a synchronization tool that helps coordinate threads to prevent race conditions.

## 5. Can a Simple Flag Variable Solve Race Condition?

No, a simple flag variable cannot solve the race condition.

Because while checking the flag, threads can still be interrupted, which may lead to race conditions.

Therefore, advanced synchronization techniques are necessary.

## 6. What is Peterson’s Solution?

Peterson’s solution is an algorithm that prevents race conditions for two processes or threads.

It provides mutually exclusive access to the critical section without using locks.

However, its limitation is that it only works for two processes or threads, not for multiple threads.

## 7. What are Mutexes/Locks?

A mutex or lock is a mechanism that provides mutual exclusion.

When a thread enters the critical section, it acquires the mutex lock and prevents other threads from entering the critical section.

This ensures only one thread can work inside the critical section simultaneously, thereby avoiding race conditions.

### Disadvantages of Mutexes/Locks:

- **Contention:**  
  When one thread holds the lock, other threads wait actively. If the thread holding the lock crashes or stops abruptly, other threads may wait indefinitely.

- **Deadlocks:**  
  Sometimes two or more threads wait for each other’s locks, causing the system to hang. This situation is called a deadlock.

- **Debugging Difficulties:**  
  Using locks makes the program complex and finding bugs becomes harder.

- **Starvation of High Priority Threads:**  
  Sometimes, a high priority thread may never get the lock and keeps waiting indefinitely, causing it to starve.

---