# Queue
- A queue is a useful data structure in programming. It is similar to the ticket queue outside a cinema hall, where the first person entering the queue is the 
 first person who gets the ticket.

- Queue follows the First In First Out (FIFO) rule - the item that goes in first is the item that comes out first.

![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/f2877ada-21e4-4634-9071-9135e932432e)

- In the above image, since 1 was kept in the queue before 2, it is the first to be removed from the queue as well. It follows the FIFO rule.

- In programming terms, putting items in the queue is called enqueue, and removing items from the queue is called dequeue.

- We can implement the queue in any programming language like C, C++, Java, Python or C#, but the specification is pretty much the same.

### Queue Operations

| Operation | Description                                                                                      |
|-----------|--------------------------------------------------------------------------------------------------|
| Enqueue   | Adds an element to the rear or end of the queue.                                                  |
| Dequeue   | Removes and returns the element from the front of the queue, maintaining FIFO order.              |
| Peek      | Allows viewing the element at the front of the queue without removing it.                         |
| isEmpty   | Checks if the queue is empty. Returns true if the queue contains no elements, false otherwise.    |
| isFull    | Checks if the queue is full. Returns true if the queue is at maximum capacity, false otherwise.  |


## Working of Queue
### Queue operations work as follows:

- 1.two pointers FRONT and REAR
- 2.FRONT track the first element of the queue
- 3.REAR track the last element of the queue
- 4.initially, set value of FRONT and REAR to -1

## Enqueue Operation
- 1.check if the queue is full
- 2.for the first element, set the value of FRONT to 0
- 3.increase the REAR index by 1
- 4.add the new element in the position pointed to by REAR
## Dequeue Operation
- 1.check if the queue is empty
- 2.return the value pointed by FRONT
- 3.increase the FRONT index by 1
- 4.for the last element, reset the values of FRONT and REAR to -1

![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/35e1637d-0dcf-440c-953a-be572fdbcd32)

## Example
```c
// Queue implementation in C

#include <stdio.h>
#define SIZE 5

void enQueue(int);
void deQueue();
void display();

int items[SIZE], front = -1, rear = -1;

int main() {
//deQueue is not possible on empty queue
deQueue();

//enQueue 5 elements
enQueue(1);
enQueue(2);
enQueue(3);
enQueue(4);
enQueue(5);

// 6th element can't be added to because the queue is full
enQueue(6);

display();

//deQueue removes element entered first i.e. 1
deQueue();

//Now we have just 4 elements
display();

return 0;
}

void enQueue(int value) {
if (rear == SIZE - 1)
printf("\nQueue is Full!!");
else {
if (front == -1)
front = 0;
rear++;
items[rear] = value;
printf("\nInserted -> %d", value);
}
}

void deQueue() {
if (front == -1)
printf("\nQueue is Empty!!");
else {
printf("\nDeleted : %d", items[front]);
front++;
if (front > rear)
front = rear = -1;
}
}

// Function to print the queue
void display() {
if (rear == -1)
printf("\nQueue is Empty!!!");
else {
int i;
printf("\nQueue elements are:\n");
for (i = front; i <= rear; i++)
printf("%d  ", items[i]);
}
printf("\n");
}
```
## Limitations of Queue
- As you can see in the image below, after a bit of enqueuing and dequeuing, the size of the queue has been reduced.
- ![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/c7f8e7c9-5511-429b-9ed4-9a22a8134a24)
- And we can only add indexes 0 and 1 only when the queue is reset (when all the elements have been dequeued).
- After REAR reaches the last index, if we can store extra elements in the empty spaces (0 and 1), we can make use of the empty spaces. This is implemented by a 
 modified queue called the circular queue.

## Complexity Analysis
- The complexity of enqueue and dequeue operations in a queue using an array is O(1). If you use pop(N) in python code, then the complexity might be O(n) 
 depending on the position of the item to be popped.

## Applications of Queue
- CPU scheduling, Disk Scheduling
- When data is transferred asynchronously between two processes.The queue is used for synchronization. For example: IO Buffers, pipes, file IO, etc
  Handling of interrupts in real-time systems.
- Call Center phone systems use Queues to hold people calling them in order.

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 5

