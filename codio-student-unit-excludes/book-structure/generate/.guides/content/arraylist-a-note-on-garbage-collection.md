In `MyArrayList` from the previous exercise, the array grows if necessary, but it never shrinks. The array never gets garbage collected, and the elements don't get garbage collected until the list itself is destroyed.


One advantage of the linked list implementation is that it shrinks when elements are removed, and the unused nodes can get garbage collected immediately.


Here is my implementation of the `clear` method:

```code
    public void clear() {
        head = null;
        size = 0;
    }
```

When we set `head` to `null`, we remove a reference to the first `Node`. If there are no other references to that `Node` (and there shouldn't be), it will get garbage collected. At that point, the reference to the second `Node` is removed, so it gets garbage collected, too. This process continues until all nodes are collected.

So how should we classify `clear`? The method itself contains two constant time operations, so it sure looks like it's constant time. But when you invoke it, you make the garbage collector do work that's proportional to the number of elements. So maybe we should consider it linear!


This is an example of what is sometimes called a **performance bug**: a program that is correct in the sense that it does the right thing, but it doesn't belong to the order of growth we expected. In languages like Java that do a lot of work, like garbage collection, behind the scenes, this kind of bug can be hard to find.