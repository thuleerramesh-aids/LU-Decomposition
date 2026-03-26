# LU Decomposition 

## AIM:
To write a program to find the LU Decomposition of a matrix.

## Equipments Required:
1. Hardware – PCs
2. Anaconda – Python 3.7 Installation / Moodle-Code Runner

## Algorithm
Step 1: Import the numpy module to use built-in functions for calculations.
Step 2: Import the lu function from scipy.linalg to perform LU decomposition.
Step 3: Read the input matrix, perform LU decomposition using lu(A), and print the L matrix and U matrix.
Step 4: End the program.

## Program:
(i) To find the L and U matrix
```
Developed by: Thuleer R
RegisterNumber: 212225230285

import os
os.environ["OPENBLAS_NUM_THREADS"] = "1"

import numpy as np
import ast

def lu_decomposition(A):
    A = np.array(A, dtype=float)
    n = len(A)

    L = np.zeros((n, n))
    U = A.copy()

    for i in range(n):
        # Pivoting
        max_row = np.argmax(abs(U[i:, i])) + i
        if i != max_row:
            U[[i, max_row]] = U[[max_row, i]]
            L[[i, max_row], :i] = L[[max_row, i], :i] 

        # Set diagonal
        L[i][i] = 1

        for j in range(i + 1, n):
            factor = U[j][i] / U[i][i]
            L[j][i] = factor
            U[j] = U[j] - factor * U[i]

    return L, U


A = ast.literal_eval(input())

L, U = lu_decomposition(A)

print(L)
print(U)


```
(ii) To find the LU Decomposition of a matrix
```
'''Program to solve a matrix using LU decomposition.
Developed by: Thuleer R
RegisterNumber: 212225230285
'''


import os
os.environ["OPENBLAS_NUM_THREADS"] = "1"

import numpy as np
import ast

def lu_decomposition(A):
    A = np.array(A, dtype=float)
    n = len(A)

    L = np.zeros((n, n))
    U = A.copy()
    P = np.eye(n)  

    for i in range(n):
        # Pivoting
        max_row = np.argmax(abs(U[i:, i])) + i
        if i != max_row:
            U[[i, max_row]] = U[[max_row, i]]
            P[[i, max_row]] = P[[max_row, i]]
            L[[i, max_row], :i] = L[[max_row, i], :i]

        L[i][i] = 1

        for j in range(i + 1, n):
            factor = U[j][i] / U[i][i]
            L[j][i] = factor
            U[j] = U[j] - factor * U[i]

    return L, U, P


def forward_substitution(L, b):
    n = len(L)
    y = np.zeros(n)
    for i in range(n):
        y[i] = b[i] - sum(L[i][j] * y[j] for j in range(i))
    return y


def backward_substitution(U, y):
    n = len(U)
    x = np.zeros(n)
    for i in range(n - 1, -1, -1):
        x[i] = (y[i] - sum(U[i][j] * x[j] for j in range(i + 1, n))) / U[i][i]
    return x

A = ast.literal_eval(input())
b = np.array(ast.literal_eval(input()), dtype=float)

L, U, P = lu_decomposition(A)

b = P @ b

y = forward_substitution(L, b)
x = backward_substitution(U, y)

print(x)
```

## Output:
<img width="730" height="853" alt="mfai 5a" src="https://github.com/user-attachments/assets/4c4126ed-5485-463b-8287-28106f20abdf" />
<img width="565" height="843" alt="mfai 5b" src="https://github.com/user-attachments/assets/10388710-4e86-4932-b51b-8ffda30e05bb" />




## Result:
Thus the program to find the LU Decomposition of a matrix is written and verified using python programming.

