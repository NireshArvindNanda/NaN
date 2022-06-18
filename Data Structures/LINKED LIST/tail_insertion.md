# Inserting a node at the end of the 

https://www.hackerrank.com/challenges/insert-a-node-at-the-tail-of-a-linked-list/problem?isFullScreen=true

## Key points 

  * Don't forget to handle the case when head is ```NULL```
  * Move to last node not outside of the linked list --- ```while(temp->next)```
  * Creation of node in CPP --- ```LinkedListNode* temp = new LinkedListNode(data)```


## Code 

```
SinglyLinkedListNode* insertNodeAtTail(SinglyLinkedListNode* head, int data) {

    SinglyLinkedListNode* temp = new SinglyLinkedListNode(data);
    
    SinglyLinkedListNode *temp1 = head;
    if(!head){head=temp;return head;}
    while(temp1->next){
        temp1=temp1->next;
    }
    temp1->next=temp;
    return head;

}
```

