# Merge Sort

- Here's a simple way to visualize Merge Sort:

- Divide: Split your array of data in half, again and again, until each piece can't be divided further (you'll end up with arrays of just one element).
- Conquer: Now, with each piece being sorted (since it's just one element), you start combining them.
- Merge: As you combine these pieces, you sort them along the way. Think of merging two small stacks of cards where each stack is already in order.

- This process continues until all the small, sorted pieces are merged back into a single, sorted array.


### Algorithm
- Step 1: Create two pointers, one for each sorted half.

- Step 2: Initialize an empty temporary array to hold the merged result.

- Step 3: Compare the elements at the pointers of the two halves:

- Copy the smaller element into the temporary array.

- Move the pointer of the sublist with the smaller element forward.

- Step 4: Repeat step 3 until one of the sublists is empty.

- Step 5: Copy the remaining elements from the non-empty sublist to the temporary array.

- Step 6: Copy the elements back from the temporary array to the original list.


![image](https://github.com/user-attachments/assets/8b2c71c2-8c60-4f44-94f1-ed5e27dacdef)


