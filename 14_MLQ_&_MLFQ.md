# Multi-Level Queue (MLQ) and Multi-Level Feedback Queue (MLFQ) Scheduling

## 1. Multi-Level Queue Scheduling (MLQ)

In Multi-Level Queue scheduling, the ready queue is divided into multiple sub-queues, each having its own priority.

Each process is permanently assigned to one particular queue based on certain properties of the process, such as:

- Process priority,
- Process type (system process, interactive process, batch process),
- Memory or process size.

This assignment is inflexible, meaning that once a process is assigned to a queue, it cannot move to another queue.

Each queue can have its own scheduling algorithm. For example:

- System Process queue might use Round Robin (RR),
- Interactive Process queue might use Round Robin (RR),
- Batch Process queue might use First-Come-First-Serve (FCFS).

### Types of Processes:

- **System Process:** Created by the OS, with the highest priority.
- **Interactive Process (Foreground Process):** Waits for user input or I/O, has relatively high priority.
- **Batch Process (Background Process):** Runs silently in the background, no user input needed, has lower priority.

Scheduling between the different queues uses fixed priority preemptive scheduling. This means that processes in higher priority queues always get the CPU before those in lower priority queues.

For example, if an interactive (foreground) process becomes ready while a batch process is running, the batch process will be preempted.

### Problems in MLQ:

- Lower priority queues may suffer **starvation**, because their processes are not scheduled until all higher priority queues are empty.
- **Convoy Effect** can occur if a long process in a queue blocks others, causing delays.

---

## 2. Multi-Level Feedback Queue Scheduling (MLFQ)

MLFQ also uses multiple sub-queues, but it adds flexibility by allowing processes to move between queues.

The idea is to place processes into different queues based on their CPU burst times:

- Processes that use a lot of CPU time are moved to lower priority queues.
- I/O-bound or interactive processes that frequently wait for input are placed in higher priority queues.

If a process waits too long in a lower priority queue, its priority is increased and it is moved to a higher priority queue — this is called **ageing**.

This technique reduces starvation.

Because of this dynamic adjustment, MLFQ is more flexible than MLQ.

MLFQ can also be configured according to system design requirements by adjusting its parameters.

---

## 3. Comparison Table

| Algorithm                  | Design Complexity | Preemption | Convoy Effect | Overhead |
|----------------------------|-------------------|------------|---------------|----------|
| FCFS                       | Simple            | No         | Yes           | No       |
| SJF                        | Complex           | No         | Yes           | No       |
| PSJF (Preemptive SJF)      | Complex           | Yes        | No            | Yes      |
| Priority                   | Complex           | No         | Yes           | No       |
| Preemptive Priority        | Complex           | Yes        | Yes           | Yes      |
| Round Robin (RR)           | Simple            | Yes        | No            | Yes      |
| Multi-Level Queue (MLQ)    | Complex           | Yes        | Yes           | Yes      |
| Multi-Level Feedback Queue (MLFQ) | Complex   | Yes        | Yes           | Yes      |

---

## Summary (in simple terms)

In MLQ, a process is permanently assigned to one queue, and each queue has its own priority. Processes do not move between queues. This can cause starvation and convoy effects.

In MLFQ, processes are allowed to move between queues. If a process uses too much CPU time, it is moved to a lower priority queue. If it waits too long, its priority is increased and it moves to a higher priority queue (ageing). This reduces starvation and makes MLFQ more flexible and intelligent in scheduling processes based on their behavior.

Both algorithms use multiple queues, but MLFQ provides better adaptability and fairness.

---