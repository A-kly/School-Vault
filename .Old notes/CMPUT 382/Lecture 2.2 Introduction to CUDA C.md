# Vector Addition – Traditional C Code
```C
// Compute vector sum C = A + B
void vecAdd(float *h_A, float *h_B, float *h_C, int n)
{
	int i;
	for (i = 0; i<n; i++) h_C[i] = h_A[i] + h_B[i];
}
int main()
{
	// Memory allocation for h_A, h_B, and h_C
	// I/O to read h_A and h_B, N elements
	…
	vecAdd(h_A, h_B, h_C, N);
}
```
This code does this in C:
![[Pasted image 20240913140634.png]]
# Heterogeneous Computing vecAdd CUDA Host Code
![[Pasted image 20240913140757.png]]
- Transfering data between memory kinds
```C
#include <cuda.h>
void vecAdd(float *h_A, float *h_B, float *h_C, int n)
{
	int size = n* sizeof(float);
	float *d_A, *d_B, *d_C;
	// Part 1
		// Allocate device memory for A, B, and C
		// copy A and B to device memory
	// Part 2
		// Kernel launch code – the device performs the actual vector addition
	// Part 3
		// copy C from the device memory
		// Free device vectors
}
```
## Partial Overview of CUDA Memories
![[Pasted image 20240913140917.png]]
- Grid of data is broken into blocks, which threads get executed on

- Device code can:
	- R/W per-thread registers
	- R/W all-shared globalmemory
- Host code can:
	- Transfer data to/from per grid global memory
## CUDA Device Memory Management API functions
- cudaMalloc()
	- Allocates an object in the device global memory
	- Two parameters
		- Address of a pointer to the allocated object
		- Size of allocated object in terms of bytes
- cudaFree()
	- Frees object from device global memory
	- One parameter
		- Pointer to freed object
- cudaMemcpy()
	- memory data transfer
	- Requires four parameters
		- Pointer to destination
		- Pointer to source
		- Number of bytes copied
		- Type/Direction of transfer
- Transfer to device is asynchronous
# Vector Addition Host Code (in cpu)
```c
void vecAdd(float *h_A, float *h_B, float *h_C, int n)
{
	int size = n * sizeof(float); float *d_A, *d_B, *d_C;
	cudaMalloc((void **) &d_A, size);
	cudaMemcpy(d_A, h_A, size, cudaMemcpyHostToDevice);
	cudaMalloc((void **) &d_B, size);
	cudaMemcpy(d_B, h_B, size, cudaMemcpyHostToDevice);
	cudaMalloc((void **) &d_C, size);
	// Kernel invocation code – to be shown later
	cudaMemcpy(h_C, d_C, size, cudaMemcpyDeviceToHost);
	cudaFree(d_A); cudaFree(d_B); cudaFree (d_C);
}
```
- d_x = device vector (GPU)
- h_x = host vector (CPU)
## In Practice, Check for API Errors in Host Code
```c
cudaError_t err = cudaMalloc((void **) &d_A, size);
if (err != cudaSuccess) {
	printf(“%s in %s at line %d\n”, cudaGetErrorString(err), __FILE__, __LINE__);
	exit(EXIT_FAILURE);
}
```
# Threads and Kernel Functions
- Heterogeneous host (CPU) + device (GPU) application C program
	- Serial parts in host C code
	- Parallel parts in device Single Program Multiple Data (SPMD) kernel code
	- **Each SM computes a block, sequentially in groups of 32**

![[Pasted image 20240913141554.png]]
- nBlk = **Number of blocks**
- nTid = **Number of threads**
## Example: Vector Addition Kernel
**Device Code**
- THIS CODE RUNS ON GPU
```c
// Compute vector sum C = A + B
// Each thread performs one pair-wise addition
__global__ //THIS INDICATES THAT THIS RUNS ON THE GPU
void vecAddKernel(float* A, float* B, float* C, int n)
{
	int i = threadIdx.x+blockDim.x*blockIdx.x;
	if(i<n) C[i] = A[i] + B[i];
}
```
- The line `int i = threadIdx.x+blockDim.x*blockIdx.x;` is used to determine where in memory we are retrieving data
	- 
## Example: Vector Addition Kernel Launch (Host Code)
**Host Code**
- THIS CODE RUNS ON CPU
```c
void vecAdd(float* h_A, float* h_B, float* h_C, int n)
{
	// d_A, d_B, d_C allocations and copies omitted
	// Run ceil(n/256.0) blocks of 256 threads each
	vecAddKernel<<<ceil(n/256.0),256>>>(d_A, d_B, d_C, n);
}
```
- Best way to think is that every element in the array has a block ID associated with it
- `ceil(n/256.0),256` =256 warp per block
## Kernel execution in a nutshell
![[Pasted image 20240913142330.png]]
# CUDA Function Declarations
![[Pasted image 20240913142512.png]]
# Arrays of Parallel Threads
- A CUDA kernel is executed by a grid (array) of threads
	- All threads in a grid run the same kernel code (Single Program Multiple Data)
	- Each thread has indexes that it uses to compute memory addresses and make control decisions
	- ![[Pasted image 20240923133800.png]]
## Threads blocks are scalable
- Divide thread array into multiple blocks
	- Threads within a block cooperate via shared memory, *atomic operations and barrier synchronization*
	- Threads in different blocks do not interact
# ==I hope that it will be easier to follow this class by watching lectures without taking notes, or taking minimal ones, and not copying slides. I'm starting that now
