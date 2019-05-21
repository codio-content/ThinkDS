For the next exercise I provide a partial implementation of the `List` interface that uses a linked list to store the elements. If you are not familiar with linked lists, you can read about them at [http://thinkdast.com/linkedlist](http://thinkdast.com/linkedlist), but this section provides a brief introduction.


A data structure is “linked” if it is made up of objects, often called “nodes”, that contain references to other nodes. In a linked *list*, each node contains a reference to the next node in the list. Other linked structures include trees and graphs, in which nodes can contain references to more than one other node.

See the ListNode.java file in the top-left pane for a class definition for a simple node.


The `ListNode` object has two instance variables: `data` is a reference to some kind of `Object`, and `next` is a reference to the next node in the list. In the last node in the list, by convention, `next` is `null`. [Highlight in Code](open_file code/ListNode.java panel=0 ref="public Object data" count=2)



`ListNode` provides several constructors, allowing you to provide values for `data` and `next`, or initialize them to the default value, `null`. [Highlight in Code](open_file code/ListNode.java panel=0 ref="//constructors" count=15)



You can think of each `ListNode` as a list with a single element, but more generally, a list can contain any number of nodes. There are several ways to make a new list. A simple option is to create a set of `ListNode` objects, like this:

```code
        ListNode node1 = new ListNode(1);
        ListNode node2 = new ListNode(2);
        ListNode node3 = new ListNode(3);
```
[Highlight in Code](open_file code/LinkedListExample.java panel=1 ref="ListNode node1" count=3)


And then link them up, like this:

```code
        node1.next = node2;
        node2.next = node3;
        node3.next = null;
```
[Highlight in Code](open_file code/LinkedListExample.java panel=1 ref="node1.next" count=3)


Alternatively, you can create a node and link it at the same time. For example, if you want to add a new node at the beginning of a list, you can do it like this:

```code
        ListNode node0 = new ListNode(0, node1);
```
[Highlight in Code](open_file code/LinkedListExample.java panel=1 ref="ListNode node0" count=1)


After this sequence of instructions, we have four nodes containing the `Integer`s 0, 1, 2, and 3 as data, linked up in increasing order. In the last node, the `next` field is `null`.

![Figure 3.1 Object diagram of a linked list.](figs/linked_list1.jpg)

**Figure 3.1 Object diagram of a linked list.**


Figure 3.1 is an object diagram that shows these variables and the objects they refer to.  In an object diagram, variables appear as names inside boxes, with arrows that show what they refer to.  Objects appear as boxes with their type on the outside (like `ListNode` and `Integer`) and their instance variables on the inside.