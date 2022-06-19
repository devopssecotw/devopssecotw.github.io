Q: Find duplicated e-mail address;  
A: 
Group e-mail address,Sum it,filter the sum number

Q: reverse linked list 
A: 
LinkedList
Steps:
A->B->C->D->E->null

Node tmp=cur.next;
cur.next=prev;
prev=cur;
cur=tmp;

null<-A<-B<-C<-D<-E

Q: LCA lowest common ancestor 
A:  Binary search tree
TreeNode in ConcurrentHashMap
```
    static final class TreeNode<K,V> extends Node<K,V> {
        TreeNode<K,V> parent;  // red-black tree links
        TreeNode<K,V> left;
        TreeNode<K,V> right;
        boolean red = true;
    }
```
findLca(root,p,q){
    Node node=root;
    while(node!=null){
        var rValue=node.value;
        var pValue=p.value;
        var qValue=q.value;
        if(pValue>rValue&&qValue>rValue){
            node=node.right;
        }else if(pValue<rValue&&qValue<rValue){
            node=node.left;
        }else{
            return node;
        }
    }
}

Q: iterate a tree; reverse order of a tree
A: DFS depth first search; BFS breadth first search


Q: 
Two Sum : Given an array of integers, find two numbers such that they add up to a specific target number.
A: 
Array, Hash Table
b=c-a
put the b as key and index of a in the array to the hash table

Q: Add Two Numbers : You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return the sum as a linked list.
A: linked list, math
class LinkedNextNode{
    int val;
    LinkedNextNode next;
    LinkedNextNode(int x){
        val=x;
    }
}

Q: Longest Substring Without Repeating Characters: Find a string containing the longest substring without repeating characters.
A: 
 

Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


Q: 
A: 


A: 

