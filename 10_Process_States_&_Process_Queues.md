**Process States and Process Queues**

When a process is being executed by an Operating System (OS), it goes through different phases called *process states*. These states reflect the current condition or activity of a process. The OS uses these states to manage and schedule processes efficiently.

---

### 1. Process States

#### a. New

* This is the initial state of a process.
* A program becomes a process and is about to be loaded into memory.
* The process has not yet been admitted into the pool of executable processes.

#### b. Ready

* The process is in main memory and is ready to run.
* It is waiting for CPU allocation.
* The process has everything it needs to execute but is in queue for CPU time.

#### c. Running

* The process is currently being executed by the CPU.
* Instructions of the process are actively being carried out.
* Only one process can be in the running state per CPU core.

#### d. Waiting

* The process is not eligible for CPU until some event completes.
* Usually waiting for input/output (I/O) operations.
* Once the I/O completes, it returns to the ready state.

#### e. Terminated

* The process has finished its execution.
* It is removed from the process table and no longer exists.

---

### 2. Process Queues

Due to the different states of a process, the OS maintains several queues to manage scheduling and execution.

#### a. Job Queue

* Contains all processes in the "new" state.
* These processes reside in secondary storage (like hard disks).
* The Long Term Scheduler (LTS) selects processes from this queue to bring them into main memory.

#### b. Ready Queue

* Contains all processes that are in memory and ready to execute.
* Managed by the Short Term Scheduler (STS).
* The STS selects one of these processes to assign to the CPU.

#### c. Waiting Queue

* Holds all the processes that are waiting for I/O operations to complete.
* Once I/O is done, these processes are moved back to the ready queue.

---

### 3. Degree of Multiprogramming

* Refers to the number of processes that are in memory at any given time.
* A higher degree means more processes are ready to execute, which increases CPU utilization.
* Managed by the Long Term Scheduler to avoid system overload.

---

### 4. Dispatcher

* A part of the OS responsible for handing over CPU control from one process to another.
* It performs context switching: saves the state of the old process and loads the state of the new one from its Process Control Block (PCB).
* Works closely with the Short Term Scheduler.

---

### Summary

* **Process States**: New, Ready, Running, Waiting, Terminated.
* **Process Queues**: Job Queue (new processes), Ready Queue (waiting for CPU), Waiting Queue (waiting for I/O).
* **Degree of Multiprogramming**: Number of processes in memory, controlled by LTS.
* **Dispatcher**: Responsible for switching CPU from one process to another via context switching.

Understanding these fundamental concepts helps in grasping how the OS schedules and manages multiple processes efficiently.

---