typedef struct {
    int items[MAX_SIZE];
    int front;
    int rear;
} Queue;

void initializeQueue(Queue *queue) {
    queue->front = -1;
    queue->rear = -1;
}

int isEmpty(Queue *queue) {
    return (queue->front == -1 && queue->rear == -1);
}

int isFull(Queue *queue) {
    return (queue->rear + 1) % MAX_SIZE == queue->front ? 1 : 0;
}

void enqueue(Queue *queue, int value) {
    if (isFull(queue)) {
        printf("Queue is full. Cannot enqueue.\n");
        return;
    } else if (isEmpty(queue)) {
        queue->front = 0;
    }
    queue->rear = (queue->rear + 1) % MAX_SIZE;
    queue->items[queue->rear] = value;
    printf("Enqueued: %d\n", value);
}

int dequeue(Queue *queue) {
    if (isEmpty(queue)) {
        printf("Queue is empty. Cannot dequeue.\n");
        return -1;
    } else if (queue->front == queue->rear) {
        int value = queue->items[queue->front];
        queue->front = -1;
        queue->rear = -1;
        printf("Dequeued: %d\n", value);
        return value;
    } else {
        int value = queue->items[queue->front];
        queue->front = (queue->front + 1) % MAX_SIZE;
        printf("Dequeued: %d\n", value);
        return value;
    }
}

int peek(Queue *queue) {
    if (isEmpty(queue)) {
        printf("Queue is empty. Cannot peek.\n");
        return -1;
    } else {
        printf("Front element: %d\n", queue->items[queue->front]);
        return queue->items[queue->front];
    }
}

int main() {
    Queue myQueue;
    initializeQueue(&myQueue);

    enqueue(&myQueue, 10);
    enqueue(&myQueue, 20);
    enqueue(&myQueue, 30);

    peek(&myQueue);

    dequeue(&myQueue);
    peek(&myQueue);

    enqueue(&myQueue, 40);

    return 0;
}
```

### Array Representation:
- Using an array to represent a queue is one of the simplest ways to implement it. In this approach, we use a fixed-size array to store the elements of the queue. Two pointers, front and rear, are used to keep 
 track of the front and rear of the queue, respectively.

##Operations:
### Enqueue Operation (enqueue):
```c
- When an element is inserted into the queue, it is added to the rear end.
 We increment the rear pointer to the next available position in the array and place the new element there.
 If the queue is empty initially, both front and rear are set to 0.
```


### Dequeue Operation (dequeue):
```c

When an element is removed from the queue, it is always removed from the front end.
We increment the front pointer to point to the next element to be dequeued.
If the queue becomes empty after dequeuing, both front and rear are reset to -1 to indicate an empty queue.
```

### Empty and Full Checks (isEmpty and isFull):
```c
isEmpty checks if the queue is empty by inspecting the value of front.
isFull checks if the queue is full by inspecting the value of rear in relation to the maximum capacity of the array.
```
### Implementation:
- We use a fixed-size array to hold the elements of the queue.
- Two pointers, front and rear, are used to maintain the position of the front and rear elements.
- enqueue adds elements to the rear and updates rear.
- dequeue removes elements from the front and updates front.
- isEmpty and isFull check if the queue is empty or full, respectively.
- If the rear pointer reaches the end of the array, it can either wrap around (circular queue) or resize the array.

### Advantages and Disadvantages:
- Advantages:
```c
Simple and easy to implement.
Constant time complexity for enqueue and dequeue operations (O(1)).
```

- Disadvantages:
```c
Limited by the size of the array.
May lead to memory wastage if the array is larger than necessary.
Resizing the array (if dynamic) can be expensive (O(n)).
```
### Implementation
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

// Structure to represent a queue
struct Queue {
    int items[MAX_SIZE];
    int front;
    int rear;
};

// Function to create a new queue
struct Queue* createQueue() {
    struct Queue* queue = (struct Queue*)malloc(sizeof(struct Queue));
    queue->front = -1;
    queue->rear = -1;
    return queue;
}

// Function to check if the queue is full
int isFull(struct Queue* queue) {
    return queue->rear == MAX_SIZE - 1;
}

// Function to check if the queue is empty
int isEmpty(struct Queue* queue) {
    return queue->front == -1;
}

// Function to add an element to the queue
void enqueue(struct Queue* queue, int value) {
    if (isFull(queue)) {
        printf("Queue is full\n");
        return;
    }
    if (isEmpty(queue)) {
        queue->front = 0;
    }
    queue->rear++;
    queue->items[queue->rear] = value;
}

// Function to remove an element from the queue
int dequeue(struct Queue* queue) {
    int item;
    if (isEmpty(queue)) {
        printf("Queue is empty\n");
        return -1;
    }
    item = queue->items[queue->front];
    if (queue->front >= queue->rear) {
        queue->front = -1;
        queue->rear = -1;
    } else {
        queue->front++;
    }
    return item;
}

// Function to display the elements of the queue
void display(struct Queue* queue) {
    int i;
    if (isEmpty(queue)) {
        printf("Queue is empty\n");
        return;
    }
    printf("Queue elements are:\n");
    for (i = queue->front; i <= queue->rear; i++) {
        printf("%d ", queue->items[i]);
    }
    printf("\n");
}

int main() {
    struct Queue* queue = createQueue();

    enqueue(queue, 1);
    enqueue(queue, 2);
    enqueue(queue, 3);
    enqueue(queue, 4);

    display(queue);

    printf("Dequeuing element: %d\n", dequeue(queue));
    printf("Dequeuing element: %d\n", dequeue(queue));

    display(queue);

    enqueue(queue, 5);
    enqueue(queue, 6);

    display(queue);

    return 0;
}
```
![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/1d0eed57-169f-40eb-84f6-79c877c53def)

