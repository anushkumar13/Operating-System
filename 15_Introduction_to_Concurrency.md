# Introduction to Concurrency

## 1. What is Concurrency?

Concurrency means running multiple sequences of instructions or tasks at the same time. In an operating system, when many processes or threads run simultaneously, it is called concurrency.

In other words, different tasks are happening together, making the system appear more efficient and work faster.

## 2. What is a Thread?

A thread is a single sequence of instructions that runs inside a process.

It is an independent path within a process where instructions get executed.

Threads are also called light-weight processes because they exist within a process and use fewer resources compared to full processes.

With multi-threading, we can divide a process's tasks into smaller independent parts that run as separate threads, achieving parallelism.

**Example:** In a browser with multiple tabs, while you type in one tab, background tasks like spell check, formatting, and saving text are happening simultaneously through different threads.

## 3. Thread Scheduling

To execute threads, they need to be scheduled.

The operating system allocates CPU time slices to each thread based on their priority.

This means the OS decides which thread gets the CPU and when.

Although threads run at runtime, the CPU time is allocated by the OS scheduler.

## 4. Thread Context Switching

When one thread is working and another thread needs to run, a context switch happens.

The OS saves the current thread’s state (such as the program counter, registers, stack) and then gives the CPU to another thread.

Important point: In thread switching, the memory address space does **not** switch because threads belong to the same process.

That is why thread context switching is faster than process context switching.

Also, CPU cache is better preserved during thread switching, making it more efficient.

## 5. How Do Threads Get CPU Time?

Each thread has its own program counter (PC) which indicates the current instruction being executed.

The OS decides which thread to run based on its scheduling algorithm.

Then, the OS fetches and executes instructions from that thread’s PC.

## 6. I/O or Time Quantum (TQ) Based Context Switching

Context switching among threads also happens when a thread completes its I/O or its allocated time quantum ends.

Just like processes have a Process Control Block (PCB), threads have a Thread Control Block (TCB).

The TCB stores the thread's state and necessary information, allowing the OS to perform efficient context switching.

## 7. Does Multi-threading Benefit a Single CPU System?

No, multi-threading does not benefit single CPU systems.

Because the CPU needs to frequently switch between threads to give them CPU time, which adds overhead.

Therefore, on a single CPU, multi-threading does not improve performance.

## 8. Benefits of Multi-threading

- **Responsiveness:** Multi-threading makes the system more responsive. For example, user input can be processed while background tasks run simultaneously.

- **Resource Sharing:** Threads share the same process resources, leading to efficient resource utilization.

- **Economy:** Creating and switching processes is costly, whereas creating and switching threads is relatively cheaper. Therefore, dividing tasks into threads within a process is better.

- **Multiprocessor Utilization:** Threads work better on multiprocessor systems, meaning if the system has multiple CPUs, threads can run in parallel and improve efficiency.

---