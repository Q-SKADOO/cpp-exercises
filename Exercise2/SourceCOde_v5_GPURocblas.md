```cpp
#include <iostream>
#include <bits/stdc++.h>
#include <cstdlib>
#include </opt/rocm-5.7.0/include/rocblas/rocblas.h>
//#include <rocblas/rocblas.h>
#include </opt/rocm-5.7.0/include/hip/hip_runtime.h>
//#include <cblas.h>
using namespace std;


//Failed to create a function to be used later in Main() to create the 3 matrices
//
/*
std::vector<double> matrixA(double m, long n)
{
        double** matrixa = new long*[m];
        for(double i=0; i<m; i++){
            matrixa[i] = new double[n];

                for(double j = 0; j < n; ++j)
                {
                        double random = 0 + (rand() % 11);
                        double random2 = 0 + (rand() % 11);

                        matrixa[i][j]= random, random2;
                        //cout << "a" << i << j << ": " << matrix_a[i][j] << "\t";
                }

        }


}

std::vector<double> matrixB(double m, long n)
{
        double** matrixb = new long*[m];
        for(double i=0; i<m; i++){
            matrixb[i] = new double[n];

                for(double j = 0; j < n; ++j)
                {
                        double random = 0 + (rand() % 11);
                        double random2 = 0 + (rand() % 11);

                        matrixb[i][j]= random, random2;
                        //cout << "a" << i << j << ": " << matrix_a[i][j] << "\t";
                }

        }

}


std::vector<double> matrixC(double m, long n)
{
        double** matrixc = new long*[m];
        for(double i=0; i<m; i++){
            matrixc[i] = new double[n];
        }

}
*/

int main()
{
    rocblas_int r1, c1, r2, c2, t1, t2, t3; //using rocblas_int

    rocblas_handle test_handle;
    rocblas_create_handle(&test_handle);

    //std::vector<double> b(1000)(1000);
    //std::vector<double> a(1000)(1000);


    cout << "Enter rows and columns for first matrix: ";
    cin >> r1 >> c1;
    cout << "Enter rows and columns for second matrix: ";
    cin >> r2 >> c2;

    // If column of first matrix in not equal to row of second matrix,
    // ask the user to enter the size of matrix again.
    while (c1!=r2)
    {
        cout << "Error! column of first matrix not equal to row of second.";

        cout << "Enter rows and columns for first matrix: ";
        cin >> r1 >> c1;

        cout << "Enter rows and columns for second matrix: ";
        cin >> r2 >> c2;

    }


    t1 = r1 * c1;
    t2 = r2*c2;
    t3 = c1*r2;


    double** matrixa = new double*[1];
    matrixa[0] = new double[t1];
    for(int i=0; i<t1; i++){

                        double random = 0 + (rand() % 11);
                        double random2 = 0 + (rand() % 11);

                        matrixa[0][i]= random;
                        //cout << "a" << i  << ": " << matrixa[0][i] << "\t";
                }


    double** matrixb = new double*[1];
    matrixb[0] = new double[t2];
    for(int i=0; i<t2; i++){


                        double random = 0 + (rand() % 11);
                        double random2 = 0 + (rand() % 11);

                        matrixb[0][i]= random;
                        //cout << "b" << i << ": " << matrixb[0][i] << "\t";
                }


    double* d_matrixa, *d_matrixb, *d_matrixc;



    // Matrix Multiplication
    //cout << "\nMultiplication of given two matrices is:\n";

 // Allocate memory on the GPU
    hipMalloc(&d_matrixa, t1 * sizeof(double));
    hipMalloc(&d_matrixb, t2 * sizeof(double));
    hipMalloc(&d_matrixc, t3 * sizeof(double));

    // Copy data from CPU to GPU
    hipMemcpy(d_matrixa, h_matrixa, t1 * sizeof(double), hipMemcpyHostToDevice);
    hipMemcpy(d_matrixb, h_matrixb, t2 * sizeof(double), hipMemcpyHostToDevice);


   //rocblas manual
   /*rocblas_dgemm(rocblas_handle handle, rocblas_operation transa, rocblas_operation
                   transb, rocblas_int m, rocblas_int n, rocblas_int k, const double *alpha, const double *A, rocblas_int lda, const double *B, rocblas_int
                   ldb, const double *beta, double *C, rocblas_int ldc)*/
   /* Parameters
• handle: rocblas_handle. handle to the rocblas library context queue.
• transA: rocblas_operation specifies the form of op( A )
• transB: rocblas_operation specifies the form of op( B )
• m: rocblas_int.
• n: rocblas_int.
• k: rocblas_int.
• alpha: specifies the scalar alpha.
• A: pointer storing matrix A on the GPU.
• lda: rocblas_int specifies the leading dimension of A.
• B: pointer storing matrix B on the GPU.
• ldb: rocblas_int specifies the leading dimension of B.
• beta: specifies the scalar beta.
• C: pointer storing matrix C on the GPU.
• ldc: rocblas_int specifies the leading dimension of C.
*/

   double hA = 1.0;
   const double* ha = &hA;
   double hC = 0.0;
   const double* hc = &hC;

   clock_t begin1 = clock();
   rocblas_dgemm(test_handle, rocblas_operation_none, rocblas_operation_none,
           r1, c2, r2, ha, *matrixa, c1, *matrixb, c2, hc, *matrixc, c2);
   clock_t end1 = clock();
   double time_taken = (double)(end1 - begin1) / CLOCKS_PER_SEC;
   printf("\n \nfunction took %f seconds to execute. \n", time_taken);

   /* for(int i=0; i<t3; i++){
   cout << matrixc[0][i] << "\t";
   } */

    // Copy the result back from GPU to CPU
    hipMemcpy(h_matrixc, d_matrixc, t3 * sizeof(double), hipMemcpyDeviceToHost);

    // Free GPU memory and destroy ROCBLAS handle
    hipFree(d_matrixa);
    hipFree(d_matrixb);
    hipFree(d_matrixc);
   rocblas_destroy_handle(test_handle);

   //Learned that you have to manually deallocate memory when using dynamic memory allocation

    delete []matrixa[0];
    delete []matrixb[0];
    delete []matrixc[0];


    delete []matrixa;
    delete []matrixb;
    delete []matrixc;

    printf("\n \nCode finally successful after the delete statements \n");
    return 0;


    }
```
