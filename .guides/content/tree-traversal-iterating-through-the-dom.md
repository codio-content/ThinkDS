To make your life easier, I provide a class called `WikiNodeIterable` that lets you iterate through the nodes in a DOM tree. Here's an example that shows how to use it:


```code
    Elements paragraphs = content.select("p");
    Element firstPara = paragraphs.get(0);

    Iterable<Node> iter = new WikiNodeIterable(firstPara);
    for (Node node: iter) {
        if (node instanceof TextNode) {
            System.out.print(node);
        }
    }
```

This example picks up where the previous one leaves off. It selects the first paragraph in `paragraphs` and then creates a `WikiNodeIterable`, which implements `Iterable<Node>`.  `WikiNodeIterable` performs a “depth-first search”, which produces the nodes in the order they would appear on the page.


In this example, we print a `Node` only if it is a `TextNode` and ignore other types of `Node`, specifically the `Element` objects that represent tags. The result is the plain text of the HTML paragraph without any markup. The output is:



> Java is a general-purpose computer programming language that is
> concurrent, class-based, object-oriented,{[}13{]} and specifically
> designed \ldots