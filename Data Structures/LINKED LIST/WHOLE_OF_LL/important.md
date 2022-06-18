# Some of the important points when touching on a linked list problem

## Runtime errors

  * head might be ```NULL```
  * you might have moved out of the linked list
  * you are trying to access a node out bound like this  -- ```temp->next ``` when temp is actually ```NULL```

## Edge cases

* Check if head might be ```NULL``` i.e. the linked list is empty
* If inserting in between then check for the condition of inserting at the tail, becuase at that time you might not have a ```next``` node
* while deleting a node check for the case of deleting the head when there is only one element in linked list
* while deleting a node check for the case of deleting a tail node becasue there is no ```next``` node
* 
