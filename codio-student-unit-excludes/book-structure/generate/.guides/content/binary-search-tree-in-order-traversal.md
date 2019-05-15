The last method I asked you to write is `keySet`, which returns a `Set` that contains the keys from the tree in ascending order. In other implementations of `Map`, the keys returned by `keySet` are in no particular order, but one of the capabilities of the tree implementation is that it is simple and efficient to sort the keys. So we should take advantage of that.


Here's my solution:

```code
public Set<K> keySet() {
    Set<K> set = new LinkedHashSet<K>();
    addInOrder(root, set);
    return set;
}

private void addInOrder(Node node, Set<K> set) {
    if (node == null) return;
    addInOrder(node.left, set);
    set.add(node.key);
    addInOrder(node.right, set);        
}
```

In `keySet`, we create a `LinkedHashSet`, which is a `Set` implementation that keeps the elements in order (unlike most other `Set` implementations). Then we call `addInOrder` to traverse the tree.


The first parameter, `node`, is initially the root of the tree, but as you should expect by now, we use it to traverse the tree recursively. `addInOrder` performs a classic “in-order traversal” of the tree.

If `node` is `null`, that means the subtree is empty, so we return without adding anything to `set`. Otherwise we:



1. 
Traverse the left subtree in order.

1. 
Add `node.key`.

1. 
Traverse the right subtree in order.


Remember that the BST property guarantees that all nodes in the left subtree are less than `node.key`, and all nodes in the right subtree are greater. So we know that `node.key` has been added in the correct order.


Applying the same argument recursively, we know that the elements from the left subtree are in order, as well as the elements from the right subtree.  And the base case is correct: if the subtree is empty, no keys are added.  So we can conclude that this method adds all keys in the correct order.

Because this method visits every node in the tree, like `containsValue`, it takes time proportional to $n$.