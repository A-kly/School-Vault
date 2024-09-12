![[Pasted image 20240906140850.png]]
# CPU
- Cpu has large cache in order to hide the slowness of dRAM
- SIMD - CPU has some of these, but not a lot, used for ALU add for example
# GPU
- GPU has smaller cache but way more registers, so we can move faster
- More SIMD to process more data per instruction

![[Pasted image 20240906141251.png]]
- Box 3 is SIMD unit 
	- SIMD = Single instruction multiple data
- PU = Processing unit.
	- Essentially a core
- GPU uses SIMD, instruction comes to a WARP (32 PUs), and is executed by all processors in the warp
	- The instruction pool dictates a thread. In order for each PU to compute different things, the data they work on must be different.
# Turing Machine
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
# Harvard Vs Von Neuman
![[Pasted image 20240906143336.png]]
- ROM is used for instructions memory rather than using RAM for that, this makes it easier for us to boot off of the ROM and access RAM only for data
- von Neuman slows down things due to address bus being used for both instructions and data
- **Each core in a modern cpu is it's own von Neuman (or harvard) machine**
# CPUs Are Latency Oriented Design
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
## RISC Vs CISC
### CISC Machine Architecture
![[Pasted image 20240906144320.png]]
- Complex instruction set computing (CISC) is a processor design where single instructions can execute several low-level operations (such as a load from memory, an arithmetic operation, and a memory store) or are capable of multi-step operations or addressing modes within single instructions  
- The term was retroactively coined in contrast to reduced instruction set computer (RISC) and has therefore become something of an umbrella term for everything that is not RISC, from large and complex mainframe computers to simplistic microcontrollers where memory load and store operations are not separated from arithmetic instructions CISC

### RISC Machine Architecture
![[Pasted image 20240906144518.png]]
- A RISC-based computer design approach means processors require fewer transistors than typical complex instruction set computing (CISC) x86 processors in most personal computers
- This approach reduces costs, heat and power use
- Such reductions are desirable traits for light, portable, battery-powered devices—including smartphones, laptops and tablet computers, and other embedded systems
- For Supercomputers, which consume large amounts of electricity, ARM could also be a power- efficient solution
- **Less transistors, less energy, slightly less powerful**
	- **ARM** Architecture is further reduced for simplicity

### Instructions
![[Pasted image 20240906144121.png]]
- CISC multiply instruction = Load+load+product+store RISC instructions
- RISC is more simple von Neuman architecture
### Compare
#### CISC
- Richer instruction set, some simple, some very complex.
- Instructions generally take more than 1 clock to execute.
- Instructions of a variable size.
- Instructions interface with memory in multiple mechanisms with complex addressing modes.
- **No pipelining**
- Upward compatibility within a family.
- Microcode control.
- Work well with simpler compiler.
#### RISC
- Simple primitive instructions and addressing modes.
- Instructions execute in one clock cycle.
- Uniformed length instructions and fixed instruction format.
- Instructions interface with memory via fixed mechanisms.
- Pipelining.
- Instruction set is orthogonal (little overlapping of instruction functionality)
- **Hardwired control**
- **Complexity pushed to the compiler**
# Computing Trends
## Moore's Law
![[Pasted image 20240910142025.png]]
- "Law" is slowing down and becoming less accurate
- We are limited by minimum size
	- ![[Pasted image 20240910142142.png]]
	- We run into limits and start hitting quantum limits
