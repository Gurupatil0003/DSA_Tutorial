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
# 1. Infix Expressions
- Infix expressions are the most usual type of expression. This notation is typically employed when writing arithmetic expressions by hand. Moreover, in the infix 
 expression, we place the operator between the two operands it operates on.

- For example, the operator “+” appears between the operands A and B in the expression “A + B”. The following figure depicts the example:

  ![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/3fe85874-89ba-4691-8b18-ab6ea7d35437)

- Furthermore, infix expressions can also include parentheses to indicate the order of operations. In this way, we should observe the operator precedence rules 
 and use parentheses to clarify the order of operations in expressions in infix notation.

- Operator precedence rules specify the operator evaluation order in an expression. So, in an expression, operators with higher precedence are evaluated before 
 operators with lower precedence.

### Some operator precedence rules follow:

- Parentheses: expressions inside parentheses are evaluated first
- Exponentiation: exponents are evaluated next
- Multiplication and division: multiplication and division are evaluated before addition and subtraction
- Addition and subtraction: finally, addition and subtraction are evaluated last
- However, if an expression has multiple operators with the same precedence, the evaluation of those operators occurs from left to right.

### 2. Prefix Expressions
- Prefix expressions, also known as Polish notation, place the operator before the operands.

- For example, in the expression “+ A B”,  we place the “+” operator before the operands A and B, as demonstrated in the image next:
- ![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/f89fa26b-8b81-4598-90a9-7ce561f7a763)
- We should consider that prefix expressions are evaluated from right to left. Thus, we apply each operator to its operands as it is encountered.

### Postfix Expressions
- Postfix expressions, also known as reverse Polish notation, where we place the operator after the operands.

- For instance, in the expression “A B +”, the “+” we place the operator after the operands A and B. The figure next depicts the example:
![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/7294a960-72fe-46e0-a4f2-7ee122e40e75)

- Hence, we can evaluate postfix expressions from left to right, with each operator being applied to its operands as encountered.


## Infix, Postfix, and Prefix Notations

| Infix                 | Postfix       | Prefix         | Notes                                                            |
|-----------------------|---------------|----------------|------------------------------------------------------------------|
| A * B + C / D         | A B * C D / + | + * A B / C D  | multiply A and B, divide C by D, add the results                  |
| A * (B + C) / D       | A B C + * D / | / * A + B C D  | add B and C, multiply by A, divide by D                          |
| A * (B + C / D)       | A B C D / + * | * A + B / C D  | divide C by D, add B, multiply by A                              |


### Infix to Postfix Using Stack
```c
#include <stdio.h>      // Include standard input-output library
#include <ctype.h>      // Include ctype library for character functions

#define SIZE 40         // Define the maximum size of the stack and expression

char stack[SIZE];       // Declare stack array to store characters
int top = -1;           // Initialize top of stack to -1 indicating an empty stack

// Function to push a character onto the stack
void push(char c) {
    
    stack[++top] = c;        // Increment top and push character onto stack
}

// Function to pop a character from the stack
char pop() {
 
      return stack[top--]; // Return top character and decrement top
    }


// Function to determine precedence of operators
int precedence(char op) {
    if (op == '+' || op == '-')       // Lowest precedence
        return 1;
    if (op == '*' || op == '/' || op == '%')   // Medium precedence
        return 2;
    if (op == '^')                   // Highest precedence
        return 3;
    return 0;                        // Non-operator characters
}

// Function to convert infix expression to postfix
void infixToPostfix(char* infix, char* postfix) {
    int i = 0, j = 0;    // Initialize indices for infix and postfix arrays
    char ch, popped;

    // Process each character in the infix expression
    while ((ch = infix[i++]) != '\0') {
        if (isdigit(ch) || isalpha(ch)) {   // If operand, add to postfix
            postfix[j++] = ch;
        } else if (ch == '(') {             // If '(', push to stack
            push(ch);
        } else if (ch == ')') {             // If ')', pop until '('
            while (top != -1 && (popped = pop()) != '(') {
                postfix[j++] = popped;
            }
        } else {                            // If operator
            while (top != -1 && precedence(stack[top]) >= precedence(ch)) {
                postfix[j++] = pop();       // Pop higher or equal precedence operators
            }
            push(ch);                       // Push current operator onto stack
        }
    }

    // Pop remaining operators from the stack
    while (top != -1) {
        postfix[j++] = pop();
    }

    postfix[j] = '\0';    // Null-terminate the postfix expression
}

int main() {
    char infix[SIZE], postfix[SIZE];  // Declare arrays for infix and postfix expressions

    printf("Enter an infix expression: ");
    scanf("%s", infix);               // Read infix expression from user

    infixToPostfix(infix, postfix);   // Convert infix to postfix

    printf("Postfix expression: %s\n", postfix);  // Output the postfix expression

    return 0;                         // Exit program
}
```
### Algorithm for Evaluation of Postfix Expression
- Create an empty stack and start scanning the postfix expression from left to right. 

