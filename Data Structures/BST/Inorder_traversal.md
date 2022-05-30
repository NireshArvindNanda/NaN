
# Inorder Traversal of BST

[https://leetcode.com/problems/binary-tree-inorder-traversal/](https://leetcode.com/problems/binary-tree-inorder-traversal/)

## Problem Statement

Inroder traversal is a kind a of ```depth-first``` search
which visits all the nodes in a tree. When it comes to a BST, inorder
traversal visits the nodes in ```sorted``` order which makes it 
the ideal traversal used for finding any ordering among the nodes.

## Recursive approach

* **Approach to solve**

    * Visit the root node

    * If there is a left node visit that first, recursively until leaf node

    * Process the node after you have reached the leaf node

    * Recurse through the right subtree

* **Code**

```
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> v;
        helper(root,v);
        return v;
    }
    void helper(TreeNode* root,vector<int> &v){
        if(root==NULL)return;
        helper(root->left,v);
        v.push_back(root->val);
        helper(root->right,v);
    }
};
```

* **Time Complexity** O(n)
* **Space Complexity** O(n) - stack call space

## Iterative approach

* **Approach to solve**

    * Visit the root node

    * If the stack is not empty or there are nodes to be processed, add the current node to the stack and process and visit its left subtree

    * If you have reached a leaf node, save that node and pop it from the stack and visit the right subtree

* **Code**

```
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> v;
        stack<TreeNode*> s;
        TreeNode* curr = root;
        
        while(!s.empty() || curr!=NULL){
            if(curr!=NULL){
                s.push(curr);
                curr=curr->left;
            }else{
                curr=s.top();
                s.pop();
                v.push_back(curr->val);
                curr=curr->right;
            }
        }
        return v;
    }
};
```

* **Data structures used**
    * Stack 

* **Library function**
    * [stack](https://www.geeksforgeeks.org/stack-in-cpp-stl/) - LIFO data structure

* **Time Complexity** O(n)
* **Space Complexity** O(n) - usually the height of tree, for skewed tree O(n)

## Morris traversal

* **Approach to solve**

    *   Look carefully and you will notice that inorder traversal
        is nothing but the traversing the tree from left to right 
        in an ordered fashion

    *   This approach leverages the fact that in the inorder traversal,
        the previous and the next term of a node is simply the predecessor and 
        successor of the node. We can ignore the successor

    *   We can somehow connect the predecessor node of the currrent to the
        current node


* **Pseudocode**       

    *   Visit a node

    *   If it does not have a left subtree then simply Process
        the current node and move to the right subtree

    *   Else, find its indorder predecessor by moving the rightmost 
        node of its left subtree and connect that predecessor's right to the
        current node

    *   After the connection, later on you can process the current node. Now
        you can move to left subtree and repeat the above from step 2

    *   Later on you will have to come back to the same node to print and to break 
        the connection to the successor

    *   Hence, a node will be visited 3 times at most


* **Time Complexity** O(n)
* **Space Complexity** O(1)
