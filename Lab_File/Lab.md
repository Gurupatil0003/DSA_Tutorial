Implement Stack and its operations like push and pop
```c
#include <stdio.h>

void push();
void display();

int a[100], top = -1;

int main() {
    int x;
    while (1) {
        printf("\n0 or CTRL-C to Exit ");
        printf("\n1. Push");
        printf("\n5. Display");
        printf("\nEnter your choice? \n");
        scanf("%d", &x);
        switch (x) {
            case 0:
                return 0;
            case 1:
                push();
                break;
            case 5:
                display();
                break;
            default:
                printf("\nInvalid choice,\nPlease try again.\n");
        }
    }
    return 0;
}

// function for pushing the element
void push() {
    int n = 0;
    printf("\nEnter the value to be inserted: ");
    scanf("%d", &n);
    top += 1;
    a[top] = n;
}

// function to view entire stack
void display() {
    if (top == -1) {
        printf("\nStack is empty");
    } else {
        printf("\nStack elements:\n");
        for (int i = top; i >= 0; i--) {
            printf("%d\n", a[i]);
        }
    }
}
```
# Push Operation
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 100 // Maximum size of the stack

// Define the stack structure
typedef struct {
    int items[MAX];
    int top;
} Stack;

// Initialize the stack
void initStack(Stack *s) {
    s->top = -1;
}

// Check if the stack is full
int isFull(Stack *s) {
    return s->top == MAX - 1;
}

// Push an element onto the stack
void push(Stack *s, int item) {
    if (isFull(s)) {
        printf("Stack overflow\n");
        return;
    }
    s->items[++(s->top)] = item;
    printf("%d pushed to stack\n", item);
}

int main() {
    Stack s;
    initStack(&s);

    push(&s, 10);
    push(&s, 20);
    push(&s, 30);

    return 0;
}
```


# Postfix Evalution
```c
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
    int i, a, b, result;
    char ch;

    // Prompt the user to enter a postfix expression
    printf("Enter a postfix expression: ");
    scanf("%s", postfix); // Read the postfix expression, e.g., "89+9-8/"

    // Process each character in the postfix expression
    for(i = 0; postfix[i] != '\0'; i++)
    {
        ch = postfix[i]; // Get the current character

        // If the character is a digit, push it onto the stack
        if(isdigit(ch))
        {
            push(ch - '0'); // Convert char to int and push onto the stack
        }
        // If the character is an operator, pop two elements and apply the operator
        else if(ch == '+' || ch == '-' || ch == '*' || ch == '/' || ch == '%')
        {
            b = pop(); // Pop the top element
            a = pop(); // Pop the next top element

            // Perform the operation based on the operator
            switch(ch)
            {
                case '+': result = a + b; break;
                case '-': result = a - b; break;
                case '*': result = a * b; break;
                case '/': result = a / b; break;
                case '%': result = a % b; break;
                default: 
                    printf("Invalid operator encountered!\n");
                    exit(-1);
            }
            
            // Push the result back onto the stack
            push(result);
        }
        else
        {
            printf("Invalid character encountered in expression!\n");
            exit(-1);
        }
    }

    // Pop the final result from the stack
    result = pop();

    // Print the result of the postfix evaluation
    printf("The postfix evaluation is: %d\n", result);
    
    return 0;
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


```
```c
Simplified Step-by-Step Execution for Input 89+9-8/:
Initialization:

stack: An array to store the numbers.
top: Initialized to -1 to indicate an empty stack.
Processing Each Character in 89+9-8/:

8:
isdigit('8') returns true.
Convert '8' to 8 (ch - '0').
Push 8 onto the stack.
Stack: [8], top: 0.

9:
isdigit('9') returns true.
Convert '9' to 9 (ch - '0').
Push 9 onto the stack.
Stack: [8, 9], top: 1.

+:
isdigit('+') returns false.
Pop 9 from the stack.
Pop 8 from the stack.
Perform 8 + 9 = 17.
Push 17 onto the stack.
Stack: [17], top: 0.

