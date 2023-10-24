```cpp
#include <iostream>
#include <bits/stdc++.h>
using namespace std;

// DEFINES ---------------------------------------------------------------------
#define MAXDIM 2000

// VARIABLES -------------------------------------------------------------------
long matrix_a[MAXDIM][MAXDIM], matrix_b[MAXDIM][MAXDIM], matrix_c[MAXDIM][MAXDIM];

int main()
{
    long r1, c1, r2, c2, i, j, k;

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

    //Random number generator to populate matrices
    //
    // Providing a seed value - Commented out for testing purposes (Consistent numbers without seed)
        /* srand((unsigned) time(NULL)); */

    //Populating matrix A
    for(i = 0; i < r1; ++i)
        for(j = 0; j < c1; ++j)
        {
            long random = 0 + (rand() % 11);
            long random2 = 0 + (rand() % 11);

            matrix_a[i][j]= random, random2;
            //cout << "a" << i << j << ": " << matrix_a[i][j] << "\t";
        }

    cout << "\n";

    //Populating Matrix B
    for(i = 0; i < r1; ++i)
        for(j = 0; j < c1; ++j)
        {
            long random = 0 + (rand() % 11);
            long random2 = 0 + (rand() % 11);
            matrix_b[i][j]= random, random2;
           // cout << "b" << i << j << ": " << matrix_b[i][j] << "\t";
        }

    // Matrix Multiplication
    //cout << "\nMultiplication of given two matrices is:\n";


    //long rslt[r1][c2];

    clock_t begin1 = clock();
    for (long j = 0; j < c2; j++) {
        for (long k = 0; k < r2; k++) {
            //rslt[j][k] = 0;

            for (long i = 0; i < r1; i++) {
                //rslt[i][j] = 0;
                matrix_c[i][j] += matrix_a[i][k] * matrix_b[k][j];
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
    return 0;


    }
```
