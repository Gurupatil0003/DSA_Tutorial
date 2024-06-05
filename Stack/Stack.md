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



### Structure to represent the stack
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
code 
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