9:
isdigit('9') returns true.
Convert '9' to 9 (ch - '0').
Push 9 onto the stack.
Stack: [17, 9], top: 1.

-:
isdigit('-') returns false.
Pop 9 from the stack.
Pop 17 from the stack.
Perform 17 - 9 = 8.
Push 8 onto the stack.
Stack: [8], top: 0.

8:
isdigit('8') returns true.
Convert '8' to 8 (ch - '0').
Push 8 onto the stack.
Stack: [8, 8], top: 1.

/:
isdigit('/') returns false.
Pop 8 from the stack.
Pop 8 from the stack.
Perform 8 / 8 = 1.
Push 1 onto the stack.
Stack: [1], top: 0.
Final Result:

Pop the final result 1 from the stack.
Stack: [], top: -1.

Output: The postfix evaluation is: 1.

```
```c
printf("Enter a postfix expression: ");
scanf("%s", postfix); // User inputs "89+9-8/"
```
- The input string "89+9-8/" is stored in the postfix array:

```c
postfix = ['8', '9', '+', '9', '-', '8', '/', '\0']
```

- Processing the Input:
- The for loop iterates through each character of the postfix array until it encounters the null terminator ('\0'), which indicates the end of the string.
```c
for (i = 0; postfix[i] != '\0'; i++) {
    ch = postfix[i];
    // Process the character stored in ch
}
```
```c
Let's break down each iteration:

Iteration 1:

i = 0
postfix[0] = '8'
ch = '8'
Since '8' is a digit, push(ch - '0') converts it to an integer (8) and pushes it onto the stack.
Iteration 2:

i = 1
postfix[1] = '9'
ch = '9'
Since '9' is a digit, push(ch - '0') converts it to an integer (9) and pushes it onto the stack.
Iteration 3:

i = 2
postfix[2] = '+'
ch = '+'
Since '+' is an operator, two elements (9 and 8) are popped from the stack, the addition operation is performed (8 + 9), and the result (17) is pushed back onto the stack.
Iteration 4:

i = 3
postfix[3] = '9'
ch = '9'
Since '9' is a digit, push(ch - '0') converts it to an integer (9) and pushes it onto the stack.
Iteration 5:

i = 4
postfix[4] = '-'
ch = '-'
Since '-' is an operator, two elements (9 and 17) are popped from the stack, the subtraction operation is performed (17 - 9), and the result (8) is pushed back onto the stack.
Iteration 6:

i = 5
postfix[5] = '8'
ch = '8'
Since '8' is a digit, push(ch - '0') converts it to an integer (8) and pushes it onto the stack.
Iteration 7:

i = 6
postfix[6] = '/'
ch = '/'
Since '/' is an operator, two elements (8 and 8) are popped from the stack, the division operation is performed (8 / 8), and the result (1) is pushed back onto the stack.

```
# Push and Pop Operation

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 100 // Maximum size of the stack

// Define the stack structure
typedef struct {
    int items[MAX];
    int top;
} Stack;

// Initialize the stack
void initStack(Stack *s) {
    s->top = -1;
}

// Check if the stack is full
int isFull(Stack *s) {
    return s->top == MAX - 1;
}

// Check if the stack is empty
int isEmpty(Stack *s) {
    return s->top == -1;
}

// Push an element onto the stack
void push(Stack *s, int item) {
    if (isFull(s)) {
        printf("Stack overflow\n");
        return;
    }
    s->items[++(s->top)] = item;
    printf("%d pushed to stack\n", item);
}

// Pop an element from the stack
int pop(Stack *s) {
    if (isEmpty(s)) {
        printf("Stack underflow\n");
        return -1;
    }
    return s->items[(s->top)--];
}

int main() {
    Stack s;
    initStack(&s);

    // Push elements onto the stack
    push(&s, 10);
    push(&s, 20);
    push(&s, 30);

    // Pop elements from the stack
    printf("%d popped from stack\n", pop(&s));
    printf("%d popped from stack\n", pop(&s));
    printf("%d popped from stack\n", pop(&s));

    return 0;
}
```

