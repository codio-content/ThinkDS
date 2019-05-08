There are two possible solutions to this problem:



* 
You could avoid adding keys to the `Map` in order. But this is
not always possible.

* 
You could make a tree that does a better job of handling keys if they
happen to be in order.


The second solution is better, and there are several ways to do it. The most common is to modify `put` so that it detects when the tree is starting to become unbalanced and, if so, rearranges the nodes. Trees with this capability are called “self-balancing”. Common self-balancing trees include the AVL tree (“AVL” are the initials of the inventors), and the red-black tree, which is what the Java `TreeMap` uses.


In our example code, if we replace `MyTreeMap` with the Java `TreeMap`, the runtimes are about the same for the random strings and the timestamps. In fact, the timestamps run faster, even though they are in order, probably because they take less time to hash.


In summary, a binary search tree can implement `get` and `put` in logarithmic time, but only if the keys are added in an order that keeps the tree sufficiently balanced. Self-balancing trees avoid this problem by doing some additional work each time a new key is added.

You can read more about self-balancing trees at [http://thinkdast.com/balancing](http://thinkdast.com/balancing).