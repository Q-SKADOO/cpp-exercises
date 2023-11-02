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
    int r1, c1, r2, c2, t1, t2, t3;

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

    // we need MxN for each matrix
    t1 = r1 * c1;
    t2 = r2*c2;
    t3 = c1*r2;


    double** matrixa = new double*[1]; // This time we want a 1D array. So create one pointer to memory on heap instead of a column of pointers
    matrixa[0] = new double[c1*r1]; // This array has a length of MxN for the matrix. cblas_dgemm takes continuous memory
    for(int i=0; i<t1; i++){

                        double random = 0 + (rand() % 11);
                        double random2 = 0 + (rand() % 11);

                        matrixa[0][i]= random;
                       // cout << "a" << i  << ": " << matrixa[0][i] << "\t";
                }


    double** matrixb = new double*[1];
    matrixb[0] = new double[r2*c2];
    for(int i=0; i<t2; i++){


                        double random = 0 + (rand() % 11);
                        double random2 = 0 + (rand() % 11);

                        matrixb[0][i]= random;
                        //cout << "b" << i << ": " << matrixb[0][i] << "\t";
                }


    double** matrixc = new double*[1];
    matrixc[0] = new double[t3];




    // Matrix Multiplication
    //cout << "\nMultiplication of given two matrices is:\n";


   clock_t begin1 = clock();
   cblas_dgemm(CblasRowMajor, CblasNoTrans, CblasNoTrans,
           r1, c2, r2, 1.0, *matrixa, c1, *matrixb, c2, 0.0, *matrixc, c2);
   clock_t end1 = clock();
   double time_taken = (double)(end1 - begin1) / CLOCKS_PER_SEC;
   printf("\n \nfunction took %f seconds to execute. \n", time_taken);

   /*for(int i=0; i<t3; i++){
   cout << matrixc[0][i] << "\t";
   }*/

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
