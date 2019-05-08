There are several ways you might reasonably traverse a tree, each with different applications. We'll start with “depth-first search”, or DFS. DFS starts at the root of the tree and selects the first child. If the child has children, it selects the first child again. When it gets to a node with no children, it backtracks, moving up the tree to the parent node, where it selects the next child if there is one; otherwise it backtracks again. When it has explored the last child of the root, it's done.


There are two common ways to implement DFS, recursively and iteratively. The recursive implementation is simple and elegant:

```code
private static void recursiveDFS(Node node) {
    if (node instanceof TextNode) {
        System.out.print(node);
    }
    for (Node child: node.childNodes()) {
        recursiveDFS(child);
    }
}
```

This method gets invoked on every `Node` in the tree, starting with the root. If the `Node` it gets is a `TextNode`, it prints the contents. If the `Node` has any children, it invokes `recursiveDFS` on each one of them in order.


In this example, we print the contents of each `TextNode` before traversing the children, so this is an example of a “pre-order” traversal. You can read about “pre-order”, “post-order”, and “in-order” traversals at [http://thinkdast.com/treetrav](http://thinkdast.com/treetrav).  For this application, the traversal order doesn't matter.


By making recursive calls, `recursiveDFS` uses the call stack ([http://thinkdast.com/callstack](http://thinkdast.com/callstack)) to keep track of the child nodes and process them in the right order. As an alternative, we can use a stack data structure to keep track of the nodes ourselves; if we do that, we can avoid the recursion and traverse the tree iteratively.