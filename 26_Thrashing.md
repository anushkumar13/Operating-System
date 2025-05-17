# Thrashing

## 1. What is Thrashing?

Thrashing occurs when a process does not have enough frames to support the pages it is actively using, leading to frequent page faults.

In simple terms:

- The process has fewer memory frames than the number of pages it needs to use actively.
- Whenever the process accesses a page not present in memory, a page fault occurs.
- On a page fault, the OS loads the required page from disk into memory.
- Since all pages are actively used, the OS ends up replacing pages that the process will immediately need again.
- This causes a continuous cycle where a page is replaced but soon required again, resulting in repeated loading and replacement.

This rapid and continuous page fault and page swapping condition is called **Thrashing**.

---

## 2. Effects of Thrashing

- The system spends a large amount of time servicing page faults.
- Much of the system's resources are used in loading pages from disk rather than executing actual processes.
- As a result, overall system performance degrades significantly.

---

## 3. How to Handle Thrashing? (Techniques)

### i. Working Set Model

- This model is based on the **Locality Model**.
- The Locality Model states that a process uses a small set (locality) of pages actively at any given time, and this set changes as the process executes.
- The Working Set Model suggests allocating enough frames to a process to cover its current locality of pages.
- If the number of frames allocated is less than the size of the locality, the process will experience thrashing.
- Therefore, it is important to track the working set size and allocate sufficient frames to each process to support its active pages.

### ii. Page Fault Frequency (PFF) Scheme

- Thrashing causes a very high page fault rate.
- To control thrashing, the system monitors page fault rates.
- In this scheme, upper and lower limits for acceptable page fault frequency are set.
- If the page fault rate goes **above the upper limit**, it indicates the process needs more frames, so additional frames are allocated.
- If the page fault rate drops **below the lower limit**, it means the process has more frames than needed, and some frames can be taken away.
- By controlling page fault frequency through dynamic frame allocation, thrashing can be prevented.

---

## Summary

- Thrashing happens when a process has fewer frames than the number of its active pages, causing frequent page faults.
- This leads to severe performance degradation because the system spends too much time swapping pages in and out.
- The Working Set Model recommends giving a process enough frames to cover its current locality of active pages.
- The Page Fault Frequency scheme controls thrashing by monitoring and adjusting the number of frames based on the page fault rate.

---