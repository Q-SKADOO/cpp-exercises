```cpp
#include <iostream>
#include <bits/stdc++.h>
using namespace std;



int main()
{
    long a[10][10], b[10][10], mult[10][10], r1, c1, r2, c2, i, j, k;

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

            a[i][j]= random, random2;
            cout << "a" << i << j << ": " << a[i][j] << "\t";
        }

    cout << "\n";

    //Populating Matrix B
    for(i = 0; i < r1; ++i)
        for(j = 0; j < c1; ++j)
        {
            long random = 0 + (rand() % 11);
            long random2 = 0 + (rand() % 11);
            b[i][j]= random, random2;
            cout << "b" << i << j << ": " << b[i][j] << "\t";
        }

    // Matrix Multiplication
    cout << "\nMultiplication of given two matrices is:\n";


    long rslt[r1][c2];
    for (long i = 0; i < r1; i++) {
        for (long j = 0; j < c2; j++) {
            rslt[i][j] = 0;

            for (long k = 0; k < r2; k++) {

                rslt[i][j] += a[i][k] * b[k][j];
            }

            cout << rslt[i][j] << "\t";
        }

        cout << endl;
    }


    return 0;


    }
```
