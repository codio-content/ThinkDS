As I explained in the previous exercise, the runtime of `findNode` is proportional to the height of the tree, not the number of nodes, because we don't have to search the whole tree. But for `containsValue`, we have to search the values, not the keys; the BST property doesn't apply to the values, so we have to search the whole tree.


My solution is recursive:

```code
public boolean containsValue(Object target) {
    return containsValueHelper(root, target);
}

private boolean containsValueHelper(Node node, Object target) {
    if (node == null) {
        return false;
    }
    if (equals(target, node.value)) {
        return true;
    }
    if (containsValueHelper(node.left, target)) {
        return true;
    }
    if (containsValueHelper(node.right, target)) {
        return true;
    }
    return false;
}
```

`containsValue` takes the target value as a parameter and immediately invokes `containsValueHelper`, passing the root of the tree as an additional parameter.


Here's how `containsValueHelper` works:



* 
The first `if` statement checks the base case of the recursion.
If `node` is `null`, that means we have recursed to the
bottom of the tree without finding the `target`, so we should
return `false`. Note that this only means that the target did
not appear on one path through the tree; it is still possible that it
will be found on another.

* 
The second case checks whether we've found what we're looking for. If
so, we return `true`. Otherwise, we have to keep going.

* 
The third case makes a recursive call to search for `target` in
the left subtree. If we find it, we can return `true`
immediately, without searching the right subtree. Otherwise, we keep
going.

* 
The fourth case searches the right subtree. Again, if we find what we
are looking for, we return `true`. Otherwise, having searched
the whole tree, we return `false`.


This method “visits” every node in the tree, so it takes time proportional to the number of nodes.