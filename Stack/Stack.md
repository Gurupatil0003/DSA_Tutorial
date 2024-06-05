# Stack
- In fact, Stack is more of behaviour of structure than being a structure itself. We can turn a regular array (either static or dynamic) into a stack with simple modification. Stack is an Abstract Data Type (ADT) they may have different implementations:

- 1.Using arrays.
- 2.Using linked lists (later on this note).
 For both implementations, the following requirements should be satisfied in order to hava an ADT Stack (from wikipedia):

- push, which adds an element to the collection,
- pop, which removes the most recently added element that was not yet removed,
- front, which returns the most recent element in the stack.
- The order in which elements come off a stack gives rise to its alternative name, LIFO (last in, first out). Additionally, a peek operation may give access to the top without modifying the stack. – Stack (Abstract Data Type).

- ![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/2aecda2b-20b8-49ad-a8fc-7c63f2b1ccce)

- This table should draw the boundaries between Abstract Data Types (ADT) and Concrete Data Types, and keep in mind that Abstract Data Types are built upon Concrete Data Types.


| Abstract Data Type (ADT) | Possible Implementations |
|--------------------------|--------------------------|
| Stack                    | Array or Linked List     |
| Queue                    | Array or Linked List     |



### Stack Array Implementation:
- A Stack is a Data Structure that implements the LIFO (last in first out) way of getting the data in and out. So, we insert on top and get from top. Exactly the same way as we would stack books. We can’t get a 
 book that is not on the top, without getting the others on top of it before. We define a stack again as a struct that has to have:

- an static Array that contains the Stack Data the top index of the Stack Array, where the last Item sits We could also include capacity, if we make it pseudodynamic.

-To keep it simple I will only talk about Integer Arrays. So, an struct of an Stack will look like this:

```c
#define MAX_SIZE 100 // Maximum size of the stack

// Structure to represent the stack
typedef struct {
    int data[MAX_SIZE]; // Array to hold the stack elements
    int top; // Index of the top element
} Stack;
```

### Operation Operation 

| Operation      | Description                                          |
|----------------|------------------------------------------------------|
| Push           | Add an element to the top of the stack.              |
| Pop            | Remove and return the top element from the stack.    |
| Peek/Top       | Return the top element without removing it.          |
| isEmpty        | Check if the stack is empty.                         |
| isFull         | Check if the stack is full (for fixed-size stacks).  |
| Initialize     | Initialize the stack to make it ready for use.       |

### Array Representation of a Stack
- 1.Define the Maximum Size: Set a maximum size for the stack.
 Initialize the Stack: Create a structure to hold the stack elements and the top index.
- 2.Operations:
  Push: Add an element to the top of the stack.
  Pop: Remove and return the top element of the stack.
  Peek: Return the top element without removing it.
  isEmpty: Check if the stack is empty.
  isFull: Check if the stack is full.
- 3.Display: Print all elements in the stack


### Opertation and Array represntation in stack
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 100  // Maximum size of the stack

typedef struct {
    int data[MAX];
    int top;
} Stack;

// Function to initialize the stack
void initStack(Stack *s) {
    s->top = -1;
}

// Function to check if the stack is empty
int isEmpty(Stack *s) {
    return s->top == -1;
}

// Function to check if the stack is full
int isFull(Stack *s) {
    return s->top == MAX - 1;
}

// Function to push an element onto the stack
void push(Stack *s, int value) {
    if (isFull(s)) {
        printf("Stack overflow\n");
        return;
    }
    s->data[++(s->top)] = value;
}

// Function to pop an element from the stack
int pop(Stack *s) {
    if (isEmpty(s)) {
        printf("Stack underflow\n");
        return -1;
    }
    return s->data[(s->top)--];
}

// Function to peek the top element of the stack
int peek(Stack *s) {
    if (isEmpty(s)) {
        printf("Stack is empty\n");
        return -1;
    }
    return s->data[s->top];
}

// Function to display the elements of the stack
void display(Stack *s) {
    if (isEmpty(s)) {
        printf("Stack is empty\n");
        return;
    }
    for (int i = 0; i <= s->top; i++) {
        printf("%d ", s->data[i]);
    }
    printf("\n");
}

int main() {
    Stack stack;
    initStack(&stack);

    push(&stack, 10);
    push(&stack, 20);
    push(&stack, 30);

    printf("Stack elements: ");
    display(&stack);

    printf("Top element: %d\n", peek(&stack));

    printf("Popped element: %d\n", pop(&stack));

    printf("Stack elements after pop: ");
    display(&stack);

    return 0;
}

```
## Stacks using Dynamic Arrays
- Array in C is static in nature, so its size should be known at compile time and we can’t change the size of the array after its declaration. Due to this, we may encounter situations where our array doesn’t 
 have enough space left for required elements or we allotted more than the required memory leading to memory wastage. To solve this problem, dynamic arrays come into the picture.

- A Dynamic Array is allocated memory at runtime and its size can be changed later in the program.

- We can create a dynamic array in C by using the following methods:
- 1.Using malloc() Function
- 2.Using calloc() Function
- 3.Resizing Array Using realloc() Function
- 4.Using Variable Length Arrays(VLAs)
- 5.Using Flexible Array Members
- 6.free
```c


