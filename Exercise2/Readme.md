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
* M_DIM: 1000 Time-of-Execution j-k-i: 2.99s i-j-k: 2.74s ------ M_DIM: 2000 Time-of-Execution j-k-i: 49.54s i-j-k: 38.83s
* Thought: Online i've seen people mention cache misses depending on which loop is nested i vs j
* Also "It is well known that j-k-i loop nest is optimal in this situation. " Needs personal investigating to determine current loop structure vs "optimal" then performance evaluation
* Performance is affected when the max dimension of the double array is bigger than what is asked for.

## Source Code V4: Things learned
* How to dynamically allocate memory
* Differences between stack and heap
* The matrix multiplication is slower in this version (https://stackoverflow.com/questions/2264969/why-is-memory-allocation-on-heap-much-slower-than-on-stack)
* The management of a stack only involves the instruction and registers (SP, BP), which is naturally/purely hardware in a sense.
* While for a heap, it further involves complex software data structures and algorithms, which involves function calling (again stack involved), memory access, etc.
* M_DIM: 2000 Time-of-Execution 81.5s vs 38.83s (V4 code)

### To do 10/27
* Figure out how to use math libraries when compiling code
* Outfit code to run on gpu
* Create script to record dimension size vs time of execution

