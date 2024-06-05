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
