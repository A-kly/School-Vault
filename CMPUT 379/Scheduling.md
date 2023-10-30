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
- **CPU bound**
**CPU bursts** are the “customers” (think of a person in line for checkout at a grocery store). We care about the *turnaround time of CPU bursts*. Should processes with short CPU bursts (i.e., I/O bound processes) be given priority in acquiring the CPU?
## How Do You Classify?
- Force the user to provide such information.
- The system may try to guess…
	- A process can change its performance characteristics over time.
	- Extrapolate the duration of the next CPU burst from the past history.
	- Use a Simple Moving Average (MVA), the average over a time period
	- Use an Exponential Moving Average (EMA), a dynamic average by decaying the value of older data points.