# Program, Process, and Thread – Detailed Explanation

---

## What is a Program?

First, it is important to understand what a **Program** is.

A program is an executable file that contains instructions designed to complete a specific task.  
When a programmer writes software, these instructions are saved in a file that the computer can understand.

These instructions are in a special form called **compiled code**.  
Compiled means that the human-readable code (like C, Java, Python) is converted into machine code that the computer can directly execute.

This program is stored on a hard disk or any permanent storage device.  
It remains safe there until the computer is turned off.

### Summary of Program:
- A static set of instructions.  
- Exists as a file.  
- Until executed, it is just a file.  
- Examples: Notepad.exe, Chrome.exe, Calculator.exe — all are programs.

---

## What is a Process?

Now, let's understand what a **Process** is.

When you run a program on your computer, the program becomes a **process**.  
A process means the program that is currently running — the instructions being executed at that moment.

A process has its own state — meaning where it is in the execution, which instructions are running, and what resources it is using.

A process has its own **address space** in RAM (primary memory).  
This means the process's instructions and data are temporarily stored in RAM for the CPU to access quickly.

Each process has a **Process Control Block (PCB)** containing information like process ID, priority, state, CPU registers, memory pointers, etc.

### Summary of Process:
- A running instance of a program.  
- Resides in RAM (memory).  
- The form of the program during execution.  
- Multiple processes can run simultaneously.  
- Example: When you open Chrome, the Chrome process loads into RAM.

---

## What is a Thread?

Now, let's understand the most interesting concept — **Thread**.

A thread is a small execution unit inside a process.

If the process is a big task, threads are smaller parts of that task that can run simultaneously or in parallel.

Threads are also called **light-weight processes** because they are much easier and faster to create than a full process.

A process can have one or many threads, and these threads work in parallel to perform different parts of the process’s job.

This improves efficiency and speeds up task completion.

### Features of Threads:
- A thread is a single sequence of instructions — it follows its own independent path inside the process.  
- Threads share the process’s resources like memory and files, allowing easy communication between them.  
- Threads enable multitasking and parallelism within a process.

### Real-life example of Threads:
Imagine you are using a browser like Chrome.

When you open multiple tabs, each tab is handled by a different thread.

- One thread handles typing in a tab.  
- Another thread checks spelling.  
- A third thread formats text.  
- A fourth thread saves the document.

All these threads work inside the same Chrome process at the same time.

### Summary of Thread:
- A smaller execution path inside a process.  
- Lightweight and independent.  
- Multiple threads divide process tasks.  
- Used to achieve parallelism.

---

## Overall Relationship

- **Program** = A file containing instructions.  
- **Process** = The running form of a program loaded into RAM.  
- **Thread** = A small execution stream inside a process that runs independently.

---

# Multitasking and Multithreading – Detailed Explanation

---

## What is Multitasking?

First, let’s understand **Multitasking**.

Multitasking means a computer system running multiple tasks or processes simultaneously.  
In other words, the computer is doing more than one task at the same time.

When we do multitasking, the CPU divides its time into small parts (this is called **time-sharing**) and gives each process a little bit of time.

This way, it appears that all tasks are running simultaneously, but actually, the CPU is switching very fast between these tasks.

### Types of Multitasking:

- **Preemptive Multitasking:**  
  The CPU decides on its own which process gets how much time and when.  
  When the current process's time is over, the CPU switches control to another process.

- **Cooperative Multitasking:**  
  Processes themselves decide when to give control to other processes.  
  Processes cooperate to share the CPU time.

### Benefits of Multitasking:

- Users can run multiple programs at the same time.  
- System productivity increases.  
- CPU utilization is maximized.

### Example of Multitasking:

Imagine you are running Chrome, VS Code, and Spotify on your computer simultaneously.  
All these running together means multitasking.

---

## What is Multithreading?

Now, let’s understand **Multithreading**.

Multithreading means having multiple threads inside a single process, and these threads work simultaneously.

As we learned earlier, threads are independent execution units inside a process.

