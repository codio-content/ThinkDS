Here is an iterative version of DFS that uses an `ArrayDeque` to represent a stack of `Node` objects: [Highlight in Code](open_file code/WikiNodeExample.java panel=0 ref="private static void iterativeDFS" count=23)



The parameter, `root`, is the root of the tree we want to traverse, so we start by creating the stack and pushing the root onto it.


The loop continues until the stack is empty. Each time through, it pops a `Node` off the stack. If it gets a `TextNode`, it prints the contents. Then it pushes the children onto the stack. In order to process the children in the right order, we have to push them onto the stack in reverse order; we do that by copying the children into an `ArrayList`, reversing the elements in place, and then iterating through the reversed `ArrayList`.

One advantage of the iterative version of DFS is that it is easier to implement as a Java `Iterator`; you'll see how in the next chapter.


But first, one last note about the `Deque` interface: in addition to `ArrayDeque`, Java provides another implementation of `Deque`, our old friend `LinkedList`. `LinkedList` implements both interfaces, `List` and `Deque`. Which interface you get depends on how you use it. For example, if you assign a `LinkedList` object to a `Deque` variable, like this:

```code
Deqeue<Node> deque = new LinkedList<Node>();
```

you can use the methods in the `Deque` interface, but not all methods in the `List` interface. If you assign it to a `List` variable, like this:

```code
List<Node> deque = new LinkedList<Node>();
```

you can use `List` methods but not all `Deque` methods. And if you assign it like this:

```code
LinkedList<Node> deque = new LinkedList<Node>();
```

you can use *all* the methods. But if you combine methods from different interfaces, your code will be less readable and more error-prone.