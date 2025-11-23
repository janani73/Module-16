# Ex. No: 16A - Construction of an AVL Tree Using Python

## AIM:
To demonstrate the creation of an AVL (Adelson-Velsky and Landis) tree, a self-balancing binary search tree, and display its length.
## ALGORITHM:
```
1.Import the AVL class from the TreeAVL module.
2.Define a function Construct_AVL(L) that:
       ->Takes a list L of elements as input.
       ->Creates an AVL tree using AVL(L).
3.Prints the length of the tree using tree.length_tree.
4.Call Construct_AVL(L) with a sample list of elements to construct the tree.
```
## PYTHON PROGRAM
```
from TreeAVL.AVL import AVL
def Construct_AVL(L):
    tree=AVL(L)
    print("Length of an AVL Tree is",tree.length_tree)
```

## OUTPUT
<img width="1180" height="197" alt="image" src="https://github.com/user-attachments/assets/02d44643-08b3-4685-999c-060d09a31792" />

## RESULT
->The program constructs an AVL tree from the input list.

->The tree automatically balances itself after insertions.

->The length of the AVL tree is displayed, representing the number of nodes.
