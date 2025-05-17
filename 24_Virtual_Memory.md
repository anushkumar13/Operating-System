# Virtual Memory, Demand Paging, and Page Faults Explained in Detail

## 1. What is Virtual Memory?

Virtual memory is a technique that allows the execution of processes even when their entire program is not fully loaded into physical memory (RAM). This means a process can run without having its whole program present in the RAM at once.

This technique creates an illusion for the user that they have a large main memory, even though the actual physical memory is limited. It is possible because the system uses a part of secondary memory (like a hard disk) as an extension of main memory, called the **swap space**.

## 2. Benefits of Virtual Memory

The biggest advantage of virtual memory is that programs can be larger than the available physical memory.

## 3. Problem Solved by Virtual Memory

For executing instructions, those instructions must be present in physical memory. But since physical memory size is limited, program size also gets limited.

However, the entire program doesn't need to be in memory at once all the time.

So, if we can execute a program even when only a part of it is in memory, it will be very beneficial.

**Benefits:**

- Program size can be larger than physical memory.
- Each user program requires less physical memory, so more programs can run simultaneously, improving CPU utilization and system throughput.
- Both the system and the user benefit because programs run even when fully loaded memory is not available.

## 4. Providing Virtual Memory to the Programmer

Programmers are given a large virtual memory space, regardless of the physical memory size.

This means programmers can write large programs without worrying about the physical memory limits.

## 5. What is Demand Paging?

Demand paging is a popular method to manage virtual memory.

## 6. How Demand Paging Works

Pages of the process that are not frequently used are stored in secondary memory.

## 7. Bringing Pages into Main Memory

When a particular page is needed, it is copied from secondary memory to main memory. This event is called a **page fault**.

On a page fault, the OS uses page replacement algorithms to decide which page to remove to make space for the new page.

## 8. What is a Lazy Swapper?

Lazy swapping means the entire process is not swapped at once.

Instead, pages are swapped only when they are actually needed.

## 9. Difference Between Swapper and Pager

We view a process as a sequence of pages, not as a single continuous address space.

- **Swapper** swaps the entire process in and out.
- **Pager** manages individual pages.

Demand paging uses a pager, not a swapper.

## 10. How Demand Paging Works in Detail

- When swapping in a process, the pager predicts which pages will be needed.
- Instead of swapping the whole process, only the required pages are loaded into memory.
- This reduces swap time and physical memory requirements.
- The page table uses a **valid-invalid bit** to indicate if a page is in memory or on disk.
  - Valid-invalid bit = 1 means the page is valid and in memory.
  - Valid-invalid bit = 0 means the page is invalid (not in memory or on disk).
- If a process accesses a page marked invalid, a **page fault** occurs.
- Hardware detects the page fault and traps the OS.
- The OS then handles the page fault:
  1. Checks in the Process Control Block (PCB) if the reference was valid.
  2. If the access was invalid (illegal), the process is terminated or an exception is raised.
  3. If valid, the pager selects a free frame in memory.
  4. A disk read operation is scheduled to bring the page into this free frame.
  5. After loading, the page table is updated to mark the page as present in memory.
  6. The interrupted instruction is restarted, and now the process can access the page without issues.

## 11. Pure Demand Paging

In the extreme case of pure demand paging, the process starts execution with no pages loaded into memory.

When the OS sets the instruction pointer to the first instruction, if that instruction is not in memory, a page fault occurs, and the OS loads it.

No page is loaded into memory until it is absolutely necessary.

## 12. Use of Locality of Reference

Demand paging performance improves using the concept of **locality of reference**.

Programs tend to access a small set of pages repeatedly over a short period.

Thus, only frequently used pages are kept in memory, which makes demand paging efficient.

## 13. Advantages of Virtual Memory

- Increases degree of multiprogramming.
- Allows running large programs on limited physical memory.

## 14. Disadvantages of Virtual Memory

- System performance may slow down due to time taken in swapping pages.
- **Thrashing** can occur, where excessive paging operations reduce system performance drastically.

## Summary

Virtual memory is a system that allows programs to run without fully loading the entire process into RAM. Demand paging is a common mechanism where pages are loaded only when needed, triggered by page faults. This approach increases multiprogramming and allows larger programs to run, but it can cause performance issues due to swapping and thrashing.

---