Multithreading divides the process into smaller tasks that can run in parallel.

This makes the work inside a process faster and more efficient.

### Features of Multithreading:

- A process contains multiple threads.  
- Threads share their resources like memory.  
- Threads allow parallel execution, meaning one thread does not disturb the other.  
- Threads are lightweight, so creating and managing them is easier than processes.

### Example of Multithreading:

Imagine using a text editor where you are typing, spell-checking is running in the background, and text is being saved simultaneously.  
All these happen through different threads inside the same process.

---

## Multitasking vs Multithreading

| Point                  | Multitasking                               | Multithreading                          |
|------------------------|-------------------------------------------|---------------------------------------|
| What is it?            | Running multiple processes simultaneously | Running multiple threads inside one process |
| Level                  | Process level                             | Thread level                          |
| Resource Sharing       | Processes have separate resources (separate memory) | Threads share resources (common memory) |
| Overhead               | High (process switching is costly)       | Low (thread switching is fast)       |
| Use                    | When multiple applications run simultaneously | When parallel tasks run inside one application |
| Example                | Running multiple apps (Chrome + VS Code) | Multiple threads inside one app (browser tabs, typing + spell check) |

---

## Summary

Multitasking is running multiple processes at the same time where the CPU shares its time among them.

Multithreading is running multiple threads inside a process, dividing tasks in parallel.

Multithreading can also be considered a part of multitasking because parallel execution of threads inside a process also gives a feel of multitasking.

---

# Thread Scheduling – Detailed Explanation

---

## What is Thread Scheduling?

When a process contains multiple threads, the CPU needs to decide which thread will run and for how long. This decision-making process is called **Thread Scheduling**.

In other words, thread scheduling is the task of the CPU and operating system where they allocate time to threads and decide which thread will use the CPU resources.

---

## Why is Thread Scheduling Important?

When multiple threads exist inside a process, they all compete for the same CPU.

A CPU can execute only one thread at a time (in the case of a single-core processor).

The operating system must decide how to switch between threads efficiently so that CPU utilization is maximized and the system runs fast.

Therefore, thread scheduling is very important.

---

## Types of Thread Scheduling

Operating systems use different algorithms to schedule threads. The main types are:

1. **Preemptive Scheduling:**  
   Here, the OS can forcibly remove a thread from the CPU if it thinks another thread is more important or the current thread's time is over.  
   This way, every thread gets a fair chance to use the CPU.  
   Preemptive scheduling is used in most modern operating systems.

2. **Cooperative Scheduling:**  
   Here, threads voluntarily give up CPU control when they finish their work or need to wait.  
   Then another thread can use the CPU.  
   If a thread does not voluntarily release the CPU, the system may hang.  
   This type of scheduling is found in older or simpler systems.

---

## Important Factors in Thread Scheduling

The operating system considers several factors while scheduling threads:

- **Priority:** Some threads are considered more important and get more CPU time.  
- **Fairness:** Every thread should get CPU time; no thread should starve (never get CPU).  
- **Response Time:** Threads should get CPU quickly to keep the system responsive.  
- **Throughput:** The system should complete as much work as possible.

---

## Thread States and Scheduling

Threads go through different states during their lifecycle:

- **New:** Thread is just created.  
- **Runnable:** Thread is ready and waiting for CPU.  
- **Running:** Thread is currently executing on CPU.  
- **Waiting/Blocked:** Thread is waiting for some resource and cannot execute.  
- **Terminated:** Thread has finished its execution.

Thread scheduling happens when:

- A thread is in the **Runnable** state, meaning it is ready for CPU.  
- The OS scheduler decides which runnable thread gets the CPU.  
- When a thread’s time slice (time quantum) ends or the thread becomes blocked, scheduling happens again.

---

## Scheduling Algorithms for Threads

Some common algorithms used for thread scheduling are:

1. **First-Come, First-Served (FCFS):**  
   The thread that becomes ready first gets the CPU first.  
   It is simple but if the first thread runs long, others must wait (called convoy effect).

