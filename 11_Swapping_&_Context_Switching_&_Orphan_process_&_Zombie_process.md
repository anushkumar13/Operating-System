# Swapping | Context-Switching | Orphan Process | Zombie Process

## 1. Swapping  
Swapping is a process where the system temporarily moves processes out of the main memory to secondary storage (like a hard disk) to manage memory efficiently and allocate space for other processes. Later, when needed, the process is brought back into memory and continues execution from where it left off.

### Detailed Explanation:  
In a time-sharing system, there is a Medium Term Scheduler (MTS) responsible for swapping. Sometimes, memory becomes insufficient for all running processes (degree of multi-programming increases), so some processes need to be temporarily removed from memory to keep the system running smoothly.

- When a process is moved out of memory, it is called **swap-out**.  
- When a process is brought back into memory to resume execution, it is called **swap-in**.  

Swapping allows better utilization of memory and creates a better mix of processes. It becomes necessary when memory requirements change and more processes or data need to be loaded than the available memory.

Swapping pauses the process execution by sending it to secondary storage and later brings it back without losing any data.

---

## 2. Context-Switching  
Context-switching is the process where the CPU switches control from one running process to another. It involves saving the current process state and loading the state of the new process to continue execution.

### Detailed Explanation:  
Whenever the CPU switches from one process to another, it saves the current process’s context (like CPU registers, program counter, stack pointer, etc.) into the Process Control Block (PCB).

Then, it loads the context of the new process from its PCB into the CPU registers so that the new process can run.

This entire procedure is called **context-switching**.

Context-switching introduces overhead because the CPU is not doing useful work during this time but only switching between processes.

The speed of context-switching depends on hardware factors like memory speed and the number of registers to save/restore.

---

## 3. Orphan Process  
An orphan process is a child process whose parent process has terminated but the child is still running.

### Detailed Explanation:  
When a process creates a child process, it becomes the parent. If the parent terminates before the child finishes, the child becomes an orphan process.

Orphan processes are adopted by the **init** process, which is the first process started by the OS. The init process manages these orphan processes to ensure proper system functioning.

---

## 4. Zombie Process / Defunct Process  
A zombie process is a process that has completed execution but still has an entry in the process table.

### Detailed Explanation:  
When a child process finishes execution and terminates, it must send its exit status to the parent process.

If the parent process does not read this exit status using the **wait** system call, the child process’s entry remains in the process table as a zombie process.

In other words, a zombie process is a terminated process whose record is still present in the process table because the parent has not yet handled its exit status.

This usually happens if the parent delays calling the wait() system call after the child terminates.

Once the parent calls wait() and receives the exit status, the OS removes the zombie process entry from the process table. This is called **reaping the zombie process**.

Zombie processes do not consume memory or resources, but their entries in the process table waste system space unnecessarily.

---

## Summary  
- **Swapping:** Temporarily moving processes between main memory and secondary storage to optimize memory usage.  
- **Context-Switching:** Saving the state of the currently running process and loading the state of another process when switching CPU control.  
- **Orphan Process:** A child process whose parent has terminated but the child is still running; it is adopted by the init process.  
- **Zombie Process:** A terminated process whose entry remains in the process table until the parent reads its exit status.

---