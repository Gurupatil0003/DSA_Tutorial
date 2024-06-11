# Union
- Unions are conceptually similar to structures in C. The syntax to declare/define a union is also similar to that of a structure. **The only differences is in terms of storage**. In structure each member has its own storage location, whereas all members of union uses a single shared memory location which is equal to the size of 
 its largest data member


### What is the Major Difference between Structure and Union
![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/499ed234-f0bb-4154-99f3-2d35d2174a87)

## Union in C Programming
A union is a data type. C Language provides us a special type of data type called union by which it can store many types of data types in the same memory location but it has the same value in the variable of data types at the same time. But the Union can use the same memory location in many types through Union All members of the Union use only one memory location and their size can be as much as the member with the largest size.

## Defining a Union
Let's use the union keyword to define unions. This is similar to defining the structure.

**The basic syntax of Unions:-**
```c
union union_name
{
  data_type var1;
  data_type var2;
  ...
  ...
  data_type varn;
}u1.u2,….un;
```
First of all, union defines keyword and union name. Then before we define variables in curly brackets {}. Then let's create before union variables of curly brackets {}.
```
union in-put
{
  int a;
  float b;
}in;
```
Now it is of in variable input type and it can store an integer value or it can store a float value. We cannot store value in both its variables simultaneously.

## Sizeof Union
```c
#include <stdio.h>
union letter{  
int a;  
char b;  
float c;  
double d;  
};  

int main()  
{  
  printf("The size of union letter is %d", sizeof(union letter));  
  return 0;  
}
```
## Accessing Union Member Variables
Union members also access the same way structure members access. First of all, we write the name of the union. Then before dot (.) An operator is written and the member's name is written. We can assign the value of union members with this type.
```
in.a = 10;
```
If we want to print this union member then we can do with these types.
printf(“%d”,in.a);

### For Example:-
```c
#include<stdio.h>

/* Declaring input union */
union input
{
  int a;
  float b;
}in; /* Union variable */
int main()
{
  in.a = 15;
  in.b = 20;
  /* Will print a garbage value */
  printf(“Value of a is : %dn”,in.a);

  /* Will print 20 */
  printf(“Value of b is : %f”,in.b);
return 0;
}
```
### Output
```
Value of a is: 1101345
Value of b is: 20.00000
```

I hope that you all liked this tutorial, if you want to read these tutorials more then stay connected with me.


Originaly posted on - [Union in C Programming](https://alimammiya.hashnode.dev/union-in-c-programming)
