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

### Technical Description of Trees  

- Trees can defined as a collection of  entities, that constitute it’s frame, known as nodes.
- Nodes are the basic building blocks of a tree structure that store some data/value .
- These are  ADT (Abstract Data Structures) which form a hierarchical layout comprising of a single root node followed by parent nodes and children nodes, which 
 are connected to each other via edges.

- Since trees are flexible and powerful data structures, they are multipurpose data structure that provide a wide range of applications to the user.

![introduction](https://github.com/user-attachments/assets/dcb9501b-6494-4cfe-9aa5-ab8f17027386)


## Components
```c
Root
Parent
Child nodes
Siblings
Leaves
Brach
Sub-Tree
Ancestor
Descendants
Null Nodes
```
## other Components
```c
Degree
Edges
Path
Depth
Level
Height
```

### 1. Root  ![image](https://github.com/user-attachments/assets/1056facf-9094-4ed5-8a9f-931101a38666)


```c
The topmost node of  a tree is known as the root.
There exists only one root node per tree.
Taking the image above as reference, node ‘a’ is the root of the tree as shown here.

```

### 2. Parent ![parent](https://github.com/user-attachments/assets/43b17fda-0b6d-47f3-ad93-62ef9bcd2645)

```c
Any node which has an edge directed downwards to the child node is known as parent node.
Each parent can have one or more child node.
In the given image we can see, the node ‘a’ is the parent of the nodes ‘b’ and ‘c’.
```
3. Child Node
Any node which has an edge directed upwards to the parent node is known as child node.
Each child node has a single parent node.
In the given image we can see, the nodes ‘h’ and ‘i’ are the child nodes of the node ‘d’.
child
4. Sibling
A set of nodes that are extended from the same parent are known as the siblings.
In the given image, we can see that
the nodes ‘b’ and ‘c’ are sibling nodes. 
the nodes ‘h’ and ‘i’  are sibling nodes.
sibling
5. Leaf(external nodes)
Any node that does not have any child node is known as the leaf node.
In the given image, the nodes ‘f’, ‘h’, ‘i’, ‘j’, ‘k’, ‘l’ and ‘m’ are leaf nodes since these nodes are terminal and have no further child nodes.
Total Number of leaf nodes in a Binary Tree = Total Number of nodes with 2 children + 1

leaf
6. Branch(internal nodes)
Any node which has at least one child node is known as branch node.
In the given image, the nodes ‘b’ , ‘c’ , ‘d’ , ‘e’ , ‘g’ are branch nodes since each of these nodes extend further to their respective children.
branch
7. Sub-Tree
A sub tree of a tree is defined as a tree that consist of a node along with all it’s descendants.
In the image , we can see that a sub tree can be extended from node ‘b’ which will be termed as the left sub tree.
Similarly, a sub tree can be extended from the node ‘c’ which will be termed as the right sub tree. 
subtree
8. Ancestor
Any predecessor of a node along with all the ancestors of the predecessor of that node is known is as the ancestor.
The root node has no ancestors.
In the given image, the ancestors of the node ‘h’ will be ‘d’, ‘b’ and ‘a’.
ancestors
9. Descendant
All the children of a node along with all the descendants of the children of a node is known as descendant.
A leaf node has no descendants.
In the given image, if we consider the node ‘c’, the descendants of node ‘c’ will be nodes ‘f’ , ‘g’ , ‘l’ and ‘m’ .
descendant
10. Null Nodes
If in a binary tree, a node has only one child it is said to have a single null link.
Similarly if a node has no child node it is said to have two null links.
We can see in the image given the two cases of null links.
null link
Terminologies