# peek and Search
```c
#include <stdio.h>

// Define the maximum size of the stack
#define MAX 100

// Define a stack structure
struct Stack {
    int arr[MAX];
    int top;
};

// Function to initialize the stack
void initialize(struct Stack* stack) {
    stack->top = -1;
}

// Function to push an element onto the stack
void push(struct Stack* stack, int value) {
    if (stack->top < MAX - 1) {
        stack->arr[++(stack->top)] = value;
    } else {
        printf("Stack overflow. Cannot push %d\n", value);
    }
}

// Function to peek the top element of the stack
int peek(struct Stack* stack) {
    if (stack->top == -1) {
        printf("Stack is empty\n");
        return -1;
    }
    return stack->arr[stack->top];
}

// Function to search for an element in the stack
int search(struct Stack* stack, int value) {
    if (stack->top == -1) {
        printf("Stack is empty\n");
        return -1;
    }
    for (int i = stack->top; i >= 0; i--) {
        if (stack->arr[i] == value) {
            return i; // Return the index of the found element
        }
    }
    return -1; // Return -1 if element not found
}

int main() {
    struct Stack myStack;
    initialize(&myStack);

    // Push elements onto the stack
    push(&myStack, 10);
    push(&myStack, 20);
    push(&myStack, 30);
    push(&myStack, 40);
    push(&myStack, 50);

    // Peek the top element
    int topElement = peek(&myStack);
    if (topElement != -1) {
        printf("Top element: %d\n", topElement);
    }

    // Search for an element
    int searchElement = 20;
    int index = search(&myStack, searchElement);
    if (index != -1) {
        printf("Element %d found at index %d\n", searchElement, index);
    } else {
        printf("Element %d not found in the stack\n", searchElement);
    }

    return 0;
}
```

# Final Code 
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 100 // Define the maximum size of the stack

typedef struct Stack {
    int data[MAX];
    int top;
} Stack;

void createStack(Stack *s) {
    s->top = -1; // Initialize top to -1 indicating the stack is empty
}

void push(Stack *s, int value) {
    if (s->top == MAX - 1) {
        printf("Stack Overflow!\n");
        return;
    }
    s->data[++(s->top)] = value; // Increment top and add value
}

int pop(Stack *s) {
    if (s->top == -1) {
        printf("Stack Underflow!\n");
        return -1; // Return -1 if stack is empty
    }
    return s->data[(s->top)--]; // Return the top value and decrement top
}

void traverse(Stack *s) {
    if (s->top == -1) {
        printf("Stack is empty!\n");
        return;
    }
    for (int i = 0; i <= s->top; i++) {
        printf("%d ", s->data[i]);
    }
    printf("\n");
}

int peek(Stack *s) {
    if (s->top == -1) {
        printf("Stack is empty!\n");
        return -1;
    }
    return s->data[s->top];
}

int search(Stack *s, int value) {
    for (int i = 0; i <= s->top; i++) {
        if (s->data[i] == value) {
            return i; // Return the index of the value if found
        }
    }
    return -1; // Return -1 if value is not found
}

int main() {
    Stack s;
    createStack(&s);
    
    push(&s, 10);
    push(&s, 20);
    push(&s, 30);
    
    printf("Stack after pushing 10, 20, 30:\n");
    traverse(&s);
    
    printf("Top element is %d\n", peek(&s));
    
    printf("Popping top element: %d\n", pop(&s));
    printf("Stack after popping:\n");
    traverse(&s);
    
    int value = 20;
    int index = search(&s, value);
    if (index != -1) {
        printf("Element %d found at index %d\n", value, index);
    } else {
        printf("Element %d not found\n", value);
    }
    
    return 0;
}
```
