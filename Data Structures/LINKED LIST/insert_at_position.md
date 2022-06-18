# Inserting a node at the head of the linked list

https://www.hackerrank.com/challenges/insert-a-node-at-a-specific-position-in-a-linked-list/problem?isFullScreen=true

## Key points 

  * Don't forget to handle the case when head is ```NULL```
  * If inserting in between then check for the condition of inserting at the tail, becuase at that time you might not have a ```next``` node
  * Handle the case when position is out bound and also check you don't go outside of linked list - ``` while (temp1->next && position>1)```
  * Creation of node in CPP --- ```LinkedListNode* temp = new LinkedListNode(data)```


## Code 

```
SinglyLinkedListNode* insertNodeAtPosition(SinglyLinkedListNode* llist, int data, int position) {
    SinglyLinkedListNode *temp = new SinglyLinkedListNode(data);
    SinglyLinkedListNode* temp1 = llist;
    
    if(!llist){llist=temp;return llist;}
    
    
    while (temp1->next && position>1) {
        temp1=temp1->next;
        position--;
    }
    if(!temp1->next)temp1->next=temp;
    else {
        temp->next = temp1->next;
        temp1->next = temp;
    }
    return llist;
}
```
## Complexity

  * Time --  ```O(n)```
  * Space -- ```O(1)```
