# Paging 

## 1. Problem of Dynamic Partitioning – External Fragmentation

The biggest problem with dynamic partitioning is external fragmentation. This means that small free memory spaces are scattered throughout the memory, but even combined, they cannot satisfy the requirement of a large process. 

Although this problem can be somewhat reduced by compaction, compaction introduces extra overhead on the system in terms of time and CPU usage.

Therefore, we need a more flexible and efficient memory management mechanism that allows processes to be loaded into memory without causing excessive fragmentation.

## 2. Idea Behind Paging

Imagine the memory has only two small free holes, each 1 KB in size.

If a process requires 2 KB of memory, contiguous allocation will fail because we need 2 KB of continuous free space.

However, there are two free holes of 1 KB each, which together make 2 KB, but they are not contiguous.

If we divide the process into smaller blocks of 1 KB each, we can place these blocks into separate free holes.

This is the basic idea behind paging.

## 3. What is Paging?

Paging is a memory-management technique in which:

- The physical address space of a process is allocated non-contiguously.
- External fragmentation is avoided, and compaction is not needed.
- Physical memory is divided into fixed-size blocks called **frames**.
- Logical memory is also divided into blocks of the same size called **pages**.
- The page size equals the frame size (for example, both are 4 KB).
- The page size is generally decided by the processor architecture, commonly 4,096 bytes.

### What is a Page Table?

A page table is a data structure that keeps track of which page is mapped to which frame.

Each entry in the page table contains the base address of the frame in physical memory.

When the CPU generates a logical address, it is divided into two parts: the **page number (p)** and the **page offset (d)**.

The page number is used as an index into the page table to find the frame's base address.

The page table is stored in the main memory when a process is created, and its base address is stored in the Process Control Block (PCB).

There is a special register called the **Page Table Base Register (PTBR)** that points to the current page table.

When a context switch occurs, only the PTBR needs to be changed, making the process efficient.

## 4. How Paging Avoids External Fragmentation

Since pages are stored in any available free frame in physical memory, the process does not require contiguous memory allocation.

All free frames in memory can be used to load the process.

This way, external fragmentation is avoided because there is no need for contiguous free space.

## 5. Why is Paging Slow, and How to Make it Faster?

Paging slows down memory access because every time the CPU generates a logical address, the system must check the page table to find which frame contains the required page.

This involves two memory accesses:

- First, accessing the page table to get the frame address.
- Second, accessing the actual data from the frame.

This extra memory access makes paging slower.

## 6. Translation Lookaside Buffer (TLB)

To speed up paging, hardware provides a special high-speed cache called the **Translation Lookaside Buffer (TLB)**.

TLB stores pairs of page numbers and their corresponding frame addresses (key-value pairs).

When the CPU generates a logical address, the TLB is checked first to see if the page number is present.

- If the page number is found in the TLB (**TLB hit**), the frame address is obtained directly without accessing the full page table.
- If the page number is not found in the TLB (**TLB miss**), the system accesses the page table to find the frame address and also stores this entry in the TLB for future use.

This makes the paging process faster.

### Address Space Identifier (ASID)

Each TLB entry also stores an **Address Space Identifier (ASID)**.

ASID uniquely identifies each process, allowing the TLB to store entries of multiple processes simultaneously without confusion.

When translating a virtual page number, the TLB checks if the ASID matches the current process's ASID.

If it does not match, the TLB treats it as a miss.

## Summary

- Paging is used to avoid the external fragmentation problem of dynamic partitioning.
- Paging divides memory into fixed-size pages and frames, allowing non-contiguous allocation.
- The page table maps logical pages to physical frames.
- Paging eliminates external fragmentation.
- Paging slows memory access because of multiple memory lookups, so TLB is used to speed up the process.
- TLB contains ASIDs to handle multiple processes efficiently.

