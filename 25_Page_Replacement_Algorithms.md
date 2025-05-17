# Page Replacement Algorithms Explained in Detail

When a **page fault** occurs, it means that a process is trying to access a page that is not currently in the main memory (RAM). The operating system (OS) needs to bring this page from secondary memory (swap space) into main memory.

## Problem

Sometimes, the physical memory is already full — all the frames are occupied by other pages. So, the OS must decide **which page to remove** to make space for the new page. This decision is made by a **Page Replacement Algorithm**.

### Aim of Page Replacement Algorithms

The main goal of page replacement algorithms is to **minimize the number of page faults**. The fewer page faults, the better and faster the system performance.

---

## Types of Page Replacement Algorithms

### 1. FIFO (First In First Out)

- This is the simplest algorithm.
- It removes the page that has been in memory the longest — i.e., the oldest page is replaced first.
- Easy to implement using a queue.

**Problem:**

- FIFO can perform poorly in some cases.
- Sometimes an old page may still be frequently used, but FIFO removes it anyway.
- This causes that page to be loaded again soon, leading to more page faults.

**Belady’s Anomaly:**

- In FIFO, sometimes increasing the number of frames can cause **more** page faults.
- This strange behavior is called **Belady's Anomaly**.
- Other algorithms generally do not have this problem.

---

### 2. Optimal Page Replacement

- This algorithm replaces the page that will **not be used for the longest time in the future**.
- It gives the **lowest possible number of page faults** — the best possible performance.

**Problem:**

- It requires knowledge of future page requests.
- Since predicting future references is impossible in practice, this algorithm is not implementable but is used as a benchmark.

---

### 3. Least Recently Used (LRU)

- This algorithm replaces the page that has **not been used for the longest time in the past**.
- It uses the idea that pages used recently will likely be used again soon (locality principle).
- This is a good approximation of the optimal algorithm.

**Implementation Methods:**

- **Counters:** Every page has a timestamp updated each time it is accessed. The page with the oldest timestamp is replaced.
- **Stack:** Maintain a stack of pages. When a page is accessed, remove it from the stack and place it on top. The bottom of the stack contains the least recently used page.

- Usually, a doubly linked list is used for efficient operations when removing and inserting pages in the stack.

---

### 4. Counting-Based Page Replacement

- Maintain a counter for each page that counts the number of references to that page.

**Types:**

- **Least Frequently Used (LFU):** Replace the page with the smallest reference count (used least frequently).
- **Most Frequently Used (MFU):** Replace the page with the highest reference count (based on the assumption that pages with many references might have just finished their use).

**Note:** LFU and MFU are rarely used in practical systems.

---

## Summary

When a page fault happens, the OS needs to decide which page to replace to bring the required page into memory.

- **FIFO** is the simplest but can perform poorly and has Belady’s Anomaly.
- **Optimal** is the best theoretically but impossible to implement due to unknown future.
- **LRU** is a practical and efficient approximation, considering recent usage.
- **Counting-based algorithms** like LFU and MFU exist but are less common in real systems.

These algorithms help balance memory usage efficiently, improving overall system performance.

---