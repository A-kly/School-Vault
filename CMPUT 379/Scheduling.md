# Introduction
![[Pasted image 20231030120140.png]]
# Policy versus Mechanism
![[Pasted image 20231030120200.png]]
## Policy: Examples
Checkout line for groceries
- All lines the same?
- 10 items or less line?
Bakery
- Take a number (priority)
Airline check-in
- Group people into zones (priorities)
- Higher priority preemption
Sports drills
- Go around a circle
# Basics
Scheduling refers to a set of *policies and mechanisms* to control the order of work to be performed by a computer system. Of all the resources of a computer system that are scheduled before use, the CPU is the far most important.
But, other criteria may be important too (e.g., memory).
Multiprogramming is the (efficient) scheduling of the CPU. The basic idea is to keep the CPU busy as much as possible by executing a (user) process until it must wait for an event and then switch to another process.
Processes alternate between consuming CPU cycles **(CPU-burst)** and performing I/O **(I/O-burst)**.
# Classification
![[Pasted image 20231030120412.png]]
- **CPU bound** = Mostly computing, low I/O
- **I/O bound** = mostly I/O, low CPU
**CPU bursts** are the “customers” (think of a person in line for checkout at a grocery store). We care about the *turnaround time of CPU bursts*. Should processes with short CPU bursts (i.e., I/O bound processes) be given priority in acquiring the CPU?
## How Do You Classify?
- Force the user to provide such information.
- The system may try to guess…
	- A process can change its performance characteristics over time.
	- Extrapolate the duration of the next CPU burst from the past history.
	- Use a *Simple Moving Average (MVA)*, the average over a time period
	- Use an *Exponential Moving Average (EMA)*, a dynamic average by decaying the value of older data points.
### SMA/EMA Example
![[Pasted image 20231030120644.png]]
# Types of Scheduling
In general, (job) scheduling is performed in three stages: short-, medium-, and long-term. The activity frequency of these stages are implied by their names.
**Long-term** (job) scheduling is done when *a new process is created*. The OS initiates processes and so controls the degree of multi-programming (number of processes in memory).
**Medium-term** scheduling involves *suspending or resuming processes by swapping* (defined later) them out of or into memory.
**Short-term** (process or CPU) scheduling *occurs most frequently and decides which process to execute next*.
## Life Cycle of a Typical Process
![[Pasted image 20231030121346.png]]
## Long- & Medium-Term Scheduling
Acting as the primary resource allocator, *the long-term scheduler admits more jobs when the resource utilization is low or blocks the incoming (batch) jobs from entering the ready queue otherwise*. 
When the main memory becomes over-committed, the *medium-term scheduler releases the memory of a suspended (blocked or stopped) process by swapping (rolling) it out*. 
In summary, ==both schedulers control the level of multiprogramming and avoid (as much as possible) overloading the system== by having many processes and causing "thrashing" (more on this later).
## Short-Term Scheduling
Short-term scheduler, also known as the process or CPU scheduler, *controls the CPU sharing among the ‘‘ready’’ processes*. The selection of a process to execute next is done by the short-term scheduler. Usually, a new process is selected under the following circumstances:
- When a process must wait for an event.
- When an event occurs (e.g., I/O completed, quantum expired).
- When a process terminates.
==The short-term scheduler must be fast==!
### Short-Term Scheduling Criteria
The goal of short-term scheduling is to optimize the system performance (e.g., high throughput), and yet provide responsive service (e.g., low latency). To achieve this goal, the following criteria are used:
- CPU utilization
- I/O device throughput
- Total service time (e.g., turnaround time)
- Responsiveness (e.g., for keystrokes)
- Fairness
- Deadlines (e.g., for real-time systems)
# Scheduler Design
A typical scheduler is designed to *select one or more primary performance criteria and rank them in order of importance*. One problem in selecting a set of performance criteria is that *they often conflict with each other*. For example, increased processor utilization is usually achieved by increasing the number of active processes, but then response time deteriorates. So, the design of a scheduler usually involves a careful balance of all requirements and constraints (i.e., trade-offs).
# Scheduler Performance Metrics
- **Turnaround time:** process entering the system to the time it completes execution (lower is better).
- **Waiting time:** total amount of time a process spends in the READY state (lower is better).
- **Throughput:** number of completed jobs per time period (higher is better).
==Getting the best performance for a scheduler does not necessarily mean getting the best result(s) for these metric(s).==

When do the above metrics give misleading results?
# Scheduling Policies
In general, scheduling policies may be **preemptive** or **non-preemptive**.
In a **non-preemptive** pure multiprogramming system, *the short-term scheduler lets the current process run until it blocks, waiting for an event or a resource, or it terminates*.
**Preemptive** policies, on the other hand, *force the currently active process to release the CPU on certain events, such as a clock interrupt, some 1/0 interrupts, or a system call*.

# Scheduling Algorithms
The following are some common scheduling algorithms:

| Non-preemptive                    | Preemptive                              |
| --------------------------------- | --------------------------------------- |
| First-Come-First-Served (FCFS)    | Round-Robin (RR)                        |
| Shortest Job First (SJF)          |                                         |
| Good for "background" batch jobs. | Good for "foreground" interactive jobs. |

## First-Come-First-Served (FCFS)
#COMEBACKTOTHIS ==Laptop is almost dead, may have to rewrite==
FCFS, also known as First-in-First-out (FIFO), *is the simplest scheduling policy*. *Arriving jobs are inserted at the tail (rear) of the ready queue and the process to be executed next is removed from the head (front) of the queue*.
FCFS performs *better for long jobs*. Relative importance of jobs measured only by arrival time (poor choice). A long CPU-bound job may hog the CPU and may force shorter (or 1/0-bound) jobs to wait prolonged periods. *This in turn may lead to a lengthy queue of ready jobs, the "convo effect"*.

## Priority-Based
