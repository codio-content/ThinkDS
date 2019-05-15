In the repository for this book, you'll find these source files:



* 
`MyTreeMap.java` contains the code from the previous section
with outlines for the missing methods.

* 
`MyTreeMapTest.java` contains the unit tests for
`MyTreeMap`.


Run `ant build` to compile the source files. Then run `ant   MyTreeMapTest`.  Several tests should fail, because you have some work to do!


I've provided outlines for `get` and `containsKey`.  Both of them use `findNode`, which is a private method I defined; it is not part of the `Map` interface. Here's how it starts:

```code
    private Node findNode(Object target) {
        if (target == null) {
            throw new IllegalArgumentException();
        }

        @SuppressWarnings("unchecked")
        Comparable<? super K> k = (Comparable<? super K>) target;

        // TODO: FILL THIS IN!
        return null;
    }
```


The parameter `target` is the key we're looking for. If `target` is `null`, `findNode` throws an exception. Some implementations of `Map` can handle `null` as a key, but in a binary search tree, we need to be able to compare keys, so dealing with `null` is problematic. To keep things simple, this implementation does not allow `null` as a key.

The next lines show how we can compare `target` to a key in the tree. From the signature of `get` and `containsKey`, the compiler considers `target` to be an `Object`. But we need to be able to compare keys, so we typecast `target` to `Comparable<? super K>`, which means that it is comparable to an instance of type `K`, or any superclass of `K`.  If you are not familiar with this use of “type wildcards”, you can read more at [http://thinkdast.com/gentut](http://thinkdast.com/gentut).


Fortunately, dealing with Java's type system is not the point of this exercise. Your job is to fill in the rest of `findNode`. If it finds a node that contains `target` as a key, it should return the node. Otherwise it should return `null`. When you get this working, the tests for `get` and `containsKey` should pass.

Note that your solution should only search one path through the tree, so it should take time proportional to the height of the tree. You should not search the whole tree!


Your next task is to fill in `containsValue`. To get you started, I've provided a helper method, `equals`, that compares `target` and a given key. Note that the values in the tree (as opposed to the keys) are not necessarily comparable, so we can't use `compareTo`; we have to invoke `equals` on `target`.


Unlike your previous solution for `findNode`, your solution for `containsValue` *does* have to search the whole tree, so its runtime is proportional to the number of keys, $n$, not the height of the tree, `h`.

The next method you should fill in is `put`. I've provided   starter code that handles the simple cases:

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

    private V putHelper(Node node, K key, V value) {
        // TODO: Fill this in.
    }
```

If you try to put `null` as a key, `put` throws an exception.

If the tree is empty, `put` creates a new node and initializes the instance variable `root`.


Otherwise, it calls `putHelper`, which is a private method I defined; it is not part of the `Map` interface.

Fill in `putHelper` so it searches the tree and:



1. 
If `key` is already in the tree, it replaces the old value with
the new, and returns the old value.

1. 
If `key` is not in the tree, it creates a new node, finds the
right place to add it, and returns `null`.


Your implementation of `put` should take time proportional to the height of the tree, $h$, not the number of elements, $n$. Ideally you should search the tree only once, but if you find it easier to search twice, you can do that; it will be slower, but it doesn't change the order of growth.


Finally, you should fill in the body of `keySet`.  According to the documentation at [http://thinkdast.com/mapkeyset](http://thinkdast.com/mapkeyset), this method should return a `Set` that iterates the keys in order; that is, in increasing order according to the `compareTo` method.  The `HashSet` implementation of `Set`, which we used in Section 8.3, doesn't maintain the order of the keys, but the `LinkedHashSet` implementation does.  You can read about it at [http://thinkdast.com/linkedhashset](http://thinkdast.com/linkedhashset).

I've provided an outline of `keySet` that creates and returns a `LinkedHashSet`:

```code
    public Set<K> keySet() {
        Set<K> set = new LinkedHashSet<K>();
        return set;
    }
```


You should finish off this method so it adds the keys from the tree to `set` in ascending order. HINT: you might want to write a helper method; you might want to make it recursive; and you might want to read about in-order tree traversal at [http://thinkdast.com/inorder](http://thinkdast.com/inorder).



When you are done, all tests should pass. In the next chapter, I'll go over my solutions and test the performance of the core methods.