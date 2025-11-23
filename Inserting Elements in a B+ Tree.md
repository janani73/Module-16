# Ex. No: 16D - Implementation of B+ Tree Using Python

## AIM:
To demonstrate insertion, node splitting, and retrieval in a B+ tree, a self-balancing tree used in databases and file systems.
## ALGORITHM:
```
1.Define a Node class:
       ->Each node stores keys, values, order, and a leaf flag.
       ->add(key, value): Inserts a key-value pair in sorted order; duplicates are stored in a list.
       ->split(): Splits a full node into two nodes and promotes the first key of the right node.
       ->is_full(): Checks if the node reached its maximum capacity.
       ->show(): Recursively prints the node keys with indentation.
2.Define a BPlusTree class:
       ->insert(key, value):
              ->Traverse down to the appropriate leaf node.
              ->Insert the key-value pair.
              ->If the leaf node is full, split it and merge with the parent if necessary.
       ->retrieve(key): Traverse to the leaf and return the values corresponding to the key.
       ->show(): Print the full tree structure.
3.Demo functions:
       ->demo_node(): Shows adding keys to a node and splitting it.
       ->demo_bplustree(): Builds a small B+ tree with initial insertions and includes user input for demonstration.
```
## PYTHON PROGRAM

```
class Node(object):
    def __init__(self, order):
        self.order = order
        self.keys = []
        self.values = []
        self.leaf = True
    def add(self, key, value):
        if not self.keys:
            self.keys.append(key)
            self.values.append([value])
            return None
        for i, item in enumerate(self.keys):
            if key == item:
                self.values[i].append(value)
                break
            elif key < item:
                self.keys = self.keys[:i] + [key] + self.keys[i:]
                self.values = self.values[:i] + [[value]] + self.values[i:]
                break
            elif i + 1 == len(self.keys):
                self.keys.append(key)
                self.values.append([value])
    def split(self):
        left = Node(self.order)
        right = Node(self.order)
        mid = self.order // 2
        left.keys = self.keys[:mid]
        left.values = self.values[:mid]
        right.keys = self.keys[mid:]
        right.values = self.values[mid:]
        self.keys = [right.keys[0]]
        self.values = [left, right]
        self.leaf = False
    def is_full(self):
        return len(self.keys) == self.order
    def show(self, counter=0):
        print(counter, str(self.keys))
        if not self.leaf:
            for item in self.values:
                item.show(counter + 1)
class BPlusTree(object):
    def __init__(self, order=8):
        self.root = Node(order)
    def _find(self, node, key):
        for i, item in enumerate(node.keys):
            if key < item:
                return node.values[i], i
        return node.values[i + 1], i + 1
    def _merge(self, parent, child, index):
        parent.values.pop(index)
        pivot = child.keys[0]
        for i, item in enumerate(parent.keys):
            if pivot < item:
                parent.keys = parent.keys[:i] + [pivot] + parent.keys[i:]
                parent.values = parent.values[:i] + child.values + parent.values[i:]
                break
            elif i + 1 == len(parent.keys):
                parent.keys += [pivot]
                parent.values += child.values
                break
    def insert( self,key, value):
        parent=None
        child=self.root
        while not child.leaf:
            parent=child
            child,index=self._find(child,key)
        child.add(key,value)
        if child.is_full():
            child.split()
            if parent and not parent.is_full():
                self._merge(parent,child,index)
    def retrieve(self, key):
        child = self.root
        while not child.leaf:
            child, index = self._find(child, key)
        for i, item in enumerate(child.keys):
            if key == item:
                return child.values[i]
        return None
    def show(self):
        self.root.show()
def demo_node():
    node = Node(order=4)
    node.add('a', 'alpha')
    node.add('b', 'bravo')
    node.add('c', 'charlie')
    node.add('d', 'delta')
    node.show()
    print('\nSplitting node...')
    node.split()
    node.show()
def demo_bplustree():
    print('B+ tree...')
    bplustree = BPlusTree(order=4)
    x=input()
    y=input()
    bplustree.insert('a', 'alpha')
    bplustree.insert('b', 'bravo')
    bplustree.insert('c', 'charlie')
    bplustree.insert('d', 'delta')
    bplustree.insert('e', 'echo')
   # fix the code below   
    bplustree.insert(x,y)
    bplustree.show()
if __name__ == '__main__':
    demo_node()
    print('\n')
    demo_bplustree()
```

## OUTPUT

<img width="1177" height="482" alt="image" src="https://github.com/user-attachments/assets/ddbf5123-d6f9-4f17-a184-c55a38ee7da9" />

## RESULT
->The program successfully inserts elements into a B+ tree.

->Nodes are split automatically when they become full, maintaining the B+ tree property.

->The tree structure can be visualized using the show() method.

->New key-value pairs, including user input, are inserted properly.
