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
	- Universal turing machine takes in extra input of machine description to change what it does
		- Can have multiple 