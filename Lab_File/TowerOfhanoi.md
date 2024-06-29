# Tower of Hanoi

![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/ed72cec0-e9e4-4c8d-94db-549a1b413128)

#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>

#define SIZE 40 // Define the maximum size of the stack

// Function prototypes
int pop();
void push(int);

// Global variables
char postfix[SIZE]; // Array to store the postfix expression
int stack[SIZE]; // Stack array
int top = -1; // Index of the top of the stack

int main()
{
}

// Function to push an element onto the stack
void push(int n)
{
    if (top < SIZE - 1) // Check if the stack is not full
    {
        stack[++top] = n; // Increment the top index and push the element
    }
    else
    {
        printf("Stack overflow!\n"); // Print error message if stack is full
        exit(-1); // Exit the program with error code
    }
}

// Function to pop an element from the stack
int pop()
{    
    if (top > -1) // Check if the stack is not empty
    {
        return stack[top--]; // Return the top element and decrement the top index
    }
    else
    {
        printf("Stack underflow!\n"); // Print error message if stack is empty
        exit(-1); // Exit the program with error code
    }
}


