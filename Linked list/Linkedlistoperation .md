### Linkedlist Creation ,Insertion and Display
```c
#include<stdio.h>
#include<stdlib.h>

struct Node
{
  int data;
  struct Node *next;
};

void insertStart (struct Node **head, int data)
{

  struct Node *newNode = (struct Node *) malloc (sizeof (struct Node));

  newNode->data = data;
  newNode->next = *head;

  //changing the new head to this freshly entered node
  *head = newNode;
}

void display (struct Node *node)
{

  //as linked list will end when Node is Null
  while (node != NULL)
    {
      printf ("%d ", node->data);
      node = node->next;
    }
  printf ("\n");
}

int main ()
{

  //creating 4 pointers of type struct Node
  //So these can point to address of struct type variable
  struct Node *head = NULL;
  struct Node *node2 = NULL;
  struct Node *node3 = NULL;
  struct Node *node4 = NULL;

  // allocate 3 nodes in the heap 
  head = (struct Node *) malloc (sizeof (struct Node));
  node2 = (struct Node *) malloc (sizeof (struct Node));
  node3 = (struct Node *) malloc (sizeof (struct Node));
  node4 = (struct Node *) malloc (sizeof (struct Node));


  head->data = 15;		// data set for head node 
  head->next = node2;		// next pointer assigned to address of node2 

  node2->data = 10;
  node2->next = node3;

  node3->data = 12;
  node3->next = node4;

  node4->data = 3;
  node4->next = NULL;

  printf ("Linklist : ");
  display (head);

  // Need '&' i.e. address as we need to change head
  insertStart (&head, 25);

  printf ("\nAfter Inserting Element\n");
  printf ("\nLinklist : ");
  // no need for '&' as head need not be changed
  // only doing traversal
  display (head);
  return 0;
}
```

### LastInsertion
```c
#include<stdio.h>
#include<stdlib.h>

struct Node
{
  int data;
  struct Node *next;
};

void insertStart (struct Node **head, int data)
{

  struct Node *newNode = (struct Node *) malloc (sizeof (struct Node));

  newNode->data = data;
  newNode->next = *head;

  //changing the new head to this freshly entered node
  *head = newNode;
}

void insertLast (struct Node **head, int data)
{

  struct Node *newNode = (struct Node *) malloc (sizeof (struct Node));

  newNode->data = data;
  newNode->next = NULL;

  //need this if there is no node present in linked list at all
  if (*head == NULL)
    {
      *head = newNode;
      return;
    }

  struct Node *temp = *head;

  while (temp->next != NULL)
    temp = temp->next;

  temp->next = newNode;
}

void display (struct Node *node)
{

  //as linked list will end when Node is Null
  while (node != NULL)
    {
      printf ("%d ", node->data);
      node = node->next;
    }
  printf ("\n");
}

int main ()
{
  struct Node *head = NULL;

  // Need '&' i.e. address as we need to change head
  insertStart (&head, 12);
  insertStart (&head, 16);
  insertStart (&head, 20);

  insertLast (&head, 10);
  insertLast (&head, 14);
  insertLast (&head, 18);
  insertLast (&head, 11);

  // no need for '&' as head need not be changed
  // only doing traversal
  display (head);
  return 0;
}
```