- If the element is an operand, push it into the stack.
- If the element is an operator O, pop twice and get A and B respectively. Calculate BOA and push it back to the stack.
- When the expression is ended, the value in the stack is the final answer.
- Evaluation of a postfix expression using a stack is explained in below example:
https://github.com/Gurupatil0003/DSA_Tutorial/blob/master/Img/Evaluation-of-a-postfix-expression-using-a-stack.gif
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
# LinkedList Operations 

~~~c

#include <stdio.h>
#include <stdlib.h>

// Define the structure of a Node
struct Node {
    int data; // The data part of the node
    struct Node *next; // Pointer to the next node in the list
};

// Function to insert a node at the beginning of the linked list
void insertStart(struct Node **head, int data) {
    // Allocate memory for the new node
    struct Node *newNode = (struct Node *) malloc(sizeof(struct Node));
    newNode->data = data; // Assign data to the new node
    newNode->next = *head; // Point the new node to the current head
    *head = newNode; // Update the head to point to the new node
}

// Function to delete a node with a specific key
void deleteNode(struct Node **head, int key) {
    struct Node *temp = *head; // Temporary pointer to traverse the list
    struct Node *prev = NULL; // Pointer to keep track of the previous node

    // If the head node itself holds the key to be deleted
    if (temp != NULL && temp->data == key) {
        *head = temp->next; // Update the head to the next node
        free(temp); // Free memory of the old head
        return;
    }

    // Traverse the list to find the key
    while (temp != NULL && temp->data != key) {
        prev = temp; // Update previous node
        temp = temp->next; // Move to the next node
    }

    // If the key was not present in the list
    if (temp == NULL) return;

    // Unlink the node from the list
    prev->next = temp->next;

    free(temp); // Free memory of the deleted node
}

// Function to search for a node with a specific key
int searchNode(struct Node *head, int key) {
    struct Node *current = head; // Initialize current pointer to head
    while (current != NULL) { // Traverse the list until the end
        if (current->data == key) // If key is found
            return 1; // Return 1 indicating key is found
        current = current->next; // Move to the next node
    }
    return 0; // Return 0 indicating key is not found
}

// Function to reverse the linked list
void reverseList(struct Node **head) {
    struct Node *prev = NULL;
    struct Node *current = *head;
    struct Node *next = NULL;

    while (current != NULL) {
        next = current->next; // Store next node
        current->next = prev; // Reverse current node's pointer
        prev = current; // Move pointers one position ahead
        current = next;
    }

    *head = prev; // Update head to point to the new first node (prev)
}

// Function to display the linked list
void display(struct Node *node) {
    while (node != NULL) { // Traverse the list until the end
        printf("%d ", node->data); // Print the data of the current node
        node = node->next; // Move to the next node
    }
    printf("\n");
}

int main() {
    struct Node *head = NULL; // Initialize head pointer
    struct Node *node2 = NULL; // Initialize node2 pointer
    struct Node *node3 = NULL; // Initialize node3 pointer
    struct Node *node4 = NULL; // Initialize node4 pointer

    // Allocate memory for the nodes
    head = (struct Node *) malloc(sizeof(struct Node));
    node2 = (struct Node *) malloc(sizeof(struct Node));
    node3 = (struct Node *) malloc(sizeof(struct Node));
    node4 = (struct Node *) malloc(sizeof(struct Node));

    // Assign data to the nodes and link them
    head->data = 15; // Data for head node
    head->next = node2; // Link head to node2

    node2->data = 10; // Data for node2
    node2->next = node3; // Link node2 to node3

    node3->data = 12; // Data for node3
    node3->next = node4; // Link node3 to node4

    node4->data = 3; // Data for node4
    node4->next = NULL; // Last node, so next is NULL

    // Display the initial linked list
    printf("Linklist: ");
    display(head);

    // Insert a new node at the beginning
    insertStart(&head, 25);

    // Display the linked list after insertion
    printf("\nAfter Inserting Element\n");
    printf("Linklist: ");
    display(head);

    // Delete a node with the data value 10
    deleteNode(&head, 10);

    // Display the linked list after deletion
    printf("\nAfter Deleting Element\n");
    printf("Linklist: ");
    display(head);

    // Reverse the linked list
    reverseList(&head);

    // Display the linked list after reversal
    printf("\nAfter Reversing the List\n");
    printf("Linklist: ");
    display(head);

    // Search for a node with the data value 12
    int key = 12;
    if (searchNode(head, key))
        printf("\nElement %d found in the list.\n", key);
    else
        printf("\nElement %d not found in the list.\n", key);

    // Search for a node with the data value 10
    key = 10;
    if (searchNode(head, key))
        printf("Element %d found in the list.\n", key);
    else
        printf("Element %d not found in the list.\n", key);

    return 0;
}
~~~



    



~~~c
void reverseList(struct Node **head) {
    struct Node *prev = NULL;
    struct Node *current = *head;
    struct Node *next = NULL;

    while (current != NULL) {
        next = current->next; // Store next node
        current->next = prev; // Reverse current node's pointer
        prev = current; // Move pointers one position ahead
        current = next;
    }

    *head = prev; // Update head to point to the new first node (prev)
}.     Could u explain reverse operation each by clearly
Certainly! Let's walk through the reverseList function step by step to understand how it reverses a singly linked list:

