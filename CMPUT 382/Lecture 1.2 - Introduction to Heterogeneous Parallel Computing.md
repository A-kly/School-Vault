![[Pasted image 20240906140850.png]]
## CPU
- Cpu has large cache in order to hide the slowness of dRAM
- SIMD - CPU has some of these, but not a lot, used for ALU add for example
## GPU
- GPU has smaller cache but way more registers, so we can move faster
- More SIMD to process more data per instruction

![[Pasted image 20240906141251.png]]
- Box 3 is SIMD unit 
	- SIMD = Single instruction multiple data
- PU = Processing unit.
	- Essentially a core
# Turing machine
- Infinitely long strip of tape
	- head to read and store symbols on tape
- state machine used to move head and alter content of tape
	- Use state diagram to describe what the machine does
	- Halting state is used to stop program
- Can be made more abstract in order to generalize it
	- Has input, output, and program P to do this
	- new machine required for every computation
	- **Universal turing machine** takes in extra input of machine description to change what it does
		- Can have multiple machine descriptions (programs) to change what the machine does and chain together operations
# The Von-Neumann Architecture
![[Pasted image 20240906142459.png]]
- Tom scott Von-Neumann Architecture basics video
# Harvard vs von Neuman
![[Pasted image 20240906143336.png]]
- ROM is used for instructions memory rather than using RAM for that, this makes it easier for us to boot off of the ROM and access RAM only for data
- von Neuman slows down things due to address bus being used for both instructions and data
- **Each core in a modern cpu is it's own von Neuman (or harvard) machine**
# CPUs are Latency Oriented Design
![[Pasted image 20240906143847.png]]
- limited set of very powerful ALUs 
- most of silicon is used for cache, control and limited ALUs
- *one CPU core alu is faster than one cuda core alu*
# What is a CPU?
- Primary functions:
	- Fetching
	- Decoding
	- Executing
	- Writeback
- Two types of architectures:
	- Complex Instruction Set Computing (CISC)
		- eg. intel x86
	- Reduced Instruction Set Computing (RISC)
		- eg. arm
![[Pasted image 20240906144046.png]]
## RISC vs CISC 

### Instructions
![[Pasted image 20240906144121.png]]
- CISC multiply instruction = Load+load+product+store RISC instructions
- RISC is more simple von Neuman architecture