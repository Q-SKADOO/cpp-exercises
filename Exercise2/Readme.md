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
* The current way that the double array is create takes up space on the stack which leads to seg faults
