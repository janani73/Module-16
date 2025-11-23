# Ex. No: 16B - Insertion and Preorder Traversal in an AVL Tree Using Python

## AIM:
To construct a self-balancing AVL tree, insert multiple nodes while maintaining the AVL property, and display the tree using preorder traversal.
## ALGORITHM:
```
1.Define a TreeNode class:
      ->Each node stores val, left, right, and height.
2.Define an AVL_Tree class with methods:
       ->insert(root, key):
             ->Recursively insert a node in BST fashion.
             ->Update node height.
             ->Compute the balance factor.
             ->Perform rotations if the tree becomes unbalanced:
                   ->Right rotation, left rotation, left-right rotation, right-left rotation.
             ->leftRotate(z) / rightRotate(z): Rotate subtrees to maintain balance.
             ->getHeight(root): Return the height of a node.
             ->getBalance(root): Return the difference in height between left and right subtrees.
             ->preOrder(root): Print nodes in preorder traversal (root → left → right).
3.Initialize the AVL tree object and root = None.
4.Insert nodes:
        ->Fixed nodes: 13, 10, 15, 5, 11, 16
        ->User input n is also inserted to demonstrate dynamic insertion.
5.Display the tree using preorder traversal.
```
## PYTHON PROGRAM
```
class TreeNode(object):
	def __init__(self, val):
		self.val = val
		self.left = None
		self.right = None
		self.height = 1
class AVL_Tree(object):
	def insert(self, root, key):
		if not root:
			return TreeNode(key)
		elif key < root.val:
			root.left = self.insert(root.left, key)
		else:
			root.right = self.insert(root.right, key)
		root.height = 1 + max(self.getHeight(root.left),
						self.getHeight(root.right))
		balance = self.getBalance(root)
		if balance > 1 and key < root.left.val:
			return self.rightRotate(root)
		if balance < -1 and key > root.right.val:
			return self.leftRotate(root)
		if balance > 1 and key > root.left.val:
			root.left = self.leftRotate(root.left)
			return self.rightRotate(root)
		if balance < -1 and key < root.right.val:
			root.right = self.rightRotate(root.right)
			return self.leftRotate(root)
		return root
	def leftRotate(self, z):
	    y=z.right
	    T2=y.left
	    y.left=z
	    z.right=T2
	    z.height=1+max(self.getHeight(z.left),self.getHeight(z.right))
	    y.height=1+max(self.getHeight(y.left),self.getHeight(y.right))
	    return y
	def getHeight(self, root):
		if not root:
			return 0
		return root.height
	def getBalance(self, root):
		if not root:
			return 0
		return self.getHeight(root.left) - self.getHeight(root.right)
	def preOrder(self, root):
		if not root:
			return
		print("{0} ".format(root.val), end="")
		self.preOrder(root.left)
		self.preOrder(root.right)
myTree = AVL_Tree()
root = None
n=int(input())
root = myTree.insert(root, 13)
root = myTree.insert(root, 10)
root = myTree.insert(root, 15)
root = myTree.insert(root, 5)
root = myTree.insert(root, 11)
root = myTree.insert(root, 16)
root = myTree.insert(root, n)
print("Preorder traversal of the constructed AVL tree is")
myTree.preOrder(root)
print()


```

## OUTPUT
<img width="1172" height="273" alt="image" src="https://github.com/user-attachments/assets/7a02605e-f6ca-4378-8eef-145f02fec77a" />

## RESULT
->The program constructs an AVL tree by dynamically inserting nodes.

->The AVL property (balanced tree) is maintained after each insertion.

->Preorder traversal displays the tree hierarchy starting from the root.
