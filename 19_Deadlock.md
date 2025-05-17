# The Dining Philosophers Problem

## 1. Problem Setup

The problem involves a total of 5 philosophers.

These philosophers live in only two states:  
- Thinking  
- Eating

## 2. Table and Forks Arrangement

The 5 philosophers sit around a circular table, each having one chair.

In the center of the table is a bowl containing noodles.

There are 5 forks placed on the table, one between each pair of philosophers, making a total of 5 forks.

## 3. Philosopher’s States

- **Thinking State:** When a philosopher is thinking, they do not interact with others and are lost in their thoughts.

- **Eating State:** When a philosopher feels hungry, they want to eat. To eat, they need both the forks on their left and right sides.

## 4. Use of Forks

A philosopher can only eat if they pick up both adjacent forks (left and right) simultaneously.

However, they can only pick up one fork at a time.

If a fork is already held by another philosopher, it cannot be taken.

Once the philosopher has both forks, they eat without putting down the forks.

## 5. Main Conflict in the Problem

If all philosophers simultaneously pick up their left fork, then each will have only one fork.

Then, everyone waits for the right fork, which is already held by their neighbor.

As a result, none of the philosophers can pick up both forks, leading to a deadlock where all wait indefinitely without making progress.

## 6. Solution Using Semaphores

Each fork is treated as a binary semaphore initialized to 1 (fork available).

When a philosopher picks up a fork, they perform a `wait()` operation on that fork’s semaphore (making its value 0, meaning the fork is in use).

When a philosopher finishes eating, they perform a `signal()` operation to release the fork (making the semaphore value 1 again).

Fork semaphores can be defined as:  
`Semaphore fork[5] = {1, 1, 1, 1, 1};`

## 7. Deadlock Problem

The semaphore solution ensures that two adjacent philosophers cannot eat simultaneously because forks are shared.

However, deadlock can still occur if all philosophers pick up their left fork simultaneously.

In this scenario, all fork semaphores become 0 (all forks taken).

No philosopher can pick up their right fork, as it is already held by their neighbor.

Consequently, all philosophers wait indefinitely — a deadlock.

## 8. Ways to Avoid Deadlock

To prevent deadlock, additional rules or methods need to be used; semaphores alone are not enough.

### 8.a) Allow At Most 4 Philosophers to Sit Simultaneously

Only allow a maximum of 4 philosophers to sit at the table at the same time.

This ensures that at least one fork remains free, preventing deadlock.

### 8.b) Pick Up Both Forks Together (Atomic Operation)

A philosopher should pick up both forks only when both are available.

This means acquiring both forks atomically (in one atomic step).

This requires creating a critical section where both forks are checked and acquired together.

### 8.c) Odd-Even Rule

Divide philosophers into two groups: odd-numbered and even-numbered.

Odd philosophers pick up their left fork first, then the right fork.

Even philosophers pick up their right fork first, then the left fork.

This reduces the chance of deadlock because not all philosophers try to pick up the same fork first.

## 9. Summary

The Dining Philosophers Problem is a classic example of concurrency and synchronization, showing how multiple threads/processes access shared resources (forks).

Using only semaphores is not sufficient because they do not prevent deadlock without additional logic.

To avoid deadlock, extra rules such as limiting the number of philosophers, atomic acquisition of forks, and the odd-even rule are used.

Together, these techniques provide a deadlock-free and synchronized solution.

---

## Deadlock Avoidance (How to Avoid Deadlock)

Deadlock avoidance means that the system knows in advance which resources each process will need during its lifetime. In other words, the kernel has prior information about what resources each process will request.

This helps the system to decide whether:

- The resource request should be granted immediately, or
- The process should wait a little to avoid deadlock.

To make this decision, the system needs to keep track of three things:

1. How many resources are currently available (free).
2. How many resources are currently allocated to each process.
3. How many more resources each process might request in the future and when they will release them.

### Core Idea of Deadlock Avoidance

a) The system schedules processes and their resource allocation in such a way that deadlock does not occur.

b) **Safe State**:  
The system is in a safe state if it can allocate the maximum required resources to every process without causing a deadlock.  
This means the system has a safe sequence — an order of process execution where each process gets the resources it needs, completes its task, and releases resources for the next process.

c) **Unsafe State**:  
When the system cannot guarantee that deadlock will not occur, it is said to be in an unsafe state.  
An unsafe state means there is a risk of deadlock, but deadlock may or may not actually happen.

d) The system only approves resource requests that keep it in a safe state. If it cannot fulfill a request safely, it asks the process to wait.

---

## Banker’s Algorithm (A Deadlock Avoidance Algorithm)

The Banker’s Algorithm is a scheduling method that allocates resources to processes in a way that prevents deadlocks.

- When a process requests resources, the system checks if granting the request keeps the system in a safe state.
- If yes, the request is approved.
- If no, the process must wait until enough resources are available.

The name "Banker’s Algorithm" comes from banking: a bank only grants a loan if it is sure the money will be paid back; otherwise, it denies the loan.

---

## Deadlock Detection (When Deadlock Prevention or Avoidance is Not Used)

If a system does not use deadlock prevention or avoidance, it must detect deadlocks and then recover from them.

The system periodically checks whether a deadlock has occurred using:

### a) Single Instance of Each Resource Type — Wait-for Graph Method

- A graph is created where each node is a process.
- An edge from process P1 to process P2 means P1 is waiting for a resource held by P2.
- Deadlock occurs if there is a cycle in this graph.
- The system scans the graph for cycles periodically. If a cycle is found, deadlock exists.

### b) Multiple Instances of Each Resource Type

- In this case, the Banker’s Algorithm is used to detect deadlock.

---

## Recovery from Deadlock (How to Get Out of Deadlock)

Once deadlock is detected, the system must recover by:

### a) Process Termination

- Abort all deadlocked processes, or
- Abort processes one by one until the deadlock cycle is broken.

### b) Resource Preemption

- Forcefully take resources from some processes and give them to others.
- Continue transferring resources until the deadlock is resolved.

---

## Summary

Deadlock avoidance requires prior knowledge of processes’ resource needs to ensure the system stays in a safe state.

The Banker’s Algorithm is a popular method that checks the system’s safety before granting resource requests.

If deadlock is not avoided, the system must detect it using methods like the wait-for graph or Banker’s Algorithm.

After detection, deadlock is resolved either by terminating processes or by preempting resources.

---

