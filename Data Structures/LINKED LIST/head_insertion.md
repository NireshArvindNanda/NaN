# Inserting a node at the head of the linked list

https://www.hackerrank.com/challenges/insert-a-node-at-the-head-of-a-linked-list/problem

## Key points 

  * Don't forget to handle the case when head is ```NULL```
  * Creation of node in CPP --- ```LinkedListNode* temp = new LinkedListNode(data)```


## Code 

```
SinglyLinkedListNode* insertNodeAtHead(SinglyLinkedListNode* llist, int data) {

    SinglyLinkedListNode *temp = new SinglyLinkedListNode(data);
    if(!llist){llist=temp;return llist;}
    temp->next = llist;
    llist=temp;
    return llist;

}
```
## Complexity

  * Time --  ```O(1)```
  * Space -- ```O(1)```
