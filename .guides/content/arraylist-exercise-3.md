you'll find the source files you need for this exercise:




*  `MyLinkedList.java` contains a partial implementation of
the `List` interface using a linked list to store the elements.

*  `MyLinkedListTest.java` contains JUnit tests for
`MyLinkedList`.


Run `ant MyLinkedList` to run `MyLinkedList.java`, which contains a few simple tests. 

Then you can run `ant MyLinkedListTest` to run the JUnit tests. Several of them should fail. If you examine the source code, you'll find three `TODO` comments indicating the methods you should fill in.

Before you start, let's walk through some of the code. Here are the instance variables and the constructor for `MyLinkedList`:

```code
public class MyLinkedList<E> implements List<E> {

    private int size;            // keeps track of the number of elements
    private Node head;           // reference to the first node

    public MyLinkedList() {
        head = null;
        size = 0;
    }
}
```

As the comments indicate, `size` keeps track of how many elements are in `MyLinkedList`; `head` is a reference to the first `Node` in the list or `null` if the list is empty.


Storing the number of elements is not necessary, and in general it is risky to keep redundant information, because if it's not updated correctly, it creates opportunities for error. It also takes a little bit of extra space.


But if we store `size` explicitly, we can implement the `size` method in constant time; otherwise, we would have to traverse the list and count the elements, which requires linear time.


Because we store `size` explicitly, we have to update it each time we add or remove an element, so that slows down those methods a little, but it doesn't change their order of growth, so it's probably worth it.

The constructor sets `head` to `null`, which indicates an empty list, and sets `size` to 0.


This class uses the type parameter `E` for the type of the elements. If you are not familiar with type parameters, you might want to read this tutorial: [http://thinkdast.com/types](http://thinkdast.com/types).

The type parameter also appears in the definition of `Node`, which is nested inside `MyLinkedList`:

```code
    private class Node {
        public E data;
        public Node next;

        public Node(E data, Node next) {
            this.data = data;
            this.next = next;
        }
    }
```

Other than that, `Node` is similar to `ListNode` above.


Finally, here's my implementation of `add`:

```code
    public boolean add(E element) {
        if (head == null) {
            head = new Node(element);
        } else {
            Node node = head;
            // loop until the last node
            for ( ; node.next != null; node = node.next) {}
            node.next = new Node(element);
        }
        size++;
        return true;
    }
```


This example demonstrates two patterns you'll need for your solutions:



1. 
For many methods, we have to handle the first element of the list as a
special case. In this example, if we are adding the first element of a
list, we have to modify `head`. Otherwise, we traverse the
list, find the end, and add the new node.

1. 
This method shows how to use a `for` loop to traverse the nodes
in a list. In your solutions, you will probably write several
variations on this loop. Notice that we have to declare `node`
before the loop so we can access it after the loop.


Now it's your turn.  Fill in the body of `indexOf`.  As usual, you should read the documentation, at [http://thinkdast.com/listindof](http://thinkdast.com/listindof), so you know what it is supposed to do. In particular, notice how it's supposed to handle `null`.


As in the previous exercise, I provide a helper method called `equals` that compares an element from the array to a target value and checks whether they are equal --- and it handles `null` correctly. This method is private because it is used inside this class but it is not part of the `List` interface.

When you are done, run the tests again; `testIndexOf` should pass now, as well as the other tests that depend on it.


Next, you should fill in the two-parameter version of `add`, which takes an index and stores the new value at the given index. Again, read the documentation at [http://thinkdast.com/listadd](http://thinkdast.com/listadd), write an implementation, and run the tests for confirmation.


Last one: fill in the body of `remove`.  The documentation is here: [http://thinkdast.com/listrem](http://thinkdast.com/listrem).  When you finish this one, all tests should pass.

Once you have your implementation working, compare it to the version in the `solution` directory of the repository.