The `put` method is a little more complicated than `get` because it has to deal with two cases: (1) if the given key is already in the tree, it replaces and returns the old value; (2) otherwise it has to add a new node to the tree, in the right place.


In the previous exercise, I provided this starter code:

```code
public V put(K key, V value) {
    if (key == null) {
        throw new IllegalArgumentException();
    }
    if (root == null) {
        root = new Node(key, value);
        size++;
        return null;
    }
    return putHelper(root, key, value);
}
```

And asked you to fill in `putHelper`. Here's my solution:

```code
private V putHelper(Node node, K key, V value) {
    Comparable<? super K> k = (Comparable<? super K>) key;
    int cmp = k.compareTo(node.key);

    if (cmp < 0) {
        if (node.left == null) {
            node.left = new Node(key, value);
            size++;
            return null;
        } else {
            return putHelper(node.left, key, value);
        }
    }
    if (cmp > 0) {
        if (node.right == null) {
            node.right = new Node(key, value);
            size++;
            return null;
        } else {
            return putHelper(node.right, key, value);
        }
    }
    V oldValue = node.value;
    node.value = value;
    return oldValue;
}
```


The first parameter, `node`, is initially the root of the tree, but each time we make a recursive call, it refers to a different subtree.  As in `get`, we use the `compareTo` method to figure out which path to follow through the tree.  If `cmp < 0`, the key we're adding is less than `node.key`, so we want to look in the left subtree. There are two cases:



*  If the left subtree is empty, that is, if `node.left` is `null`, we have reached the bottom of the tree without finding `key`. At this point, we know that `key` isn't in the tree, and we know where it should go. So we create a new node and add it as the left child of `node`.
*  Otherwise we make a recursive call to search the left subtree. 

If `cmp > 0`, the key we're adding is greater than `node.key`, so we want to look in the right subtree. And we handle the same two cases as in the previous branch. Finally, if `cmp == 0`, we found the key in the tree, so we replace and return the old value.


I wrote this method recursively to make it more readable, but it would be straightforward to rewrite it iteratively, which you might want to do as an exercise.