# Dynamic Memory Allocation

## Key Terms
* Fixed Size Array
* Variable Sized Array
* Stack
* Heap


## Fixed Size v.s. Variable Sized Array
int a[50] - fixed sized
The 50 indicates a fixed size

int n; cin >> n; or int a[n] -> represent a variable sized array

Cons of variable sized array:
May not work on all compilers
Value is given by user at runtime

Pros of Fixed size array:
We know how much memory is required at compile time

## Two Types of Memory Allocation
Stack and heap

### Stack
Stack is small and heap is big as compared

int i = 10 or int a[20] would get allocated to the stack.

even large arrays such as int a[10,000] it is still sent to stack but at compile time it allocates a bigger stack memory

However with int a[n] at compile time a stack is not created large enough to handle an n value such as 10^6 so the stack will not have enough memory for such a big array

### Heap
Also called Dynamic Memory Allocation

Stack is static allocation (Memory allocated during compile time only)

Heap is runtime memory allocation - int a[n] is not the right syntax for dynamic allocation

The keyword new assigns 4 bytes on the heap. And also returns the address of these 4 bytes

int* i = new int;

This syntax allows you to point to this address and insert values

```cpp
int main(){
  int *p = new int; // 8 bytes on stack, 4 bytes on heap
  *p = 10;
  cout<<p<<endl;
  cout<<*p<<endl;
  return 0
}
```

p outputs the address on the heap
*p outputs the value

Same can be done for 
```cpp
  double *d = new double;
  char *c = new char;
```

If I wanted to take a user input and properly allocate memory, regardless of size
```cpp
int n;
cin>>n;
int *a = new int[n];
```

## Issues with Fixed Array and User Input
### Static Allocation of Large Array but Small N Requested
```cpp
int a[1000];
int n;
cin>>n;
for (i = 0; i<n; i++){
  cin>>a[i];
}
```
If user request n = 10, then 990 spaces are wasted. This equates to 990*4 bytes of space wasted.

### Static Allocation of Array but N Requested is Larger than Array
```cpp
int a[10];
int n;
cin>>n;
for (i = 0; i<n; i++){
cin>>a[i]
}
```
Causes crash

Dynamic memory allocation avoids these two issues.

## How to Put Elements Inside of The Array After Dynamic Memory Allocation
for example:
int *a = new int[n]
a[0] = 10
a[20] = 40

The pointer *a is stored on the stack and points to the first element of the array on the heap
a[i] = *(a+i)

These values get stored at the address on the heap

### Find The largest Element in Array
int *a = new int[n]; //heap has 4 bytes per element. The pointer *a takes up 4 bytes on Stack
for (int i = o; i<n; i++){
  cin>>a[i]; //user setting value of each element in array
}

int Largest = -1;
for (int i = 0; i<n; i++){
  if(a[i] > Largest)(
    Largest = a[i];
    }
  }
cout<<Largest<<endl;

return 0;


main();
if()
{ int i;
}

This is static allocation. When the last bracket is reached aka the scope of i finishes and its memory gets deallocated.
So i is present inside the stack then gets deleted automatically

Dynamic Allocation this is not the case
if()
{int *i = new int i}
The *i does not have a scope. THis is heap or dynamic memory allocation so does not get deleted


Static
Releases based on scope

Dynamic
No concept of scope. So have to manually release the memory.

Example

while (true)
{
int i;
}

In the static case, the 4 bytes are allocated on the stack then as we traverse through the loop the 4 bytes are deallocated then allocated again once we reach int i again. This repeats itself through the life of the loop. At max using 4 bytes of memory.

while (true)
{
int *a = new int;
}

In the dynamic case, the 8 bytes are allocated on the stack and 4 bytes are allocated on the heap. The 8 bytes of memory on the stack gets deallocated but Since the memory is not manually deallocated, this process continues where 4 bytes are allocated to heap each cycle of the loop. Memory usage increases and at some point the program will crash.

## Ways To Delete
Single Element Deletion
delete p;

Array Deletion
delete []p;



