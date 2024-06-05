# Linked List
- A Linked List is a linear data structure consisting of connected nodes where each node has corresponding data and a pointer to the address of the next node. The first node of a linked list is called the Head, and it acts as an access point. On the other hand, the last node is called the Tail, and it marks the end of a linked list by pointing to a NULL value!

## Why Do We Need a Linked List?
```c
Imagine going to a movie theater along with a large group of friends, only to find out there's no way to book consecutive seats to accommodate all. However, there are plenty of disjoint empty seats for that particular screen. So, you all buy tickets and sit accordingly.

But there's a catch!

Since only you were buying popcorn for all, how would you distribute that to your friends? You can't remember where everyone sat, and it's dark inside the hall.

So, instead of you remembering where everyone sat, if everyone kept track of the next friend's seat, then such reference would help popcorn tubs to traverse up to a friend who's yet to get popcorn. This could be achieved by passing popcorn to the next friend starting from you!
```
![image](https://github.com/Gurupatil0003/DSA_Tutorial/assets/110026505/a1bfd12a-d4f9-4a7d-bf21-c251a22ed543)

- See how the linked list came in handy while keeping track of all these randomly distributed disjoint seats?

- In a computer, you can think of memory as a movie theatre, the virtual address space as the seats, and any particular memory address as a seat number.

- Note: The virtual address space refers to the address range on which a process relies in order to carry out its execution. Unlike seats, this address space is virtual and not real. It's a logical and abstracted mapping to a rather intricate physical memory.

- Now, if we had initiated booking in advance, we could have booked an entire row of consecutive seats much like an array does when we declare it with a fixed size in advance, like so:

- int seats[24];

- In our context of a movie theater, if more friends later decide to join the group to catch the movie. We cannot simply append them to the array of seats since there might be other audiences seating just after the last allocated seat.

- So either we find another larger empty row of consecutive seats so that all friends can sit together (much like dynamic array), or we rely on an approach similar to the linked list, in that we simply insert new friends in vacant spots but still have references to them should we require to pass popcorn and drinks.

- You see, arrays are suitable when we need fast access. Like who's seating at seat no. 13 can be answered in constant time! But arrays require you to declare a fixed size at the compile-time, due to which memory can be either wasted or fell short.
