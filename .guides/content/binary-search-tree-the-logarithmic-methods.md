In `MyTreeMap`, the methods `get` and `put` take time proportional to the height of the tree, $h$. In the previous exercise, we showed that if the tree is full --- if every level of the tree contains the maximum number of nodes --- the height of the tree is proportional to $\log n$.


And I claimed that `get` and `put` are logarithmic; that is, they take time proportional to $\log n$. But for most applications, there's no guarantee that the tree is full. In general, the shape of the tree depends on the keys and what order they are added.

To see how this works out in practice, we'll test our implementation with two sample datasets: a list of random strings and a list of timestamps in increasing order.


Here's the code that generates random strings:

```code
Map<String, Integer> map = new MyTreeMap<String, Integer>();

for (int i=0; i<n; i++) {
    String uuid = UUID.randomUUID().toString();
    map.put(uuid, 0);
}
```

[Put code in the main method](open_file code/MyTreeMap.java panel=0 ref="public static void main" count=1)

{Run | terminal}(javac code/MyTreeMap.java && java -cp code MyTreeMap)


`UUID` is a class in the `java.util` package that can generate a random “universally unique identifier”. UUIDs are useful for a variety of applications, but in this example we're taking advantage of an easy way to generate random strings.


I ran this code with `n=16384` and measured the runtime and the height of the final tree. Here's the output:

```code
Time in milliseconds = 151
Final size of MyTreeMap = 16384
log base 2 of size of MyTreeMap = 14.0
Final height of MyTreeMap = 33
```

I included “log base 2 of size of MyTreeMap” to see how tall the tree would be if it were full. The result indicates that a full tree with height 14 would contain 16,384 nodes.

The actual tree of random strings has height 33, which is substantially more than the theoretical minimum, but not too bad. To find one key in a collection of 16,384, we only have to make 33 comparisons. Compared to a linear search, that's almost 500 times faster.


This performance is typical with random strings or other keys that are added in no particular order. The final height of the tree might be 2-3 times the theoretical minimum, but it is still proportional to $\log n$, which is much less than $n$. In fact, $\log n$ grows so slowly as $n$ increases, it can be difficult to distinguish logarithmic time from constant time in practice.


However, binary search trees don't always behave so well. Let's see what happens when we add keys in increasing order. Here's an example that measures timestamps in nanoseconds and uses them as keys:

```code
MyTreeMap<String, Integer> map = new MyTreeMap<String, Integer>();

for (int i=0; i<n; i++) {
    String timestamp = Long.toString(System.nanoTime());
    map.put(timestamp, 0);
}
```

[Put code in the `main` method](open_file code/MyTreeMap.java panel=0 ref="public static void main" count=1)

{Run | terminal}(javac code/MyTreeMap.java && java -cp code MyTreeMap)


`System.nanoTime` returns an integer with type `long` that indicates elapsed time in nanoseconds. Each time we call it, we get a somewhat bigger number. When we convert these timestamps to strings, they appear in increasing alphabetical order.

And let's see what happens when we run it:

```code
Time in milliseconds = 1158
Final size of MyTreeMap = 16384
log base 2 of size of MyTreeMap = 14.0
Final height of MyTreeMap = 16384
```

The runtime is more than seven times longer than in the previous case. longer. If you wonder why, take a look at the final height of the tree: 16384!

![Figure 13.1 Binary search trees, balanced (left) and unbalanced (right).](figs/bst.jpg)

**Figure 13.1 Binary search trees, balanced (left) and unbalanced (right).**

If you think about how `put` works, you can figure out what's going on. Every time we add a new key, it's larger than all of the keys in the tree, so we always choose the right subtree, and always add the new node as the right child of the rightmost node. The result is an “unbalanced” tree that only contains right children.


The height of this tree is proportional to $n$, not $\log n$, so the performance of `get` and `put` is linear, not logarithmic.


Figure 13.1 shows an example of a balanced and unbalanced tree.  In the balanced tree, the height is 4 and the total number of nodes is $2^4-1 = 15$.  In the unbalanced tree with the same number of nodes, the height is 15.