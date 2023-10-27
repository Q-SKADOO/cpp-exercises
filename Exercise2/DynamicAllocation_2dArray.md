# How to Allocate 2D Array Dynamically

## Correct way to allocate 1D array

```cpp
new int[5]
```

So one would assume that for 2D:

```cpp
new int[10][20]
```

but the above is incorrect

```cpp
int** p = new int* [10]
```

This creates an array of interger pointers

Then need to create an array at each address for the interger pointers

```cpp
p[0] = new int[20];
p[1] = new int[20];
.
.
.
```


Of course, instead of creating arrays one by one, we would do this within a loop.

To add all of this together:

```cpp
int** p = new int*[10]; //Create integer pointer with each index storing address of an array. The 8 byte double pointer is on the stack, stores address of first element of interger pointer sitting on heap
for(i = 0; i<10; i++){
p[i] = new int[20]; // Creates the arrays at each element of the interger pointer
}

This is how to create 2D array dynamically
