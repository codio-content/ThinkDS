For this exercise you will write an implementation of the `Map` interface using a binary search tree.


Here's the beginning of an implementation, called `MyTreeMap`: [Highlight in Code](open_file code/MyTreeMap.java panel=0 ref="public class MyTreeMap" count=4)



The instance variables are `size`, which keeps track of the number of keys, and `root`, which is a reference to the root node in the tree. When the tree is empty, `root` is `null` and `size` is 0.

Here's the definition of `Node`, which is defined inside `MyTreeMap`: [Highlight in Code](open_file code/MyTreeMap.java panel=0 ref="protected class Node" count=16)




Each node contains a key-value pair and references to two child nodes, `left` and `right`. Either or both of the child nodes can be `null`.

Some of the `Map` methods are easy to implement, like `size` and `clear`: [Highlight in Code](open_file code/MyTreeMap.java panel=0 ref="public int size" count=9)



`size` is clearly constant time.


`clear` appears to be constant time, but consider this: when `root` is set to `null`, the garbage collector reclaims the nodes in the tree, which takes linear time. Should work done by the garbage collector count? I think so.


In the next section, you'll fill in some of the other methods, including the most important ones, `get` and `put`.