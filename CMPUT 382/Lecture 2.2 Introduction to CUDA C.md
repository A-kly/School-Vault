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