```
### Stack Applications: Polish notation, Infix to postfix conversion, evaluation of postfix expression.

- Stacks are crucial in solving various problems, including arithmetic expression evaluation and conversion between different notations like infix, postfix, and 
 prefix. Here's how you can implement the stack applications you mentioned:

### Polish Notation (Prefix Notation)
- In Polish notation, also known as prefix notation, the operator precedes their operands.

- Example: + 2 3 is equivalent to 2 + 3

### Infix to Postfix Conversion
- Infix notation is the common arithmetic and logical formula notation, in which operators are written between operands.

- Example: 2 + 3 * 4 is in infix notation.

### Postfix notation, also known as Reverse Polish Notation (RPN), is where every operator follows all of its operands.

- Example: 2 3 4 * + is equivalent to 2 + 3 * 4.

### Evaluation of Postfix Expression
- To evaluate a postfix expression, you can use a stack to keep track of operands and apply operators when encountered.

```c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>  // For isdigit()

#define MAX_SIZE 100

// Stack structure
typedef struct {
    int top;
    int items[MAX_SIZE];
} Stack;

// Function to initialize the stack
void initStack(Stack *s) {
    s->top = -1;
}

// Function to check if the stack is empty
int isEmpty(Stack *s) {
    return s->top == -1;
}

// Function to check if the stack is full
int isFull(Stack *s) {
    return s->top == MAX_SIZE - 1;
}

// Function to push an element onto the stack
void push(Stack *s, int value) {
    if (isFull(s)) {
        printf("Stack overflow\n");
        exit(1);
    }
    s->items[++(s->top)] = value;
}

// Function to pop an element from the stack
int pop(Stack *s) {
    if (isEmpty(s)) {
        printf("Stack underflow\n");
        exit(1);
    }
    return s->items[(s->top)--];
}

// Function to evaluate a postfix expression
int evaluatePostfix(char *exp) {
    Stack stack;
    initStack(&stack);

    for (int i = 0; exp[i] != '\0'; i++) {
        if (isdigit(exp[i])) {
            push(&stack, exp[i] - '0');
        } else {
            int operand2 = pop(&stack);
            int operand1 = pop(&stack);
            switch (exp[i]) {
                case '+':
                    push(&stack, operand1 + operand2);
                    break;
                case '-':
                    push(&stack, operand1 - operand2);
                    break;
                case '*':
                    push(&stack, operand1 * operand2);
                    break;
                case '/':
                    push(&stack, operand1 / operand2);
                    break;
                default:
                    printf("Invalid operator\n");
                    exit(1);
            }
        }
    }

    return pop(&stack);
}

int main() {
    char exp[] = "23*4+"; // Postfix expression: 2*3+4
    printf("Postfix expression: %s\n", exp);
    printf("Result: %d\n", evaluatePostfix(exp));
    return 0;
}
```
### recursive
- A function that calls itself is known as a recursive function. And, this technique is known as recursion.
- Recursion is a powerful programming technique where a function calls itself to solve smaller instances of a problem until it reaches a base case. Here are 
  implementations of some common recursive algorithms:

### How recursion works?
```c
void recurse()
{
    ... .. ...
    recurse();
    ... .. ...
}

int main()
{
    ... .. ...
    recurse();
    ... .. ...
}
```
![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/735f64dc-4e3e-47ce-a317-7483429e4a36)

## Factorial
- Factorial of a non-negative integer n, denoted as n!, is the product of all positive integers less than or equal to n.
```
#include <stdio.h>

// Recursive function to calculate factorial
int factorial(int n) {
    if (n == 0 || n == 1)
        return 1;
    else
        return n * factorial(n - 1);
}

int main() {
    int n = 5;
    printf("Factorial of %d is %d\n", n, factorial(n));
    return 0;
}
```
## GCD (Greatest Common Divisor)
- The greatest common divisor (GCD) of two integers a and b is the largest positive integer that divides both a and b without leaving a remainder.
```c
#include <stdio.h>

// Recursive function to find GCD
int gcd(int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

int main() {
    int a = 12, b = 18;
    printf("GCD of %d and %d is %d\n", a, b, gcd(a, b));
    return 0;
}
```c
# Fibonacci Sequence
- The Fibonacci sequence is a series of numbers in which each number is the sum of the two preceding ones, usually starting with 0 and 1.
```c
#include <stdio.h>

// Recursive function to calculate Fibonacci number
int fibonacci(int n) {
    if (n <= 1)
        return n;
    else
        return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n = 7;
    printf("Fibonacci sequence up to %d terms: ", n);
    for (int i = 0; i < n; i++) {
        printf("%d ", fibonacci(i));
    }
    printf("\n");
    return 0;
}
```

## Tower of Hanoi
- The Tower of Hanoi is a mathematical puzzle where you have three pegs and a number of disks of different sizes which can be slid onto any peg. The puzzle starts 
 with the disks in a neat stack in ascending order of size on one peg, the smallest at the top.
```c
#include <stdio.h>

// Recursive function to solve Tower of Hanoi
void towerOfHanoi(int n, char from, char to, char aux) {
    if (n == 1) {
        printf("Move disk 1 from %c to %c\n", from, to);
        return;
    }
    towerOfHanoi(n - 1, from, aux, to);
    printf("Move disk %d from %c to %c\n", n, from, to);
    towerOfHanoi(n - 1, aux, to, from);
}

int main() {
    int n = 3; // Number of disks
    towerOfHanoi(n, 'A', 'C', 'B'); // A, B, and C are the names of the pegs
    return 0;
}
```
