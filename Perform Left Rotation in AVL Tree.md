# Ex. No: 16E - Construction of an AVL Tree and Retrieving Its Dictionary Representation Using Python

## AIM:
To construct an AVL (Adelson-Velsky and Landis) tree, a self-balancing binary search tree, from a given list and retrieve its dictionary representation.
## ALGORITHM:
```
1.Import the AVL class from the TreeAVL module.
2.Define a function getDictTree(tree) that returns the dictionary representation of the tree using tree.dict_tree.
3.Define a function Construct_AVL(L) that:
     ->Takes a list of elements L as input.
     ->Constructs an AVL tree using AVL(L).
     ->Prints the dictionary representation of the tree using getDictTree(tree).
4.Call Construct_AVL(L) with a sample list L = [10, 20, 30, 40, 50, 25].
```
## PYTHON PROGRAM

```
from TreeAVL.AVL import AVL

def getDictTree(self):
 return self.dict_tree

def Construct_AVL(L):
    tree=AVL(L)
    print(getDictTree(tree))
L=[10 ,20 ,30 ,40 ,50 ,25]
```

## OUTPUT

<img width="1192" height="291" alt="image" src="https://github.com/user-attachments/assets/4971ba35-494d-4a3d-a248-0211c1d9657b" />

## RESULT
->The program constructs a balanced AVL tree from the input list.

->The dictionary representation of the AVL tree is displayed, showing each node and its children.

->This representation is useful for visualizing the tree structure programmatically.
