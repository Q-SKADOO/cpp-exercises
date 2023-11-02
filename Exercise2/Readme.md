## Exercise 2

### Matrix Multiplication

#### Tasks
* Fill with random values (FP32)
* Reference calculations with library
* Can use mkl or blas or cublas
* Write matrix multiplication
* Time of execution by reference
* TIme of execution by my implementation


Square Matrix Multiplication

![image](https://github.com/Q-SKADOO/cpp-exercises/assets/112571800/bcc31ad2-3237-46e1-892e-f7dd9ebc2b5a)


Thoughts:
* Have user enter the size of the matrix
* Random number generator to fill the matrices
* Print the two matrices
* Print the final product
* Implement timing

## Source Code V1: Things learned
* The current way that the double array is create takes up space on the stack which leads to seg faults. Works fine for smaller sizes but blows up for larger dimensions. long a[10][10], b[10][10] is initialized just inside of main()
* This is due to the variables being stored on what is called the "stack". There is another called "heap".
* Note for Q: Refer to the udemy lesson on memory allocation then come back to update this section.

## Source Code V2: Things learned
* Now the double arrays are initialized globally before main(): long matrix_a[MAXDIM][MAXDIM], matrix_b[MAXDIM][MAXDIM];
* The size of the matrices are defined before main as well using a define directive: #define MAXDIM 1000
* Thought: Online i've seen people mention cache misses depending on which loop is nested i vs j
* Also "It is well known that j-k-i loop nest is optimal in this situation. " Needs personal investigating to determine current loop structure vs "optimal" then performance evaluation
* Performance is affected when the max dimension of the double array is bigger than what is asked for.

## Source Code V3: Things learned
* How do you know that there is a cache miss? And what exactly is that?
* The i-j-k loop is faster than the originally j-k-i construct
* M_DIM: 1000 Time-of-Execution j-k-i: 3.22s i-j-k: 2.91s ------ M_DIM: 2000 Time-of-Execution j-k-i: 48.94s i-j-k: 41.05s i-k-j: 21.5s j-i-k: 24.08 k-i-j: 22.17s k-j-i: 48.5s
* Thought: Online i've seen people mention cache misses depending on which loop is nested i vs j
* Also "It is well known that j-k-i loop nest is optimal in this situation. " Needs personal investigating to determine current loop structure vs "optimal" then performance evaluation
* Performance is affected when the max dimension of the double array is bigger than what is asked for.

## Source Code V4: Things learned
* How to dynamically allocate memory
* Differences between stack and heap
* The matrix multiplication is slower in this version (https://stackoverflow.com/questions/2264969/why-is-memory-allocation-on-heap-much-slower-than-on-stack)
* The management of a stack only involves the instruction and registers (SP, BP), which is naturally/purely hardware in a sense.
* While for a heap, it further involves complex software data structures and algorithms, which involves function calling (again stack involved), memory access, etc.
* M_DIM: 2000 Time-of-Execution 81.5s vs 41.05s (V3 code)
* UPDATE: using i-k-j the new fastest time for V3 is 21.5s and for dynamic memory allocation 38.2s. Dynamic memory allocation is still slower than have the array on the stack or global

### V4 Math Libraries: Things Learned
* Be sure that the CPU used is the same. saw increase in speed from 81.5s to 37s which if not realized would have been attributed to my attempt at calling math libraries.
* Used `module load blas` then at the `-lblas` flag in an attempt to implement blas. No changes to V4 code made. Not sure if this is correct or will work.
* M-DIM: 2000 Time-of-Execution 81.5s vs 82.47s (V4 no-blas vs blas)
* Used `module load lapack` then at the `-llapack` flag in an attempt to implement blas. No changes to V4 code made. Not sure if this is correct or will work.
* M-DIM: 2000 Time-of-Execution 81.5s vs 82.88 (V4 no-lapack vs lapack)
* Loaded both modules and their flags for compiling. No changes to V4 code made. Not sure if this is correct or will work.
* M-DIM: 2000 Time-of-Execution 81.5s vs 82.53 (V4 no-libray vs blas/lapack)
* As of 10/30 this is a fail. How to implement math libraries???
* Attempt #2: Adding cblas.h (#include </share/modules/blas/3.8.0-8/include/cblas/cblas.h>) to the .cpp file does nothing. 82.02s
* 11/2/203: `-lcblas` is needed when compiling. It is correct to include the cblas.h file. HOWEVER, one must use the `cblas_dgemm` function to actually call blas for the matrix matrix multiplication
* NOW the code works. `SourceCode_V4_blasFail` A speed up is seen to where the Time-of-Execution is 6.27s.
* Problem: After cblas_dgemm we are hit with different errors - `double free or corruption (!prev) / Aborted (core dumped)` or `free(): invalid pointer`
* Solution: `SourceCode_V4_blasSuccess` cblas_dgemm takes the matrix as continuous memory aka 1D array so the code is outfitted to dynamically allocate space on the stack that points to memory on heap. Then create a 1D array that is of length: MxN for each matrix A, B, and C with C being empty . And we construct it as RowMajor.
* Time-of-Execution: 5.5s
* Also validated that the results are correct by testing on a 2x2 matrix


### To do 11/2
* Figure out how to use math libraries when compiling code
* Outfit code to run on gpu 
* Create script to record dimension size vs time of execution

