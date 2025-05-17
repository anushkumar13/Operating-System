# Free Space Management

Free space management is a crucial part of memory management, especially in dynamic partitioning where memory is allocated dynamically to processes. Here we will discuss free space management in detail, including how fragmentation is handled and how operating systems allocate memory efficiently.

---

## 1. Defragmentation / Compaction

One of the biggest problems in dynamic partitioning is **external fragmentation**. External fragmentation occurs when free memory spaces (holes) are scattered throughout memory in small chunks, which individually cannot accommodate a large process, even though the total free memory might be enough.

To solve this problem, the **compaction** technique is used.

Compaction means collecting all the free memory spaces together in one place, making all free partitions contiguous. At the same time, all the loaded (allocated) processes are brought together in one place.

By doing this, all the free spaces merge to form a large continuous free block of memory.

This large free space allows bigger processes to be loaded into memory.

Compaction is also called **defragmentation**, because it reduces memory fragmentation.

However, compaction comes with a downside. It decreases system efficiency since moving all the free spaces and processes to make memory contiguous takes time and requires CPU resources. This process causes CPU overhead and temporary slowdown.

---

## 2. Free Space Representation in Operating System

How does the operating system keep track of free memory spaces (holes)?

The OS maintains a special data structure called a **free list**.

The free list is typically a linked list where each node represents a free hole in memory.

Each free hole's size and starting address are stored in the free list.

Whenever a new process requests memory, the OS scans the free list to find a suitable hole to allocate memory.

---

## 3. Memory Allocation Request Algorithms

When a process requests `n` units of memory, the OS must find a hole in the free list that can satisfy this request. To do this efficiently, the OS uses several algorithms:

### a. First Fit

- The OS allocates the first hole in the free list that is large enough to satisfy the process’s memory request.
- It is the simplest and easiest algorithm to implement.
- It has low time complexity because it finds a suitable hole quickly.
- However, it may leave small free holes scattered, which could cause fragmentation issues later.

### b. Next Fit

- This is an improved version of First Fit.
- Instead of always starting from the beginning of the free list, the search starts from the hole where the last allocation was made.
- This avoids repeatedly scanning the same holes at the start and makes allocation a bit more efficient.
- Other advantages are similar to First Fit.

### c. Best Fit

- The OS allocates the smallest hole that is large enough to satisfy the memory request.
- This reduces internal fragmentation because it avoids wasting large holes on small processes.
- However, it tends to create many tiny holes, increasing external fragmentation.
- It is slower since the OS must scan the entire free list to find the best hole.

### d. Worst Fit

- The OS allocates the largest hole available that satisfies the memory request.
- The idea is that by allocating the largest hole, leftover small holes remain for future processes.
- Like Best Fit, it requires scanning the entire free list and is therefore slow.

---

## Summary

- **Compaction (Defragmentation)** reduces external fragmentation by bringing all free memory blocks together to form one large free space.
- The OS keeps track of free memory holes using a linked list called the **free list**.
- For allocating memory, the OS uses various algorithms such as **First Fit, Next Fit, Best Fit,** and **Worst Fit**, each with its own pros and cons.
- The choice of algorithm depends on system requirements and the need to balance speed and memory utilization efficiency.

---