Initial Setup
void reverseList(struct Node **head) {
    struct Node *prev = NULL;
    struct Node *current = *head;
    struct Node *next = NULL;
prev: This will eventually point to the previous node as we reverse the list. Initially, it is set to NULL because the new tail of the list (the original head) will point to NULL.
current: This points to the current node being processed. It is initialized to the head of the list.
next: This will temporarily store the next node in the list as we reverse the pointers.
Loop to Reverse the List
c

    while (current != NULL) {
        next = current->next; // Store next node
        current->next = prev; // Reverse current node's pointer
        prev = current; // Move pointers one position ahead
        current = next;
    }
Let's break down what happens in each iteration of the loop:

Store next node: next = current->next;

This saves the next node (current->next) so that we don't lose the reference to the rest of the list after reversing the current node's pointer.
Reverse current node's pointer: current->next = prev;

This changes the next pointer of the current node to point to the previous node (prev). This is the key step that reverses the direction of the list.
Move prev pointer ahead: prev = current;

Now that the current node's pointer is reversed, we move the prev pointer to the current node. prev will be used in the next iteration to reverse the next node's pointer.
Move current pointer ahead: current = next;

We move the current pointer to the next node in the original list (stored in next). This prepares us to reverse the pointer of the next node in the next iteration.
Updated 
After the loop completes, prev will be pointing to the new head of the reversed list (the original tail). We update the head pointer to point to this new head.

Example Walkthrough
Consider the following linked list: 1 -> 2 -> 3 -> NULL.

Initial State
prev = NULL
current = head (1)
next = NULL
First Iteration
next = current->next (next points to 2)
current->next = prev (1's next now points to NULL)
prev = current (prev points to 1)
current = next (current points to 2)
State:

1 -> NULL
prev = 1
current = 2
next = 2
Second Iteration
next = current->next (next points to 3)
current->next = prev (2's next now points to 1)
prev = current (prev points to 2)
current = next (current points to 3)
State:

2 -> 1 -> NULL
prev = 2
current = 3
next = 3
Third Iteration
next = current->next (next points to NULL)
current->next = prev (3's next now points to 2)
prev = current (prev points to 3)
current = next (current points to NULL)
State:

3 -> 2 -> 1 -> NULL
prev = 3
current = NULL
next = NULL
Final Update
*head = prev (head now points to 3)
The linked list is now reversed: 3 -> 2 -> 1 -> NULL.

~~~

```c

#include <stdio.h>
#include <stdlib.h>

// Define the structure of a Node for doubly linked list
struct Node {
    int data; // The data part of the node
    struct Node *prev; // Pointer to the previous node in the list
    struct Node *next; // Pointer to the next node in the list
};

// Function to insert a node at the beginning of the doubly linked list
void insertStart(struct Node **head, int data) {
    // Allocate memory for the new node
    struct Node *newNode = (struct Node *) malloc(sizeof(struct Node));
    newNode->data = data; // Assign data to the new node
    newNode->prev = NULL; // Previous of new node is NULL
    newNode->next = *head; // Next of new node is current head

    if (*head != NULL) {
        (*head)->prev = newNode; // Previous of current head is new node
    }

    *head = newNode; // Update head to point to the new node
}

// Function to delete a node with a specific key from doubly linked list
void deleteNode(struct Node **head, int key) {
    struct Node *temp = *head; // Temporary pointer to traverse the list

    // Find the node with the key to be deleted
    while (temp != NULL && temp->data != key) {
        temp = temp->next; // Move to the next node
    }

    if (temp == NULL) return; // Key not found, return

    // Adjust pointers to unlink the node from the list
    if (temp->prev != NULL) {
        temp->prev->next = temp->next; // Link previous node to next node
    }
    if (temp->next != NULL) {
        temp->next->prev = temp->prev; // Link next node to previous node
    }

    if (temp == *head) {
        *head = temp->next; // Update head if deleting the first node
    }

    free(temp); // Free memory of the deleted node
}

// Function to search for a node with a specific key in doubly linked list
int searchNode(struct Node *head, int key) {
    struct Node *current = head; // Initialize current pointer to head
    while (current != NULL) { // Traverse the list until the end
        if (current->data == key) // If key is found
            return 1; // Return 1 indicating key is found
        current = current->next; // Move to the next node
    }
    return 0; // Return 0 indicating key is not found
}

// Function to reverse the doubly linked list
void reverseList(struct Node **head) {
    struct Node *temp = NULL;
    struct Node *current = *head;

    // Swap next and prev pointers for all nodes of the doubly linked list
    while (current != NULL) {
        temp = current->prev;
        current->prev = current->next;
        current->next = temp;
        current = current->prev; // Move to the next node
    }

    // Check if the list is empty or has only one node
    if (temp != NULL) {
        *head = temp->prev; // Update head to point to the new first node
    }
}

// Function to display the doubly linked list
void display(struct Node *head) {
    struct Node *last;

    // Forward traversal
    printf("Forward: ");
    while (head != NULL) { // Traverse the list until the end
        printf("%d ", head->data); // Print the data of the current node
        last = head; // Store the current node as last
        head = head->next; // Move to the next node
    }
    printf("\n");

    // Backward traversal
    printf("Backward: ");
    while (last != NULL) { // Traverse the list backwards using the 'last' pointer
        printf("%d ", last->data); // Print the data of the current node
        last = last->prev; // Move to the previous node
    }
    printf("\n");
}

int main() {
    // Initialize pointers to nodes
    struct Node *head = NULL;
    struct Node *node2 = NULL;
    struct Node *node3 = NULL;
    struct Node *node4 = NULL;

    // Allocate memory for each node
    head = (struct Node *) malloc(sizeof(struct Node));
    node2 = (struct Node *) malloc(sizeof(struct Node));
    node3 = (struct Node *) malloc(sizeof(struct Node));
    node4 = (struct Node *) malloc(sizeof(struct Node));

    // Assign data to each node
    head->data = 15;
    node2->data = 10;
    node3->data = 12;
    node4->data = 3;

    // Link the nodes together
    head->prev = NULL;
    head->next = node2;

    node2->prev = head;
    node2->next = node3;

    node3->prev = node2;
    node3->next = node4;

    node4->prev = node3;
    node4->next = NULL;

    // Display the doubly linked list
    printf("Doubly Linked List:\n");
    display(head);

    // Delete a node with the data value 10
    deleteNode(&head, 10);

    // Display the doubly linked list after deletion
    printf("\nAfter Deleting Element\n");
    display(head);

    // Reverse the doubly linked list
    reverseList(&head);

    // Display the doubly linked list after reversal
    printf("\nAfter Reversing the List\n");
    display(head);

    // Search for a node with the data value 12
    int key = 12;
    if (searchNode(head, key))
        printf("\nElement %d found in the list.\n", key);
    else
        printf("\nElement %d not found in the list.\n", key);

    // Search for a node with the data value 10
    key = 10;
    if (searchNode(head, key))
        printf("Element %d found in the list.\n", key);
    else
        printf("Element %d not found in the list.\n", key);

    return 0;
}

```



#reverse Operation 
~~~c

void reverseList(struct Node** head) {
    struct Node *prev = NULL;
    struct Node *current = *head;
    struct Node *next = NULL;

    while (current != NULL) {
        next = current->next;  // Store the next node

        // Swap the next and prev pointers
        current->next = prev;  // Set current's next to previous
        current->prev = next;  // Set current's prev to next

        // Move pointers one position ahead
        prev = current;        // Move prev to the current node
        current = next;        // Move current to the next node
    }

    // Update head to point to the new first node (prev)
    *head = prev;
}

~~~

# BST

```c



#include <stdio.h>
#include <stdlib.h>

// Definition of a TreeNode
typedef struct TreeNode {
    int value;
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;

// Function to create a new node
TreeNode* createNode(int value) {
    TreeNode* newNode = (TreeNode*)malloc(sizeof(TreeNode));
    newNode->value = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Function to insert a value into the BST
TreeNode* insert(TreeNode* root, int value) {
    if (root == NULL) {
        return createNode(value);
    }
    if (value < root->value) {
        root->left = insert(root->left, value);
    } else {
        root->right = insert(root->right, value);
    }
    return root;
}

// Function to delete a node from the BST
TreeNode* deleteNode(TreeNode* root, int value) {
    if (root == NULL) {
        return root;
    }

    // Traverse the tree to find the node to delete
    if (value < root->value) {
        root->left = deleteNode(root->left, value);
    } else if (value > root->value) {
        root->right = deleteNode(root->right, value);
    } else {
        // Node with only one child or no child
        if (root->left == NULL) {
            TreeNode* temp = root->right;
            free(root);
            return temp;
        } else if (root->right == NULL) {
            TreeNode* temp = root->left;
            free(root);
            return temp;
        }

        // Node with two children: Find the minimum value node in the right subtree
        TreeNode* temp = root->right;
        while (temp && temp->left != NULL) {
            temp = temp->left;
        }

        // Copy the inorder successor's content to this node
        root->value = temp->value;

        // Delete the inorder successor
        root->right = deleteNode(root->right, temp->value);
    }
    return root;
}

// Function to perform in-order traversal
void inorderTraversal(TreeNode* root) {
    if (root != NULL) {
        inorderTraversal(root->left);
        printf("%d ", root->value);
        inorderTraversal(root->right);
    }
}

int main() {
    TreeNode* root = NULL;

    // Inserting values into the BST
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 40);
    insert(root, 60);
    insert(root, 80);

    // Performing in-order traversal
    printf("In-order traversal before deletion: ");
    inorderTraversal(root);
    printf("\n");

    // Deleting a node
    root = deleteNode(root, 70);

    // Performing in-order traversal after deletion
    printf("In-order traversal after deletion of 70: ");
    inorderTraversal(root);
    printf("\n");

    // Note: You will need to manually free the tree memory or use a different approach 
    // to handle memory management without the `freeTree` function.

    return 0;
}

```

# Delete Opeartion With Inorder predecessor
```c
#include <stdio.h>
#include <stdlib.h>

// Definition of a TreeNode
typedef struct TreeNode {
    int value;
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;

// Function to create a new node
TreeNode* createNode(int value) {
    TreeNode* newNode = (TreeNode*)malloc(sizeof(TreeNode));
    newNode->value = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Function to insert a value into the BST
TreeNode* insert(TreeNode* root, int value) {
    if (root == NULL) {
        return createNode(value);
    }
    if (value < root->value) {
        root->left = insert(root->left, value);
    } else {
        root->right = insert(root->right, value);
    }
    return root;
}

// Function to find the maximum value node in a subtree (Inorder Predecessor)
TreeNode* findMax(TreeNode* root) {
    while (root->right != NULL) {
        root = root->right;
    }
    return root;
}

// Function to delete a node from the BST using Inorder Predecessor
TreeNode* deleteNode(TreeNode* root, int value) {
    if (root == NULL) {
        return NULL;
    }

    // Searching for the node to delete
    if (value < root->value) {
        root->left = deleteNode(root->left, value);
    } else if (value > root->value) {
        root->right = deleteNode(root->right, value);
    } else {
        // Node to be deleted found

        // Case 1: Node has no left child
        if (root->left == NULL) {
            TreeNode* temp = root->right;
            free(root);
            return temp;
        }
        // Case 2: Node has no right child
        else if (root->right == NULL) {
            TreeNode* temp = root->left;
            free(root);
            return temp;
        }

        // Case 3: Node has two children
        // Find the Inorder Predecessor (largest node in the left subtree)
        TreeNode* temp = findMax(root->left);

        // Replace the node's value with the Inorder Predecessor's value
        root->value = temp->value;

        // Delete the Inorder Predecessor
        root->left = deleteNode(root->left, temp->value);
    }

    return root;
}

// Function to perform in-order traversal
void inorderTraversal(TreeNode* root) {
    if (root != NULL) {
        inorderTraversal(root->left);
        printf("%d ", root->value);
        inorderTraversal(root->right);
    }
}

int main() {
    TreeNode* root = NULL;

    // Inserting values into the BST
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 40);
    insert(root, 60);
    insert(root, 80);

    // Performing in-order traversal before deletion
    printf("In-order traversal before deletion: ");
    inorderTraversal(root);
    printf("\n");

    // Deleting the root node (50)
    root = deleteNode(root, 50);

    // Performing in-order traversal after deletion
    printf("In-order traversal after deletion of 50: ");
    inorderTraversal(root);
    printf("\n");

    return 0;
}


```
# Delete Opeartion With Inorder Successor


```c
#include <stdio.h>
#include <stdlib.h>

// Definition of a TreeNode
typedef struct TreeNode {
    int value;
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;

// Function to create a new node
TreeNode* createNode(int value) {
    TreeNode* newNode = (TreeNode*)malloc(sizeof(TreeNode));
    newNode->value = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Function to insert a value into the BST
TreeNode* insert(TreeNode* root, int value) {
    if (root == NULL) {
        return createNode(value);
    }
    if (value < root->value) {
        root->left = insert(root->left, value);
    } else {
        root->right = insert(root->right, value);
    }
    return root;
}

// Function to find the minimum value node in a subtree (Inorder Successor)
TreeNode* findMin(TreeNode* root) {
    while (root->left != NULL) {
        root = root->left;
    }
    return root;
}

// Function to delete a node from the BST using Inorder Successor
TreeNode* deleteNode(TreeNode* root, int value) {
    if (root == NULL) {
        return NULL;
    }

    // Searching for the node to delete
    if (value < root->value) {
        root->left = deleteNode(root->left, value);
    } else if (value > root->value) {
        root->right = deleteNode(root->right, value);
    } else {
        // Node to be deleted found

        // Case 1: Node has no left child
        if (root->left == NULL) {
            TreeNode* temp = root->right;
            free(root);
            return temp;
        }
        // Case 2: Node has no right child
        else if (root->right == NULL) {
            TreeNode* temp = root->left;
            free(root);
            return temp;
        }

        // Case 3: Node has two children
        // Find the Inorder Successor (smallest node in the right subtree)
        TreeNode* temp = findMin(root->right);

        // Replace the node's value with the Inorder Successor's value
        root->value = temp->value;

        // Delete the Inorder Successor
        root->right = deleteNode(root->right, temp->value);
    }

    return root;
}

// Function to perform in-order traversal
void inorderTraversal(TreeNode* root) {
    if (root != NULL) {
        inorderTraversal(root->left);
        printf("%d ", root->value);
        inorderTraversal(root->right);
    }
}

int main() {
    TreeNode* root = NULL;

    // Inserting values into the BST
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 40);
    insert(root, 60);
    insert(root, 80);

    // Performing in-order traversal before deletion
    printf("In-order traversal before deletion: ");
    inorderTraversal(root);
    printf("\n");

    // Deleting the root node (50)
    root = deleteNode(root, 50);

    // Performing in-order traversal after deletion
    printf("In-order traversal after deletion of 50: ");
    inorderTraversal(root);
    printf("\n");

    return 0;
}


```
# BST Travesrasl


```c
#include <stdio.h>
#include <stdlib.h>

// Define the structure of a tree node
typedef struct TreeNode {
    int value;
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;

// Function to create a new tree node
TreeNode* createNode(int value) {
    TreeNode* newNode = (TreeNode*)malloc(sizeof(TreeNode));
    newNode->value = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// In-order Traversal
void inorderTraversal(TreeNode* root) {
    if (root != NULL) {
        inorderTraversal(root->left);
        printf("%d ", root->value);
        inorderTraversal(root->right);
    }
}

// Pre-order Traversal
void preorderTraversal(TreeNode* root) {
    if (root != NULL) {
        printf("%d ", root->value);
        preorderTraversal(root->left);
        preorderTraversal(root->right);
    }
}

// Post-order Traversal
void postorderTraversal(TreeNode* root) {
    if (root != NULL) {
        postorderTraversal(root->left);
        postorderTraversal(root->right);
        printf("%d ", root->value);
    }
}

int main() {
    // Example usage
    TreeNode* root = createNode(50);
    root->left = createNode(30);
    root->right = createNode(70);
    root->left->left = createNode(20);
    root->left->right = createNode(40);
    root->right->left = createNode(60);
    root->right->right = createNode(80);

    printf("In-order Traversal: ");
    inorderTraversal(root);
    printf("\n");

    printf("Pre-order Traversal: ");
    preorderTraversal(root);
    printf("\n");

    printf("Post-order Traversal: ");
    postorderTraversal(root);
    printf("\n");

    return 0;
}


```

```c
#include <stdio.h>

int bn(int arr[], int low, int high, int x) {
    while (low <= high) {
        int mid = low + (high - low) / 2;
        
        if (arr[mid] == x) {
            return mid;
        }
        
        if (arr[mid] < x) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return -1; // Element not found
}

int main() {
    int arr[] = {1, 2, 43};
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 2;
    
    int result = bn(arr, 0, n - 1, x);
    
    printf("Element found at index: %d\n", result);
    
    return 0;
}



```
# interpolation Search
```c
#include <stdio.h>

int interpolationSearch(int arr[], int low, int high, int x) {
    while (low <= high && x >= arr[low] && x <= arr[high]) {
        // Calculate the position based on interpolation formula
        int pos = low + ((double)(high - low) / (arr[high] - arr[low])) * (x - arr[low]);
        
        if (arr[pos] == x) {
            return pos;
        }
        
        if (arr[pos] < x) {
            low = pos + 1;
        } else {
            high = pos - 1;
        }
    }
    return -1; // Element not found
}

int main() {
    int arr[] = {1, 2, 43,44,45,46};
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 46;
    
    int result = interpolationSearch(arr, 0, n - 1, x);
    
    printf("Element found at index: %d\n", result);
    
    return 0;
}
```
# Bubble Sort

```c

#include <stdio.h>

// Function to perform Bubble Sort on an array
void bubbleSort(int arr[], int n) {
    int i, j, temp;
    
    // Outer loop: runs n-1 times
    for (i = 0; i < n-1; i++) {
        // Inner loop: compare adjacent elements
        for (j = 0; j < n-i-1; j++) {
            // If the current element is greater than the next, swap them
            if (arr[j] > arr[j+1]) {
                temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

// Function to print the elements of an array
void printArray(int arr[], int size) {
    int i;
    // Loop through the array and print each element
    for (i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n"); // Print a new line after printing all elements
}

// Main function to test the bubbleSort function
int main() {
    // Define an array of integers
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    // Calculate the number of elements in the array
    int n = sizeof(arr)/sizeof(arr[0]);
    
    // Print the unsorted array
    printf("Unsorted array: \n");
    printArray(arr, n);
    
    // Call the bubbleSort function to sort the array
    bubbleSort(arr, n);
    
    // Print the sorted array
    printf("Sorted array: \n");
    printArray(arr, n);
    
    return 0; // Return 0 to indicate successful execution
}

```
#Selection Sort
```c
#include <stdio.h>

// Function to perform selection sort
void selectionSort(int arr[], int n) {
    int i, j, minIndex, temp;

    for (i = 0; i < n - 1; i++) {
        // Assume the first element of the unsorted part is the minimum
        minIndex = i;

        // Find the index of the minimum element in the remaining unsorted part
        for (j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }

        // Swap the found minimum element with the first element
        if (minIndex != i) {
            temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
    }
}

// Function to print an array
void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Original array: \n");
    printArray(arr, n);

    selectionSort(arr, n);

    printf("Sorted array: \n");
    printArray(arr, n);

    return 0;
}
```

# Insertion Sort
```c

#include <stdio.h>

// Function to perform insertion sort
void insertionSort(int arr[], int n) {
    int i, key, j;

    // Traverse from the second element to the end of the array
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        // Move elements of arr[0..i-1], that are greater than key,
        // to one position ahead of their current position
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

// Function to print an array
void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("Original array:\n");
    printArray(arr, n);

    insertionSort(arr, n);

    printf("Sorted array:\n");
    printArray(arr, n);

    return 0;
}


```

# Adjacency matrix
```c
#include <stdio.h>

#define MAX_NODES 5

// Function to add an edge to the adjacency matrix
void addEdge(int graph[MAX_NODES][MAX_NODES], int start, int end) {
    graph[start][end] = 1;
    graph[end][start] = 1; // Because it's an undirected graph
}

// Function to print the adjacency matrix
void printMatrix(int graph[MAX_NODES][MAX_NODES], int nodes) {
    printf("Adjacency Matrix:\n");
    for (int i = 0; i < nodes; i++) {
        for (int j = 0; j < nodes; j++) {
            printf("%d ", graph[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int graph[MAX_NODES][MAX_NODES] = {0}; // Initialize the matrix with zeros
    int nodes = 5;


    // Adding edges
    addEdge(graph, 0, 1);
    addEdge(graph, 0, 4);
    addEdge(graph, 1, 2);
    addEdge(graph, 1, 3);
    addEdge(graph, 2, 3);
    addEdge(graph, 3, 4);

    // Print the adjacency matrix
    printMatrix(graph, nodes);

    return 0;
}
```
# Graph 
```c

0 -- 1 -- 2
|    |
4 -- 3
```

```c
#include <stdio.h>
#include <stdbool.h>

#define MAX_NODES 5

// Function to add an edge to the adjacency matrix
void addEdge(int graph[MAX_NODES][MAX_NODES], int start, int end) {
    graph[start][end] = 1;
    graph[end][start] = 1; // Because it's an undirected graph
}

// Function to print the adjacency matrix
void printMatrix(int graph[MAX_NODES][MAX_NODES], int nodes) {
    printf("Adjacency Matrix:\n");
    for (int i = 0; i < nodes; i++) {
        for (int j = 0; j < nodes; j++) {
            printf("%d ", graph[i][j]);
        }
        printf("\n");
    }
}

// BFS algorithm implementation
void bfs(int matrix[MAX_NODES][MAX_NODES], int start, int nodes) {
    bool visited[MAX_NODES] = {false};  // Array to keep track of visited nodes
    int queue[MAX_NODES];  // Queue to hold the nodes to be explored
    int front = 0, rear = 0;  // Pointers for the front and rear of the queue

    // Start by visiting the initial node
    visited[start] = true;
    queue[rear++] = start;

    printf("BFS starting from vertex %d:\n", start);

    while (front < rear) {
        int current = queue[front++]; // Dequeue the front node
        printf("%d ", current);

        // Explore all adjacent nodes
        for (int i = 0; i < nodes; i++) {
            if (matrix[current][i] == 1 && !visited[i]) {
                visited[i] = true;
                queue[rear++] = i; // Enqueue the unvisited adjacent node
            }
        }
    }
    printf("\n");
}

int main() {
    int graph[MAX_NODES][MAX_NODES] = {0}; // Initialize the matrix with zeros
    int nodes = MAX_NODES;

    // Adding edges
    addEdge(graph, 0, 1);
    addEdge(graph, 0, 4);
    addEdge(graph, 1, 2);
    addEdge(graph, 1, 3);
    addEdge(graph, 2, 3);
    addEdge(graph, 3, 4);

    // Print the adjacency matrix
    printMatrix(graph, nodes);

    // Perform BFS starting from vertex 0
    bfs(graph, 0, nodes);

    return 0;
}

```


# DFS 
```c

#include <stdio.h>
#include <stdbool.h>

#define MAX_NODES 5

// Function to add an edge to the adjacency matrix
void addEdge(int graph[MAX_NODES][MAX_NODES], int start, int end) {
    graph[start][end] = 1;
    graph[end][start] = 1; // Because it's an undirected graph
}

// Function to print the adjacency matrix
void printMatrix(int graph[MAX_NODES][MAX_NODES], int nodes) {
    printf("Adjacency Matrix:\n");
    for (int i = 0; i < nodes; i++) {
        for (int j = 0; j < nodes; j++) {
            printf("%d ", graph[i][j]);
        }
        printf("\n");
    }
}

// Stack structure
typedef struct {
    int items[MAX_NODES];
    int top;
} Stack;

// Initialize the stack
void initStack(Stack* s) {
    s->top = -1;
}

// Push an item onto the stack
void push(Stack* s, int item) {
    if (s->top < MAX_NODES - 1) {
        s->items[++s->top] = item;
    } else {
        printf("Stack overflow\n");
    }
}

// Pop an item from the stack
int pop(Stack* s) {
    if (s->top >= 0) {
        return s->items[s->top--];
    } else {
        printf("Stack underflow\n");
        return -1;  // Return an invalid value
    }
}

// Check if the stack is empty
int isEmpty(Stack* s) {
    return s->top == -1;
}

// DFS algorithm using an explicit stack
void dfs(int graph[MAX_NODES][MAX_NODES], int start, int nodes) {
    bool visited[MAX_NODES] = {false};  // Array to keep track of visited nodes
    Stack s;
    initStack(&s);

    // Push the start node onto the stack
    push(&s, start);
    printf("DFS starting from vertex %d:\n", start);

    while (!isEmpty(&s)) {
        int vertex = pop(&s);

        // If the vertex has not been visited, visit it
        if (!visited[vertex]) {
            visited[vertex] = true;
            printf("%d ", vertex);

            // Push all adjacent unvisited nodes onto the stack
            for (int i = nodes - 1; i >= 0; i--) {  // Push nodes in reverse order to maintain correct DFS order
                if (graph[vertex][i] == 1 && !visited[i]) {
                    push(&s, i);
                }
            }
        }
    }
    printf("\n");
}

int main() {
    int graph[MAX_NODES][MAX_NODES] = {0}; // Initialize the matrix with zeros
    int nodes = 5;

    // Adding edges
    addEdge(graph, 0, 1);
    addEdge(graph, 0, 4);
    addEdge(graph, 1, 2);
    addEdge(graph, 1, 3);
    addEdge(graph, 2, 3);
    addEdge(graph, 3, 4);

    // Print the adjacency matrix
    printMatrix(graph, nodes);

    // Perform DFS using stack starting from vertex 0
    dfs(graph, 0, nodes);

    return 0;
}


```

```c
#include <stdio.h>
#include <stdbool.h>

#define MAX_NODES 5

// Function to add an edge to the adjacency matrix
void addEdge(int graph[MAX_NODES][MAX_NODES], int start, int end) {
    graph[start][end] = 1;
    graph[end][start] = 1; // Because it's an undirected graph
}

// Function to print the adjacency matrix
void printMatrix(int graph[MAX_NODES][MAX_NODES], int nodes) {
    printf("Adjacency Matrix:\n");
    for (int i = 0; i < nodes; i++) {
        for (int j = 0; j < nodes; j++) {
            printf("%d ", graph[i][j]);
        }
        printf("\n");
    }
}

// BFS algorithm implementation
void bfs(int matrix[MAX_NODES][MAX_NODES], int start, int nodes) {
    bool visited[MAX_NODES] = {false};  // Array to keep track of visited nodes
    int queue[MAX_NODES];  // Queue to hold the nodes to be explored
    int front = -1, rear = -1;  // Pointers for the front and rear of the queue

    // Start by visiting the initial node
    visited[start] = true;
    queue[++rear] = start; // Enqueue the start node and increment rear
    if (front == -1) front++; // Set front to 0 when the first element is added

    printf("BFS starting from vertex %d:\n", start);

    while (front <= rear) {
        int current = queue[front++]; // Dequeue the front node
        printf("%d ", current);

        // Explore all adjacent nodes
        for (int i = 0; i < nodes; i++) {
            if (matrix[current][i] == 1 && !visited[i]) {
                visited[i] = true;
                queue[++rear] = i; // Enqueue the unvisited adjacent node and increment rear
            }
        }
    }
    printf("\n");
}

int main() {
    int graph[MAX_NODES][MAX_NODES] = {0}; // Initialize the matrix with zeros
    int nodes = MAX_NODES;

    // Adding edges
    addEdge(graph, 0, 1);
    addEdge(graph, 0, 4);
    addEdge(graph, 1, 2);
    addEdge(graph, 1, 3);
    addEdge(graph, 2, 3);
    addEdge(graph, 3, 4);

    // Print the adjacency matrix
    printMatrix(graph, nodes);

    // Perform BFS starting from vertex 0
    bfs(graph, 0, nodes);

    return 0;
}


```

# Adjacency List 
```c
#include <stdio.h>
#include <stdlib.h>

// Node for adjacency list
typedef struct Node {
    int vertex;
    struct Node* next;
} Node;

// Function to create a new adjacency list node
Node* createNode(int vertex) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->vertex = vertex;
    newNode->next = NULL;
    return newNode;
}

// Function to initialize the adjacency list
void initList(Node* adjList[], int V) {
    for (int i = 0; i < V; i++) {
        adjList[i] = NULL;
    }
}

// Function to add an edge to the adjacency list
void addEdge(Node* adjList[], int src, int dest) {
    // Add dest to src's list
    Node* newNode = createNode(dest);
    newNode->next = adjList[src];
    adjList[src] = newNode;

    // Add src to dest's list (for undirected graph)
    newNode = createNode(src);
    newNode->next = adjList[dest];
    adjList[dest] = newNode;
}

// Function to print the adjacency list
void printList(Node* adjList[], int V) {
    for (int i = 0; i < V; i++) {
        Node* temp = adjList[i];
        printf("Vertex %d:", i);
        while (temp) {
            printf(" -> %d", temp->vertex);
            temp = temp->next;
        }
        printf("\n");
    }
}

int main() {
    int V = 5;  // Number of vertices
    Node* adjList[V];

    initList(adjList, V);

    addEdge(adjList, 0, 1);
    addEdge(adjList, 0, 4);
    addEdge(adjList, 1, 2);
    addEdge(adjList, 1, 3);
    addEdge(adjList, 2, 3);
    addEdge(adjList, 3, 4);

    printf("Adjacency List:\n");
    printList(adjList, V);

    return 0;
}
```
