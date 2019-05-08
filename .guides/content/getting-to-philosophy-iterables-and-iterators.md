In the previous chapter, I presented an iterative depth-first search (DFS), and suggested that an advantage of the iterative version, compared to the recursive version, is that it is easier to wrap in an `Iterator` object. In this section we'll see how to do that.


If you are not familiar with the `Iterator` and `Iterable` interfaces, you can read about them at [http://thinkdast.com/iterator](http://thinkdast.com/iterator) and [http://thinkdast.com/iterable](http://thinkdast.com/iterable).

Take a look at the contents of `WikiNodeIterable.java`. The outer class, `WikiNodeIterable` implements the `Iterable<Node>` interface  so we can use it in a for loop like this:

```code
    Node root = ...
    Iterable<Node> iter = new WikiNodeIterable(root);
    for (Node node: iter) {
        visit(node);
    }
```

where `root` is the root of the tree we want to traverse and `visit` is a method that does whatever we want when we “visit” a `Node`.


The implementation of `WikiNodeIterable` follows a conventional formula:



1. 
The constructor takes and stores a reference to the root
`Node`.

1. 
The `iterator` method creates a returns an `Iterator`
object.


Here's what it looks like:

```code
public class WikiNodeIterable implements Iterable<Node> {

    private Node root;

    public WikiNodeIterable(Node root) {
        this.root = root;
    }

    @Override
    public Iterator<Node> iterator() {
        return new WikiNodeIterator(root);
    }
}
```

The inner class, `WikiNodeIterator`, does all the real work:

```code
    private class WikiNodeIterator implements Iterator<Node> {

        Deque<Node> stack;

        public WikiNodeIterator(Node node) {
            stack = new ArrayDeque<Node>();
            stack.push(root);
        }

        @Override
        public boolean hasNext() {
            return !stack.isEmpty();
        }

        @Override
        public Node next() {
            if (stack.isEmpty()) {
                throw new NoSuchElementException();
            }

            Node node = stack.pop();
            List<Node> nodes = new ArrayList<Node>(node.childNodes());
            Collections.reverse(nodes);
            for (Node child: nodes) {
                stack.push(child);
            }
            return node;
        }
    }
```


This code is almost identical to the iterative version of DFS, but now it's split into three methods:



1. 
The constructor initializes the stack (which is implemented using an
`ArrayDeque`) and pushes the root node onto it.

1. 
`isEmpty` checks whether the stack is empty.

1. 
`next` pops the next `Node` off the stack, pushes its
children in reverse order, and returns the `Node` it popped. If
someone invokes `next` on an empty `Iterator`, it throws
an exception.


It might not be obvious that it is worthwhile to rewrite a perfectly good method with two classes and five methods.  But now that we've done it, we can use `WikiNodeIterable` anywhere an `Iterable` is called for, which makes it easy and syntactically clean to separate the logic of the iteration (DFS) from whatever processing we are doing on the nodes.