2. **Round Robin (RR):**  
   Each thread gets a fixed time slice, then CPU moves to the next thread.  
   It is a fair algorithm and widely used.

3. **Priority Scheduling:**  
   Threads are assigned priorities, and the highest priority ready thread gets the CPU.  
   Problem: Low priority threads might starve (never get CPU).

4. **Multilevel Queue Scheduling:**  
   Threads are placed into different queues based on priority.  
   Higher priority queue threads run first.

---

## Real-life Example of Thread Scheduling

Imagine a restaurant with 3 chefs (threads) and one stove (CPU).  
All chefs want to cook (do work), but the stove can only serve one chef at a time.

The restaurant manager (OS scheduler) decides which chef will use the stove and for how long.

If a chef’s work is not finished, they step off the stove, and another chef takes their place.

This way, all chefs get a chance to work without making others wait too long.

---

## Summary

Thread Scheduling is the OS process of deciding which thread gets CPU time.

Scheduling ensures threads run efficiently and fairly.

Different algorithms like Round Robin, Priority Scheduling, and FCFS are used.

Threads exist in different states, and scheduling mainly applies to runnable threads.

Proper scheduling makes the system fast, responsive, and efficient.

---

# Context Switching – Detailed Explanation

---

## What is Context Switching?

Context switching is the process that happens when the CPU switches from one task (process or thread) to another. During this switch, the CPU must save the state of the currently running task—such as CPU registers, program counter, stack pointer, and more—and load the state of the new task.  

This entire operation is called **Context Switching**.

Context switching enables the CPU to smoothly transition from one task to another.

---

## Thread Context Switching vs Process Context Switching

The main difference lies in what context needs to be saved and loaded because the states of threads and processes differ.

### 1. Process Context Switching

A process is an independent program with its own address space (memory), resources (files, devices), and CPU state.

When the CPU switches from one process to another, it must save the entire context of the current process, which includes:

- The process’s program counter (PC), CPU registers, stack pointer  
- Memory mappings (like page tables)  
- Open files and I/O states  
- A full snapshot of the process's address space  

Because of this, process context switching is relatively heavy and slow since a lot of data must be saved and loaded.

The operating system also updates the CPU’s Memory Management Unit (MMU) so the new process can access its own separate address space.

**Example:** When a user switches from Chrome to VS Code, process context switching occurs.

### 2. Thread Context Switching

Threads exist within the same process and share the same address space.

This means that during switching between threads, the address space does **not** change. Only the CPU state like registers, stack pointer, and program counter need to be saved and loaded.

Thread context switching is much faster and lighter compared to process switching because memory mappings do not change.

Since threads share resources, there is no need to update the MMU during thread switches.

**Example:** When multiple tabs in a browser switch between threads, thread context switching happens.

---

## Summary Table: Process vs Thread Context Switching

| Feature                | Process Context Switching                   | Thread Context Switching                  |
|------------------------|---------------------------------------------|-------------------------------------------|
| Context saved          | Process-specific context + memory mapping  | Thread-specific CPU state only             |
| Memory address space   | Changes for each process                    | Shared among threads of the same process   |
| Overhead               | High (heavy operation)                      | Low (light-weight operation)               |
| Speed                  | Slow                                        | Fast                                      |
| Resource sharing       | Processes keep their own resources         | Threads share resources                     |
| Use case               | CPU switches between different processes   | CPU switches between threads within a process |

---

## Real-Life Example of Context Switching

Imagine a library:

- **Process Switching** is like one reader using one room in the library and another reader moving to a different room. Furniture, books, and the environment are different, so switching takes time.

- **Thread Switching** is like two readers sharing the same room, where one reader stops reading and another starts using the same furniture and environment. Therefore, switching is faster.

---

## Important Points

- Thread context switching is fast, making multithreading efficient for handling multiple tasks within the same process.

- Process context switching is slower, so switching between processes is more costly.

- The OS scheduler manages both types of switching depending on whether it is multitasking (process switching) or multithreading (thread switching).

---
