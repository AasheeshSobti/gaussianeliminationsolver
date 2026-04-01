# gaussianeliminationsolver
Solves systems of ANY number of linear equations using gaussian elimination

-Run the code in your IDE
https://math.libretexts.org/Courses/Palo_Alto_College/College_Algebra/05%3A_Systems_of_Equations_and_Inequalities/5.04%3A_Solving_Systems_with_Gaussian_Elimination -- source for turning system into matrix
-Python and numpy

CODE:


#Solves systems of equations
#INPUT: A matrix (dw insturctions are there on how to make a system of equations into a matrix!)
#OUTPUT: Variable values from back to front
#Tung tung tung sahur approved

import numpy as np 
print("Triple T reporting for duty! I'm Tung tung sahere and ready to solve your linear algebra homework!")
print("Time for a quick tung tung tutorial. First, write down your system of equations, but just the coefficients and solution number. Check out math libretexts for a tutorial. For example, 3x + 4y + 5z = 4 becomes 3 4 5 4")
r = int(input("How much Rows Sir? (amount of variables) ")) #take in row amount
c = int(input("How much Columns Sir? (amount of variables +1) ")) #take in column amount

if r < 1 or c < 1: #failure handling
    print("son im crine why didn't you give positive integers do you have fractional or negative rows 😭😭🥀🥀")
    exit()

A = [] #create empty matrix

for m in range(r): #take in input for all the rows in A
    print("Please type your ", m+1, "th row rn bro")
    row = list(map(int, input().split()))
    count = len(row)
    if count != c: # failure handling
        print("son im crine values don't match try again") 
        exit()
    A.append(row)
A = np.array(A, dtype=float) #Convert to float array:
Legacy = A.copy() #Make a backup, call it legacy

def rowechelon(): #turns our matrix into row echelon form, which has diagonal 1s and 0s below, to make back substitution possible to solve systems
    for i in range(r): #makes diagonals 1
        pivot = A[i, i] #this is the diagonal point, dividing n/n is always 1 (which we want)
        A[i] = A[i] / pivot #divide everything, cause in algebra you must do the operation everywhere

        for j in range(i + 1, r):   # go through rows below pivot up to bottom
            multiplier = A[j, i]    # get value under pivot
            A[j] = A[j] - multiplier * A[i]   # eliminate, we use the row with 1 to multiply (I kept getting errors using another one and this is much cleaner)

def backsubstitution(A, r, c):
    x = np.zeros(r)
    for i in range(r - 1, -1, -1):
        rhs = A[i, c-1]
        for j in range(i + 1, r):
            rhs -= A[i, j] * x[j]

        x[i] = rhs

    print("Solutions, from the last variable in the row to front (if it says NAN, no solutions to the system):", x)



rowechelon()

backsubstitution(A, r, c)
