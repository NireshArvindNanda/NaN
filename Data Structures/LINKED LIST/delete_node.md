# Deletion of a node ata agiven position

https://www.hackerrank.com/challenges/delete-a-node-from-a-linked-list/problem?isFullScreen=true

## Key points 

  * while deleting a node check for the case of deleting the ```head```
  * while deleting a node check for the case of deleting a tail node becasue there is no ```next``` node
  * Creation of node in CPP --- ```LinkedListNode* temp = new LinkedListNode(data)```

## Points to ponder
  
  * Move to the node just before the node to be deleted
  * From there you can point to the next node to the node to be deleted and then free the memory held by node to be deleted
 
## Aleternatives

  * Given the pointer to the node to be deleted directly rather than the ```head``` you can simply copy the next node's value to the given node point it to the one node away 
  * This makes deletion possible in ```O(1)``` time provided the pointer is given directly


## Code 

```
SinglyLinkedListNode* deleteNode(SinglyLinkedListNode* llist, int position) {

    SinglyLinkedListNode* temp1 = llist, *dummy;
    
    if(position == 0){
        llist = llist->next;
    }
    
    while (temp1->next && position>1) {
        temp1=temp1->next;
        position--;
    }
    if(!temp1->next->next){
    temp1->next=NULL;return llist;}
    else {
        dummy = temp1->next;
        temp1->next = temp1->next->next;
    }
    return llist;

}
```
## Complexity

  * Time --  ```O(n)```
  * Space -- ```O(1)```
