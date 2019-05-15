My implementation of a linked list, `MyLinkedList`, uses a singly-linked list; that is, each element contains a link to the next, and the `MyArrayList` object itself has a link to the first node.


But if you read the documentation of `LinkedList` at [http://thinkdast.com/linked](http://thinkdast.com/linked), it says:



> Doubly-linked list implementation of the List and Deque
> interfaces. [\ldots] All of the operations perform as
> could be expected for a doubly-linked list. Operations that
> index into the list will traverse the list from the beginning or the
> end, whichever is closer to the specified index.


If you are not familiar with doubly-linked lists, you can read more about them at [http://thinkdast.com/doublelist](http://thinkdast.com/doublelist), but the short version is:



* 
Each node contains a link to the next node and a link to the previous
node.

* 
The `LinkedList` object contains links to the first and last
elements of the list.


So we can start at either end of the list and traverse it in either direction. As a result, we can add and remove elements from the beginning and the end of the list in constant time!


The following table summarizes the performance we expect from `ArrayList`, `MyLinkedList` (singly-linked), and `LinkedList` (doubly-linked):

|& MyArrayList|MyLinkedList|LinkedList|
|-|-|-|
|add (at the end)|**1**|n|**1**|
|add (at the beginning)|n|**1**|**1**|
|add (in general)|n|n|n|
|get / set|**1**|n|n|
|indexOf / lastIndexOf|n|n|n|
|isEmpty / size|1|1|1|
|remove (from the end)|**1**|n|**1**|
|remove (from the beginning)|n|**1**|**1**|
|remove (in general)|n|n|n|