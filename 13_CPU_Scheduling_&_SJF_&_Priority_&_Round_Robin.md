# CPU Scheduling: SJF, Priority, and Round Robin (RR)

## 1. Shortest Job First (SJF) [Non-preemptive]

In this algorithm, the CPU is allocated to the process with the smallest Burst Time (BT) first.  

This means the process that will finish its job quickly gets the CPU first.  

However, estimating the Burst Time of each process beforehand is very difficult, because accurately predicting a process’s actual execution time is practically impossible.  

The algorithm selects the process with the shortest BT and runs it until it completes. After that, it selects the next shortest BT process.  

But this algorithm can suffer from the **Convoy Effect** if the first arriving process has a very long BT.  

It can also cause **starvation**, where short BT processes never get the CPU because longer jobs keep holding it.  

Therefore, both Arrival Time (AT) and Burst Time (BT) are considered to decide scheduling.

---

## 2. Shortest Job First (SJF) [Preemptive]

In this version, whenever a new process arrives in the ready queue with a BT shorter than the currently running process, the CPU is given to the new process by preempting the current one.  

This reduces starvation since short jobs get CPU quickly.  

There is no Convoy Effect because long jobs do not hold the CPU for too long.  

This algorithm results in a better average waiting time since short jobs are prioritized and executed sooner, reducing their waiting time.  

It schedules shorter jobs ahead of longer ones to optimize overall wait time.

---

## 3. Priority Scheduling [Non-preemptive]

In this scheduling, each process is assigned a priority when it is created.  

The CPU is always allocated to the process with the highest priority.  

If two processes have the same priority, the decision is based on arrival time.  

SJF scheduling can be seen as a special case of priority scheduling where priority is inversely proportional to burst time (i.e., smaller BT = higher priority).  

Once a process gets the CPU, it keeps it until it completes its execution.

---

## 4. Priority Scheduling [Preemptive]

In this version, if a new process arrives in the ready queue with a higher priority than the currently running process, the CPU is taken away from the current process and given to the new process.  

This approach can cause **indefinite waiting** or starvation, meaning low-priority processes may find it difficult to get CPU and might never execute.  

Starvation can occur in both preemptive and non-preemptive priority scheduling.  

**Solution:** The **Ageing** technique.  

In ageing, the longer a process waits, its priority gradually increases (for example, increasing priority by 1 every 15 minutes) so that eventually it gets CPU time.

---

## 5. Round Robin Scheduling (RR)

Round Robin is the most popular CPU scheduling algorithm, especially for time-sharing systems.  

It is similar to FCFS but preemptive.  

Each process is given a fixed time slice or **Time Quantum (TQ)** to use the CPU.  

If a process does not finish its work within this time quantum, the CPU is taken away from it and given to the next process in the ready queue.  

Scheduling is based on Arrival Time (AT) and Time Quantum (TQ), and it does not depend on burst time.  

No process waits indefinitely in Round Robin, so starvation is minimal.  

There is no Convoy Effect since every process gets an equal share of CPU time.  

It is easy to implement.  

However, if the time quantum is very small, too many context switches occur, causing overhead and slowing down the system.

---

## Summary

- **SJF Non-preemptive:** The shortest job runs first, but estimating BT is difficult and Convoy Effect can happen.  
- **SJF Preemptive:** The shortest job can take CPU anytime, reducing starvation and no Convoy Effect.  
- **Priority Scheduling Non-preemptive:** High priority runs first, but starvation can occur.  
- **Priority Scheduling Preemptive:** Higher priority jobs preempt current jobs, starvation is more severe, solved by ageing.  
- **Round Robin:** Every process gets fixed time slices, preemptive, minimal starvation, simple, but very small time quantum increases overhead.

---