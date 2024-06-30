Implement Stack and its operations like push and pop
# Push Operation
```c
#include <stdio.h>

void push();
void pop();
void peek();
void search();
void display();

int a[100], top = -1;

int main() {
    int x;
    while (1) {
        printf("\n0 or CTRL-C to Exit ");
        printf("\n1. Push");
        printf("\n2. Pop");
        printf("\n3. Peek");
        printf("\n4. Search");
        printf("\n5. Display");
        printf("\nEnter your choice? \n");
        scanf("%d", &x);
        switch (x) {
            case 0:
                return 0;
            case 1:
                push();
                break;
            case 2:
                pop();
                break;
            case 3:
                peek();
                break;
            case 4:
                search();
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

// function for popping the element out
void pop() {
    if (top == -1) {
        printf("\nStack is empty");
    } else {
        int item;
        item = a[top];
        top -= 1;
        printf("\nPopped item is %d ", item);
    }
}

// function for peeking the element from top of the stack
void peek() {
    if (top >= 0)
        printf("\nThe top element is %d", a[top]);
    else
        printf("\nStack is empty");
}

// function to search for an element in the stack
void search() {
    int key, found = 0;
    printf("\nEnter the element to search: ");
    scanf("%d", &key);
    for (int i = top; i >= 0; i--) {
        if (a[i] == key) {
            printf("\nElement %d found at position %d from top.", key, top - i + 1);
            found = 1;
            break;
        }
    }
    if (!found)
        printf("\nElement %d not found in the stack.", key);
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
### Infix to Postfix in c
```c
#include <stdio.h>      // Include standard input-output library
#include <ctype.h>      // Include ctype library for character functions
#include <stdlib.h>     // Include standard library for general utilities

#define SIZE 40         // Define the maximum size of the stack and expression

char stack[SIZE];       // Declare stack array to store characters
int top = -1;           // Initialize top of stack to -1 indicating an empty stack

// Function to push a character onto the stack
void push(char c) {
    if (top >= SIZE - 1) {   // Check for stack overflow
        printf("Stack Overflow\n");
        return;
    }
    stack[++top] = c;        // Increment top and push character onto stack
}

