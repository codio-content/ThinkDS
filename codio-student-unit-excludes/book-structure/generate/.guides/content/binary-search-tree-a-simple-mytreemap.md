In the previous exercise I gave you the outline of `MyTreeMap` and asked you to fill in the missing methods. Now I'll present a solution, starting with `findNode`:


```code
private Node findNode(Object target) {
    // some implementations can handle null as a key, but not this one
    if (target == null) {
            throw new IllegalArgumentException();
    }

    // something to make the compiler happy
    @SuppressWarnings("unchecked")
    Comparable<? super K> k = (Comparable<? super K>) target;

    // the actual search
    Node node = root;
    while (node != null) {
        int cmp = k.compareTo(node.key);
        if (cmp < 0)
            node = node.left;
        else if (cmp > 0)
            node = node.right;
        else
            return node;
    }
    return null;
}
```

`findNode` is a private method used by `containsKey` and `get`; it is not part of the `Map` interface. The parameter `target` is the key we're looking for. I explained the first part of this method in the previous exercise:



* 
In this implementation, `null` is not a legal value for a key.

* 
Before we can invoke `compareTo` on `target`, we have to
typecast it to some kind of `Comparable`. The “type wildcard”
used here is as permissive as possible; that is, it works with any
type that implements `Comparable` and whose `compareTo`
method accepts `K` or any supertype of `K`.



After all that, the actual search is relatively simple. We initialize a loop variable `node` so it refers to the root node. Each time through the loop, we compare the target to `node.key`. If the target is less than the current key, we move to the left child. If it's greater, we move to the right child. And if it's equal, we return the current node.

If we get to the bottom of the tree without finding the target, we conclude that it is not in the tree and return `null`.