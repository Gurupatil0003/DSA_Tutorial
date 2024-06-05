
- Queues are another Abstract Data Type (ADT), that might be implemented using concrete structures like arrays and linked lists. We refer to Queue behaviour by FIFO (first in, first out).

- The ADT Queue should satisfy the following requirements (from wikipedia):

- enqueue, which adds an element to the collection end (back), and.
- dequeue, which removes the first element added (front) that was not yet removed.

- This makes the queue a First-In-First-Out (FIFO) data structure. In a FIFO data structure, the first element added to the queue will be the first one to be removed. Additionally, a peek operation may give 
 access to the front element without dequeuing it. – Queue (Abstract Data Type)

### Queue Operations

| Operation | Description                                                                                      |
|-----------|--------------------------------------------------------------------------------------------------|
| Enqueue   | Adds an element to the rear or end of the queue.                                                  |
| Dequeue   | Removes and returns the element from the front of the queue, maintaining FIFO order.              |
| Peek      | Allows viewing the element at the front of the queue without removing it.                         |
| isEmpty   | Checks if the queue is empty. Returns true if the queue contains no elements, false otherwise.    |
| isFull    | Checks if the queue is full. Returns true if the queue is at maximum capacity, false otherwise.  |

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
  