// Function to pop a character from the stack
char pop() {
    if (top == -1) {         // Check for stack underflow
        printf("Stack Underflow\n");
        return '\0';
    } else {
        return stack[top--]; // Return top character and decrement top
    }
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
### Queue Operation
```c
#include <stdio.h>
#include <stdlib.h> // header for using exit and return function

#define max 5 // symbolic constant

int rear = -1, front = -1; // global variables
int queue[max];

void enqueue();
int dequeue();
void display();
void peek();

int main() {
    int w, num;
    while (1) {
        printf("\n1. enqueue");
        printf("\n2. dequeue");
        printf("\n3. Display");
        printf("\n4. Peek");
        printf("\n5. EXIT");
        printf("\nEnter What you want: ");
        scanf("%d", &w);
        if (w == 1)
            enqueue();
        else if (w == 2)
            num = dequeue();
        else if (w == 3)
            display();
        else if (w == 4)
            peek();
        else if (w == 5)
            exit(1);
        else
            printf("\nInvalid Choice!!");
    }

    return 0;
}

void enqueue() {
    int num;
    if (rear == max - 1) {
        printf("\nQueue is Full!\n");
        return;
    }
    printf("\nEnter a number to insert: ");
    scanf("%d", &num);
    if (front == -1)
        front = front + 1;
    rear = rear + 1;
    queue[rear] = num;
}

int dequeue() {
    int num;
    if (front == -1 || front == rear + 1) {
        printf("\nQueue is Empty!\n");
        return 0;
    }
    num = queue[front];
    printf("\n%d was deleted!\n", num);
    front = front + 1;
    return num;
}

void display() {
    int i;
    if (front == -1 || front == rear + 1) {
        printf("\nQueue is Empty! Nothing to display!!\n");
        return;
    }
    printf("\n\n");
    for (i = front; i <= rear; i++)
        printf("%d\t", queue[i]);
    printf("\n");
}

void peek() {
    if (front == -1 || front == rear + 1) {
        printf("\nQueue is Empty!\n");
        return;
    }
    printf("\nThe front element is %d\n", queue[front]);
}
```

### Circular Queue
```c
#include <stdio.h>
#include <stdlib.h> // header for using exit and return function

#define max 5 // symbolic constant

int rear = -1, front = -1; // global variables
int queue[max];

void enqueue();
int dequeue();
void display();
void peek();

int main() {
    int w, num;
    while (1) {
        printf("\n1. Enqueue");
        printf("\n2. Dequeue");
        printf("\n3. Display");
        printf("\n4. Peek");
        printf("\n5. EXIT");
        printf("\nEnter your choice: ");
        scanf("%d", &w);
        if (w == 1)
            enqueue();
        else if (w == 2)
            num = dequeue();
        else if (w == 3)
            display();
        else if (w == 4)
            peek();
        else if (w == 5)
            exit(1);
        else
            printf("\nInvalid Choice!!");
    }

    return 0;
}

void enqueue() {
    int num;
    if ((rear + 1) % max == front) {
        printf("\nQueue is Full!\n");
        return;
    }
    printf("\nEnter a number to insert: ");
    scanf("%d", &num);
    if (front == -1)
        front = 0;
    rear = (rear + 1) % max;
    queue[rear] = num;
}

int dequeue() {
    int num;
    if (front == -1) {
        printf("\nQueue is Empty!\n");
        return 0;
    }
    num = queue[front];
    printf("\n%d was deleted!\n", num);
    if (front == rear) {
        front = rear = -1; // Reset the queue after the last element is dequeued
    } else {
        front = (front + 1) % max;
    }
    return num;
}

void display() {
    int i;
    if (front == -1) {
        printf("\nQueue is Empty! Nothing to display!!\n");
        return;
    }
    printf("\n\nQueue elements:\n");
    if (rear >= front) {
        for (i = front; i <= rear; i++)
            printf("%d\t", queue[i]);
    } else {
        for (i = front; i < max; i++)
            printf("%d\t", queue[i]);
        for (i = 0; i <= rear; i++)
            printf("%d\t", queue[i]);
    }
    printf("\n");
}

void peek() {
    if (front == -1) {
        printf("\nQueue is Empty!\n");
        return;
    }
    printf("\nThe front element is %d\n", queue[front]);
}
```

### Dynamic Circular Queue

```c

#include <stdio.h>
#include <stdlib.h>

struct Queue {
    int *arr;       // Array to store queue elements
    int capacity;   // Maximum capacity of the queue
    int front;      // Front points to the front element in the queue
    int rear;       // Rear points to the last element in the queue
    int size;       // Current number of elements in the queue
};

// Function prototypes
struct Queue *createQueue(int capacity);
void enqueue(struct Queue *queue, int item);
int dequeue(struct Queue *queue);
void display(struct Queue *queue);
void peek(struct Queue *queue);

int main() {
    int choice, item;
    struct Queue *queue = createQueue(5);  // Initial capacity of the queue

    while (1) {
        printf("\n1. Enqueue");
        printf("\n2. Dequeue");
        printf("\n3. Display");
        printf("\n4. Peek");
        printf("\n5. Exit");
        printf("\nEnter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter the element to enqueue: ");
                scanf("%d", &item);
                enqueue(queue, item);
                break;
            case 2:
                item = dequeue(queue);
                if (item != -1)
                    printf("Dequeued element: %d\n", item);
                break;
            case 3:
                display(queue);
                break;
            case 4:
                peek(queue);
                break;
            case 5:
                exit(0);
            default:
                printf("Invalid choice. Please enter again.\n");
        }
    }

    return 0;
}

// Function to create a queue with given capacity
struct Queue *createQueue(int capacity) {
    struct Queue *queue = (struct Queue *)malloc(sizeof(struct Queue));
    if (queue == NULL) {
        printf("Memory allocation failed\n");
        exit(1);
    }
    queue->capacity = capacity;
    queue->front = 0;
    queue->rear = -1;
    queue->size = 0;
    queue->arr = (int *)malloc(queue->capacity * sizeof(int));
    if (queue->arr == NULL) {
        printf("Memory allocation failed\n");
        exit(1);
    }
    return queue;
}

// Function to add an element to the queue
void enqueue(struct Queue *queue, int item) {
    if (queue->size == queue->capacity) {
        printf("Queue is full. Resizing...\n");
        queue->capacity *= 2;  // Double the capacity
        queue->arr = (int *)realloc(queue->arr, queue->capacity * sizeof(int));
        if (queue->arr == NULL) {
            printf("Memory reallocation failed\n");
            exit(1);
        }
    }
    queue->rear = (queue->rear + 1) % queue->capacity;
    queue->arr[queue->rear] = item;
    queue->size++;
}

// Function to remove an element from the queue
int dequeue(struct Queue *queue) {
    if (queue->size == 0) {
        printf("Queue is empty.\n");
        return -1;
    }
    int item = queue->arr[queue->front];
    queue->front = (queue->front + 1) % queue->capacity;
    queue->size--;
    return item;
}

// Function to display the elements of the queue
void display(struct Queue *queue) {
    if (queue->size == 0) {
        printf("Queue is empty.\n");
        return;
    }
    printf("Queue elements: ");
    int i = queue->front;
    for (int count = 0; count < queue->size; count++) {
        printf("%d ", queue->arr[i]);
        i = (i + 1) % queue->capacity;
    }
    printf("\n");
}

// Function to display the front element of the queue
void peek(struct Queue *queue) {
    if (queue->size == 0) {
        printf("Queue is empty.\n");
        return;
    }
    printf("Front element: %d\n", queue->arr[queue->front]);
}


```
