# Ex. No: 16C - Implementation of B-Tree Using Python

## AIM:
To demonstrate insertion and splitting operations in a B-Tree, a self-balancing search tree used in databases and file systems, and display its structure.

## ALGORITHM:
```
1.Define BTreeNode class:
        ->Stores keys, child nodes, and leaf status.
2.Define BTree class with minimum degree t:
        ->insert(k): Insert a key-value pair into the B-Tree.
              ->If the root is full, create a new root, split the child, and insert the key.
              ->Else, call insert_non_full() on the root.
        ->insert_non_full(x, k):
              ->If x is a leaf, insert key k in sorted order.
              ->Else, find the child to traverse; if the child is full, split it, then insert recursively.
        ->split_child(x, i):
              ->Split the full child x.child[i] into two nodes and promote the middle key to parent x.
        ->print_tree(x, l): Recursively prints the tree level-wise.
3.Demo usage in main():
        ->Create a B-Tree with t = 3.
        ->Insert key-value pairs (i, 2*i) for i = 0 to 9.
        ->Print the tree.
        ->Insert a new key (11,) to demonstrate dynamic insertion.
        ->Print the updated tree.
```
## PYTHON PROGRAM

```
class BTreeNode:
  def __init__(self, leaf=False):
    self.leaf = leaf
    self.keys = []
    self.child = []
class BTree:
  def __init__(self, t):
    self.root = BTreeNode(True)
    self.t = t
  def insert(self, k):
      root=self.root
      if len(root.keys)==(2*self.t)-1:
          temp=BTreeNode()
          self.root=temp
          temp.child.insert(0,root)
          self.split_child(temp,0)
          self.insert_non_full(temp,k)
      else:
          self.insert_non_full(root,k)
  def insert_non_full(self, x, k):
    i = len(x.keys) - 1
    if x.leaf:
      x.keys.append((None, None))
      while i >= 0 and k[0] < x.keys[i][0]:
        x.keys[i + 1] = x.keys[i]
        i -= 1
      x.keys[i + 1] = k
    else:
      while i >= 0 and k[0] < x.keys[i][0]:
        i -= 1
      i += 1
      if len(x.child[i].keys) == (2 * self.t) - 1:
        self.split_child(x, i)
        if k[0] > x.keys[i][0]:
          i += 1
      self.insert_non_full(x.child[i], k)
    # Split the child
  def split_child(self, x, i):
    t = self.t
    y = x.child[i]
    z = BTreeNode(y.leaf)
    x.child.insert(i + 1, z)
    x.keys.insert(i, y.keys[t - 1])
    z.keys = y.keys[t: (2 * t) - 1]
    y.keys = y.keys[0: t - 1]
    if not y.leaf:
      z.child = y.child[t: 2 * t]
      y.child = y.child[0: t - 1]
  # Print the tree
  def print_tree(self, x, l=0):
    print("Level ", l, " ", len(x.keys), end=":")
    for i in x.keys:
      print(i, end=" ")
    print()
    l += 1
    if len(x.child) > 0:
      for i in x.child:
        self.print_tree(i, l)
def main():
  B = BTree(3)
  for i in range(10):
    B.insert((i, 2 * i))
  print("B Tree :")
  B.print_tree(B.root)
  B.insert((11,))
  print("\nB Tree after insertion")
  B.print_tree(B.root)
if __name__ == '__main__':
  main()
```

## OUTPUT

<img width="1176" height="432" alt="image" src="https://github.com/user-attachments/assets/fa7e5a40-7f21-4ca0-b503-194de2f00d73" />

## RESULT
->The program builds a B-Tree of order 3, balancing nodes automatically.

->Full nodes are split correctly, and keys are promoted to maintain B-Tree properties.

->he print_tree() function displays the structure of the tree level by level.
