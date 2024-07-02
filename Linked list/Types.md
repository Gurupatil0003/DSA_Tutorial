### LinkedList

![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/cdea48f5-71e4-4e14-93a3-c5324a91ac8f)

- A Singly Linked List is a specialized case of a generic linked list. In a singly linked list, each node links to only the next node in the sequence, i.e. if we start traversing from the first node of the list, we can only move in one direction(pun intended).

![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/d57a5354-8856-41f1-8607-f98e638774a7)


- The Node of the singly linked list, apart from the data, stores the address of only the next element, as shown below. The following is the JAVA representation of a node.

```c
struct Node {
    int data;
    struct Node *next;
};

```
- For a linked list we maintain a special pointer known s HEAD. This pointer stores the address of the first node of the list. Also, the last node can no longer have the next element. Hence we indicate the end of the linked list by assigning NULL to its next.

- ![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/782bda42-0b3e-4853-9f02-79ae748e37ca)

- Whereas linked list shines when we need to modify existing data by insertion and deletion because it doesn't have a fixed size. So, our memory consumption is determined at run time as the linked list shrinks and grows dynamically in constant time.

- Later on, we will explore these linked list operations in-depth but first, let's discuss the types of linked lists.

### Types of Linked List
- There are mainly three types of linked lists:

- Singly Linked List
  Here, we can only traverse in one direction (not the band ) due to the linking of every node to its next nod

  ![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/49421b17-6aca-4789-9d04-d64a34090d07)

 ### Doubly Linked List
 - Here, we can traverse in both directions as every node contains an additional prev pointer that points to the previous node. 
![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/742bc0d4-2c90-42de-a8be-79d5d3960d21)

### Circular Linked List
- Here, we can keep traversing forever and ever until the program crashes as the tail node's next pointer points to the head node instead of a NULL.
![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/6cff17f9-0987-4d56-94c8-5d1eb21221ec)

