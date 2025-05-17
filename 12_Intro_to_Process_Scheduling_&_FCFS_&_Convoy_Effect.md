# Introduction to Process Scheduling | FCFS | Convoy Effect

## 1. Process Scheduling

Process scheduling is a very important concept in operating systems, especially in multitasking (multi-programming) OS.  

In a multi-programming OS, many processes reside in memory simultaneously.  

However, the CPU can execute only one process at a time.  

Therefore, the OS switches the CPU between different processes, making the system more productive.  

When a process using the CPU goes into an I/O wait or its time quantum expires, the OS takes the CPU away from that process and allocates it to another ready process.  

This switching happens continuously.

## 2. CPU Scheduler

Whenever the CPU becomes idle (meaning no process is currently executing on it), the OS selects a process from the ready queue to execute next.  

This task is performed by the Short-Term Scheduler (STS), which picks the next process from the ready queue.

## 3. Non-Preemptive Scheduling

In non-preemptive scheduling, once the CPU is allocated to a process, the process keeps the CPU until it finishes execution or moves to a waiting state (such as waiting for I/O).  

In other words, the process holds the CPU until it either terminates or voluntarily enters the waiting state.  

One problem with this approach is starvation — if a process has a very long CPU burst time, shorter processes must wait a long time before getting the CPU.  

CPU utilization tends to be lower because there is less flexibility in switching.

## 4. Preemptive Scheduling

In preemptive scheduling, the CPU is not necessarily held by a process until termination or waiting.  

The OS can forcibly take the CPU away from a running process when its time quantum expires.  

This leads to higher CPU utilization.  

Starvation is reduced because every process gets at least some CPU time.

## 5. Goals of CPU Scheduling

The OS tries to achieve the following goals in CPU scheduling:

- **Maximum CPU utilization**: Keep the CPU busy all the time.  
- **Minimum Turnaround Time (TAT)**: Reduce the total time from process submission to completion.  
- **Minimum Waiting Time (WT)**: Minimize the time a process waits in the ready queue.  
- **Minimum Response Time**: Reduce the time it takes for a process to start getting CPU after arriving in the ready queue.  
- **Maximum Throughput**: Increase the number of processes completed per unit time.

## 6. Throughput

Throughput is the number of processes completed per unit time.  

Higher throughput means a more efficient system.

## 7. Arrival Time (AT)

Arrival Time is the time when a process enters the ready queue.

## 8. Burst Time (BT)

Burst Time is the total time required by a process on the CPU to complete its task.

## 9. Turnaround Time (TAT)

Turnaround Time is the total time taken by a process from arrival in the ready queue to its completion.  

**Formula:**  
`TAT = Completion Time (CT) - Arrival Time (AT)`

## 10. Waiting Time (WT)

Waiting Time is the total time a process spends waiting in the ready queue for CPU allocation.  

**Formula:**  
`WT = Turnaround Time (TAT) - Burst Time (BT)`

## 11. Response Time

Response Time is the time from when a process arrives in the ready queue until it gets the CPU for the first time.

## 12. Completion Time (CT)

Completion Time is the time at which the process finishes its execution.

## 13. FCFS (First Come First Serve) Scheduling

FCFS is the simplest scheduling algorithm.  

The process that arrives first in the ready queue gets the CPU first.  

The process holds the CPU until it finishes execution.

### Problem of FCFS: Convoy Effect

If the first process has a very long burst time, all the shorter processes that arrive later have to wait for a long time.  

This situation is called the **Convoy Effect**.  

In the Convoy Effect, a long process holds a resource (CPU) causing other shorter processes to block and wait.  

This reduces resource utilization and degrades system performance.

---

## Summary

Process Scheduling helps the OS manage multitasking by switching the CPU among processes.  

The CPU Scheduler (Short-Term Scheduler) picks processes from the ready queue to execute on the CPU.  

Non-preemptive scheduling lets a process hold the CPU until it finishes or waits, while preemptive scheduling allows forcibly taking the CPU away after a time quantum.  

The key goals of CPU scheduling are to maximize CPU utilization, minimize waiting, turnaround, and response times, and maximize throughput.  

FCFS scheduling is easy to implement but suffers from the Convoy Effect, which can slow down the system when a long process blocks shorter ones.

---