# circular queue
- A circular queue, also known as a circular buffer or ring buffer, is a data structure that uses a single, fixed-size buffer as if it were connected end-to-end. This structure supports efficient addition and removal of elements in a FIFO (First-In-First-Out) manner. It overcomes the limitations of a simple linear queue by reusing the empty space when elements are removed from the front.
- Circular Queue is a linear data structure in which the operations are performed based on FIFO (First In
 First Out) principle and the last position is connected back to the first position to make a circle. It is also 
 called ‘Ring Buffer’.
- ![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/531dbd36-9107-4c47-a268-11c983d1df75)

- In a normal Queue, we can insert elements until queue becomes full. But once queue becomes full, we 
 can not insert the next element even if there is a space in front of queue.

- ![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/c1f67fed-f46b-4cb7-802e-f3514b45cd71)

- The Queue shown in above figure is completely filled and there can't be inserted any more element due to the 
 condition rear == max - 1 becomes true.
- However, if we delete 2 elements at the front end of the queue, we still can not insert any element since the 
 condition rear = max -1 still holds.
- This is the main problem with the linear queue, although we have space available in the array, but we can not 
  insert any more element in the queue. This is simply the memory wastage and we need to overcome this problem

  ![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/ae8d452a-46f8-4e9b-a74a-4ff9f392ddc1)
One of the solution of this problem is circular queue. In the circular queue, the first index comes right after the last 
index. You can think of a circular queue as shown in the following figure.


![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/0f593f51-c651-47ca-bc7d-14680e27bfa9)
- Circular queue will be full when front = -1 and rear = max-1. Implementation of circular queue is similar to that 
 of a linear queue. Only the logic part that is implemented in the case of insertion and deletion is different from that 
 in a linear queue.


- Circular queues using dynamic arrays in C can be an efficient way to manage queues where elements are enqueued and dequeued frequently. The idea behind a circular queue is that the end of the queue wraps around 
 to the beginning, allowing efficient use of space.

- Here's an explanation with a basic implementation of a circular queue using dynamic arrays in C:

### Concepts
- Circular Queue: A circular queue is a linear data structure that follows the FIFO (First In First Out) principle but connects the end of the queue back to the front, forming a circle.

- Dynamic Array: An array that can resize itself automatically when more elements are added than its current capacity. This involves creating a new array of larger size and copying the elements from the old array 
 to the new array.

### Basic Operations
- Enqueue: Add an element to the end of the queue.
- Dequeue: Remove an element from the front of the queue.
- Resize: Increase the capacity of the array when it's full.

### Implementation
- Here's a simple implementation of a circular queue using dynamic arrays in C:
  