### 3D-Stacked CMOS Takes Moore’s Law to New Heights
![[Pasted image 20240910142246.png]]
- Uses 3d structures to pack more transistors vertically, increasing density
- Heat transfer may be an issue
![[Pasted image 20240910142331.png]]
#### Intel is Attempting 3d Moore's Law
![[Pasted image 20240910142408.png]]
https://www.intel.com/content/www/us/en/newsroom/resources/moores-law.html#gs.ew3shd
## NVIDIA's Huang's Law For GPUs
![[Pasted image 20240910142508.png]]
- Lots of calculation transistors, numbers increasing
# Key Ideas in High Throughput Processing
![](https://www.youtube.com/watch?v=bdYkznOFb2Y)
- **Superscalar:** We are processing more instructions at once by fetching, decoding, and executing more than one instruction at once.
- This only works when Instructions can be executed in parallel, avoiding data hazards.
- **SIMD:** has one fetch, and decode unit, but multiple ALUs that all do the same instruction, once per clock, on a bunch of separate data (vector instructions).
- These can be combined to further optimize execution.
- All of this is within a single thread of execution
	- One execution context
- We can expand this entire system to be multithreaded
- AND the entire system can be multicore
- **For a GPUs:**
	- hardware is given only vector threads, control logic determines if multiple instructions can be executed at the same time by different ALUs, 
# CPU Vs GPU
![[Pasted image 20240910142650.png]]
- CPUs devote lots of area to control and storage
- GPUs devote most area to computational units 
## Nvidia GPU view
![[Pasted image 20240910152702.png]]
- Each SM is contains a group of 32 CUDA cores
- Some neural network stuff
- Each core has registers
# GPUs: Throughput Oriented Design
![[Pasted image 20240910152920.png]]
- Details
	- Small caches
		- To boost memory throughput
	- Simple control
		- No branch prediction
		- No data forwarding
	- Energy efficient ALUs
		- Many, long latency but heavily pipelined for high throughput
	- Require massive number of threads to tolerate latencies
		- Threading logic
		- Thread state

## Understanding the V100 SM
![](https://www.youtube.com/watch?v=2cHKY6ZcEEM)
- The threads in a warp are executed in a SIMD manner if they share the same next instruction
## Hardware View of a CUDA Processor
![[Pasted image 20240910153911.png]]
- Each CUDA core = One ALU and a set of registers (PUs in this diagram)
- Shared memory is used to transfer data between cores
- Control unit tells many PUs to execute one instruction
- Large stack of 32 [[#The Von-Neumann Architecture|Von Neumann machine]]
- Single thread multiple data
- Small program executed on a batch of 32 cores. This is called WARP execution.
# Arrays of Parallel Threads\
![[Pasted image 20240910154657.png]]
- A CUDA kernel is executed by a **grid** (array) of threads
	- All threads in a grid run the same kernel code (Single Program Multiple Data)
	- Each thread has indexes that it uses to compute memory addresses and make control decisions
- **Instead of pointing to data in memory, we do pointer arithmetic but with threads using thread IDs**
- **Thread IDs are pointers to data in a thread's memory**
- ==**We address separate regions in memory by the formula called `i` in this example.**==
## Thread Blocks: Scalable Cooperation
![[Pasted image 20240910154738.png]]
- Divide thread array into multiple blocks
- Threads within a block cooperate via **shared memory**, **atomic operations** and **barrier synchronization**
- *Threads in different blocks do not interact*
## Threads and Blocks
![[Pasted image 20240910155532.png]]
- Threads are organized in blocks
- A grid is a collection of thread blocks of the same thread dimensionality which all execute the same kernel
- A block is executed by a multiprocessing unit
- The threads of a block can be identified (indexed) using 1Dimension(x), 2Dimensions (x,y) or 3Dim indexes (x,y,z)
- Blocks may be also indexed 1D, 2D or 3D.
- ***Grid* is made of data *blocks*, Each block is run on a *WARP* of CUDA *cores*, addressed by execution *Threads***
## Blocks Execute on an SM
![[Pasted image 20240910155840.png]]
# High Performance Applications Use Both CPU and GPU
- CPUs for sequential parts where latency matters
	- CPUs can be 10X+ faster than GPUs for sequential code
- GPUs for parallel parts where throughput wins
	- GPUs can be 10X+ faster than CPUs for parallel code
![[Pasted image 20240910155955.png]]
# NVIDIA GPU Roadmap
![[Pasted image 20240910160150.png]]
# NVIDIA H100 GPU
![[Pasted image 20240910160213.png]]
![[Pasted image 20240910160233.png]]
# AMD RDNA 2 Architecture
![[Pasted image 20240910160300.png]]
# CUDA Kernel and Thread Hierarchy
## VERY MUCH STRUGGLING TO UNDERSTAND THIS
- A CUDA kernel is executed by an array of threads
- All threads run the same code
- Each thread has an ID that it uses to compute memory addresses and make control decisions
![[Pasted image 20240911140835.png]]
- A thread is described by c/cuda code
- Each vector is associated with a thread, and executes code on vector elements
- kernel defines the code, grid size, and block size
- each kernel associated with one grid of data
	- description of How the threads are distributed, example (256x256 pixel image)
- each grid is divided into blocks
- Each SM is assigned typically 32 blocks
- Each Block uses up to 32 threads, with one PU per thread
- Each SM executes one block at a time and manages order
- SM divides each block into 32 in order to run on CUDA cores

# CUDA Threads Execution
![[Pasted image 20240911141747.png]]
- grey box aka thread is run on one SM