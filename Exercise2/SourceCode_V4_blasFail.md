```cpp
#include <iostream>
#include <bits/stdc++.h>
#include </share/modules/blas/3.8.0-8/include/cblas/cblas.h>
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
    int r1, c1, r2, c2;

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

    double** matrixa = new double*[r1];
    for(int i=0; i<r1; i++){
            matrixa[i] = new double[c1];

                for(int j = 0; j < c1; ++j)
                {
                        double random = 0 + (rand() % 11);
                        double random2 = 0 + (rand() % 11);

                        matrixa[i][j]= random;
                        //cout << "a" << i << j << ": " << matrixa[i][j] << "\t";
                }
    }

    double** matrixb = new double*[r2];
    for(int i=0; i<r2; i++){
            matrixb[i] = new double[c2];

                for(int j = 0; j < c2; ++j)
                {
                        double random = 0 + (rand() % 11);
                        double random2 = 0 + (rand() % 11);

                        matrixb[i][j]= random;
                        //cout << "b" << i << j << ": " << matrixb[i][j] << "\t";
                }
    }

    double** matrixc = new double*[r1];
    for(int i=0; i<r1; i++){
           matrixc[i] = new double[c2];
       }



    // Matrix Multiplication
    //cout << "\nMultiplication of given two matrices is:\n";


   clock_t begin1 = clock();
   cblas_dgemm(CblasRowMajor, CblasNoTrans, CblasNoTrans,
           r1, c2, r2, 1.0, *matrixa, c1, *matrixb, c2, 0.0, *matrixc, c2);
   clock_t end1 = clock();
   double time_taken = (double)(end1 - begin1) / CLOCKS_PER_SEC;
   printf("\n \nfunction took %f seconds to execute. \n", time_taken);


   //Learned that you have to manually deallocate memory when using dynamic memory allocation
    for(int i=0;i<r1;i++){
            delete []matrixa[i];
            delete []matrixb[i];
            delete []matrixc[i];
    }

    delete []matrixa;
    delete []matrixb;
    delete []matrixc;

    printf("\n \nCode fails after the delete statements \n");
    return 0;


    }
```
