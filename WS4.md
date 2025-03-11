## Q1. 
1. this is an array of 15 interger variables
2. this is an array of 4 double variables, initilised in order (3.3,0.0,1.1,2.2)
3. this is a 2d array of 5 coloumns and 10 rows of float variables 
4. this is an array of 11 pointers to interger values
5. this is a 2d array of 4 coloumns and 5 rows of pointers to pointers to void
6. this is an array of char variables, in this case it is a makeshift string variable which contains the string "Hello"
7. this is an expression which states that the char variable which is being pointed at by 's' is "Hello"
## Q2.
```c
int a [] = {10 , 15 , 20 , 25};
int b [] = {50 , 60 , 70 , 80 , 90};

int *x [] = {a , b};
int *y [] = {a + 2, b + 3};
int *p;
int *q;
int **r;

p = a;
q = y[1];
r = &q;
*p = &p[3] - y[0];
r[0][1] = **r - y[0][1];
```
firstly arrays A and B is initialized with int values 
then, pointer arrays X, Y, P and Q are initialized
after which int pointer array R is initialized. 
Then some expression take place. 
int * x is currently [10, 50] while int * y is [20, 80]
after the expressions, this changes to: 
int * p = 10 // int * q= 80 // r = a[3] // * p  changes a[3] from 20 to 