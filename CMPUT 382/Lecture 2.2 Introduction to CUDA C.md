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
