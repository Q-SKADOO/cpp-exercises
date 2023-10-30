```cpp
#include <iostream>
#include <bits/stdc++.h>
using namespace std;


//Failed to create a function to be used later in Main() to create the 3 matrices
//
/*
std::vector<double> matrixA(long m, long n)
{
        long** matrixa = new long*[m];
        for(long i=0; i<m; i++){
            matrixa[i] = new long[n];

                for(long j = 0; j < n; ++j)
                {
                        long random = 0 + (rand() % 11);
                        long random2 = 0 + (rand() % 11);

                        matrixa[i][j]= random, random2;
                        //cout << "a" << i << j << ": " << matrix_a[i][j] << "\t";
                }

        }


}

std::vector<double> matrixB(long m, long n)
{
        long** matrixb = new long*[m];
        for(long i=0; i<m; i++){
            matrixb[i] = new long[n];

                for(long j = 0; j < n; ++j)
                {
                        long random = 0 + (rand() % 11);
                        long random2 = 0 + (rand() % 11);

                        matrixb[i][j]= random, random2;
                        //cout << "a" << i << j << ": " << matrix_a[i][j] << "\t";
                }

        }

}


std::vector<double> matrixC(long m, long n)
{
        long** matrixc = new long*[m];
        for(long i=0; i<m; i++){
            matrixc[i] = new long[n];
        }

}
*/

int main()
{
    long r1, c1, r2, c2;

    //std::vector<long> b(1000)(1000);
    //std::vector<long> a(1000)(1000);


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

    long** matrixa = new long*[r1];
    for(long i=0; i<r1; i++){
            matrixa[i] = new long[c1];

                for(long j = 0; j < c1; ++j)
                {
                        long random = 0 + (rand() % 11);
                        long random2 = 0 + (rand() % 11);

                        matrixa[i][j]= random;
                        //cout << "a" << i << j << ": " << matrixa[i][j] << "\t";
                }
    }

    long** matrixb = new long*[r2];
    for(long i=0; i<r2; i++){
            matrixb[i] = new long[c2];

                for(long j = 0; j < c2; ++j)
                {
                        long random = 0 + (rand() % 11);
                        long random2 = 0 + (rand() % 11);

                        matrixb[i][j]= random;
                        //cout << "b" << i << j << ": " << matrixb[i][j] << "\t";
                }
    }

     long** matrixc = new long*[r1];
     for(long i=0; i<r1; i++){
            matrixc[i] = new long[c2];
        }



    // Matrix Multiplication
    //cout << "\nMultiplication of given two matrices is:\n";


    //long rslt[r1][c2];

    clock_t begin1 = clock();
    for (long i = 0; i < r1; i++) {
        for (long j = 0; j < c2; j++) {
            //rslt[j][k] = 0;

            for (long k = 0; k < r2; k++) {
                //rslt[i][j] = 0;
                matrixc[i][j] += matrixa[i][k] * matrixb[k][j];
            }

                //cout << matrix_c[i][j] << "\t";
        }

        //cout << endl;
    }
    clock_t end1 = clock();
    double time_taken = (double)(end1 - begin1) / CLOCKS_PER_SEC;
    printf("\n \nfunction took %f seconds to execute \n", time_taken);

    /*
    for (long i = 0; i < r1; i++) {
            for (long j = 0; j < c2; j++) {
                    cout << matrix_c[i][j] << "\t";
            }
    }
    */

    //Learned that you have to manually deallocate memory when using dynamic memory allocation
    for(long i=0;i<r1;i++){
            delete []matrixa[i];
            delete []matrixb[i];
            delete []matrixc[i];
    }

    delete []matrixa;
    delete []matrixb;
    delete []matrixc;

    return 0;


    }
```
