In the panes to the right,

you'll find the source files you need for this exercise:




*  `MyLinkedList.java` contains a partial implementation of
the `List` interface using a linked list to store the elements.

*  `MyLinkedListTest.java` contains JUnit tests for
`MyLinkedList`.


Several of them should fail. If you examine the source code, you'll find three `TODO` comments indicating the methods you should fill in. Before you start, let's walk through some of the code. Find the instance variables and constructor for `MyLinkedList.java` in the top-left panel. [Highlight Code](open_file code/MyLinkedList.java panel=1 ref="public class MyLinkedList" count=10)



As the comments indicate, `size` keeps track of how many elements are in `MyLinkedList`; `head` is a reference to the first `Node` in the list or `null` if the list is empty.


Storing the number of elements is not necessary, and in general it is risky to keep redundant information, because if it's not updated correctly, it creates opportunities for error. It also takes a little bit of extra space.


But if we store `size` explicitly, we can implement the `size` method in constant time; otherwise, we would have to traverse the list and count the elements, which requires linear time.


Because we store `size` explicitly, we have to update it each time we add or remove an element, so that slows down those methods a little, but it doesn't change their order of growth, so it's probably worth it.

The constructor sets `head` to `null`, which indicates an empty list, and sets `size` to 0.


This class uses the type parameter `E` for the type of the elements. If you are not familiar with type parameters, you might want to read this tutorial: [http://thinkdast.com/types](http://thinkdast.com/types).

The type parameter also appears in the definition of `Node`, which is nested inside `MyLinkedList`: [Highlight Code](open_file code/MyLinkedList.java panel=1 ref="private class Node" count=9)



Other than that, `Node` is similar to `ListNode` above.


Finally, here's my implementation of `add`: [Highlight Code](open_file code/MyLinkedList.java panel=1 ref="public boolean add" count=12)




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


Now it's your turn.  Fill in the body of `indexOf`.  As usual, you should read the documentation, at [http://thinkdast.com/listindof](http://thinkdast.com/listindof), so you know what it is supposed to do. In particular, notice how it's supposed to handle `null`. [Highlight Code](open_file code/MyLinkedList.java panel=1 ref="public public int indexOf" count=4)



As in the previous exercise, I provide a helper method called `equals` that compares an element from the array to a target value and checks whether they are equal --- and it handles `null` correctly. This method is private because it is used inside this class but it is not part of the `List` interface.

When you are done, run the tests again; `testIndexOf` should pass now, as well as the other tests that depend on it.


Next, you should fill in the two-parameter version of `add`, which takes an index and stores the new value at the given index. Again, read the documentation at [http://thinkdast.com/listadd](http://thinkdast.com/listadd), write an implementation, and run the tests for confirmation. [Highlight Code](open_file code/MyLinkedList.java panel=1 ref="public void add" count=3)



Last one: fill in the body of `remove`.  The documentation is here: [http://thinkdast.com/listrem](http://thinkdast.com/listrem).  When you finish this one, all tests should pass. [Highlight Code](open_file code/MyLinkedList.java panel=1 ref="public E remove" count=4)
