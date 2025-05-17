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