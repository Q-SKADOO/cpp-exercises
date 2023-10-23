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

##Source Code V1: Things learned
* The current way that the double array is create takes up space on the stack which leads to seg faults. Works fine for smaller sizes but blows up for larger dimensions. long a[10][10], b[10][10] is initialized just inside of main()
* This is due to the variables being stored on what is called the "stack". There is another called "heap".
* Note for Q: Refer to the udemy lesson on memory allocation then come back to update this section.

##Source Code V2: Things learned
* Now the double arrays are initialized globally before main(): long matrix_a[MAXDIM][MAXDIM], matrix_b[MAXDIM][MAXDIM];
* The size of the matrices are defined before main as well using a define directive: #define MAXDIM 1000
* Thought: Online i've seen people mention cache misses depending on which loop is nested i vs j
* Also "It is well known that j-k-i loop nest is optimal in this situation. " Needs personal investigating to determine current loop structure vs "optimal" then performance evaluation

###To do 10/23
* Understand memory allocation strategies i.e. stack vs heap then discuss in readMe
* Investigate j-k-i loop construct
* Create script to record dimension size vs time of execution

