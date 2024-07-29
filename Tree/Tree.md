# Tree

- To retrace our steps a bit, a tree data structure is a way of organizing data in a hierarchical manner. Just like in nature, trees in our computer world come in 
 many shapes and sizes. For our purposes, let’s visualize one that looks as follows:

![image](https://github.com/user-attachments/assets/a8b1207d-c663-4e72-887c-402a6fd0a99c)


- We see a bunch of circles and lines connecting each circle. Each circle in the tree is known as a node. The node plays an important role in a tree. It is 
 responsible - for storing data, and it is also responsible for linking to other nodes. The link (visualized as a line) between each node is known as an edge:

![image](https://github.com/user-attachments/assets/37747cea-6871-40d6-91a7-cb535a2c20a6)


![tree-1](https://github.com/user-attachments/assets/cd422347-6d1c-4ec7-96bf-f902f62fbd85)

# Trees in Data Structures     ![tree](https://github.com/user-attachments/assets/d0a72a05-e5bf-42ed-aae6-5bb0708268d9)

- A tree is a hierarchical data structure, which has one root node and multiple child nodes(branches). Unlike, Arrays, Linked Lists, Stacks or queues, a Tree is non 
  linear data structure.



## Classification of Trees
- Trees are classified by the following types – ![tree-1](https://github.com/user-attachments/assets/8bbf1b60-cf17-48dd-a61c-2288d0317c30)

```c
By Max number of branches – Binary, Ternary, n-ary
By Heights of subtree – Full, complete, perfect, balanced (Check this page)
The following diagram shows one example of each –

Binary Tree: A tree where each node can have a maximum of two child nodes
Ternary Tree: A tree where each node can have a maximum of three child nodes
n-ary Tree: A tree where each node can have a maximum of n child nodes
This n value is sometimes called as the degree of the tree.

```

## Why Trees?   ![architecture-and-city](https://github.com/user-attachments/assets/6fc0b239-ad32-40fd-a9b2-51a2d6f7d23d)

```c
Hierarchical approach
```
- One reason could be that we want to store information that follows, natural hierarchy, like how we store folders in a computer system.
```c
No Upper Limit
```
- Trees, unlike arrays, stacks, queues do not have an upper limit on how many nodes can be created, as they are created using pointers
```c
Quicker Search and Access
```
- Trees (BST) are able to do searching quicker than arrays, linked lists etc
```c
Moderate Insertion/Deletion
```
- Trees provide moderate insertion/deletion (Slower than Linked lists, quicker than arrays)
 Trees

### Technical Description of Trees  ![introduction](https://github.com/user-attachments/assets/dcb9501b-6494-4cfe-9aa5-ab8f17027386)

- Trees can defined as a collection of  entities, that constitute it’s frame, known as nodes.
- Nodes are the basic building blocks of a tree structure that store some data/value .
- These are  ADT (Abstract Data Structures) which form a hierarchical layout comprising of a single root node followed by parent nodes and children nodes, which 
 are connected to each other via edges.

- Since trees are flexible and powerful data structures, they are multipurpose data structure that provide a wide range of applications to the user.
